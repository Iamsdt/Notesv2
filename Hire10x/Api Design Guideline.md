# API design guide

 bookmark_border

[Changelog](https://cloud.google.com/apis/design/changelog)

## Introduction

This is a general design guide for networked APIs. It has been used inside Google since 2014 and is the guide that Google follows when designing [Cloud APIs](https://cloud.google.com/apis/docs/overview) and other [Google APIs](https://github.com/googleapis/googleapis). This design guide is shared here to inform outside developers and to make it easier for us all to work together.

[Cloud Endpoints](https://cloud.google.com/endpoints/docs/grpc) developers may find this guide particularly useful when designing gRPC APIs, and we strongly recommend such developers use these design principles. However, we don't mandate its use. You can use Cloud Endpoints and gRPC without following the guide.

This guide applies to both REST APIs and RPC APIs, with specific focus on gRPC APIs. gRPC APIs use [Protocol Buffers](https://cloud.google.com/apis/design/proto3) to define their API surface and [API Service Configuration](https://github.com/googleapis/googleapis/blob/master/google/api/service.proto) to configure their API services, including HTTP mapping, logging, and monitoring. HTTP mapping features are used by Google APIs and Cloud Endpoints gRPC APIs for JSON/HTTP to Protocol Buffers/RPC [transcoding](https://cloud.google.com/endpoints/docs/transcoding).

This guide is a living document and additions to it will be made over time as new style and design patterns are adopted and approved. In that spirit, it is never going to be complete and there will always be ample room for the art and craft of API design.

## Conventions Used in This Guide

The requirement level keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" used in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

In this document, such keywords are highlighted using **bold** font.

## Sections

- [Resource-oriented Design](https://cloud.google.com/apis/design/resources)
- [Resource Names](https://cloud.google.com/apis/design/resource_names)
- [Standard Methods](https://cloud.google.com/apis/design/standard_methods)
- [Custom Methods](https://cloud.google.com/apis/design/custom_methods)
- [Standard Fields](https://cloud.google.com/apis/design/standard_fields)
- [Errors](https://cloud.google.com/apis/design/errors)
- [Naming Conventions](https://cloud.google.com/apis/design/naming_convention)
- [Design Patterns](https://cloud.google.com/apis/design/design_patterns)
- [Documentation](https://cloud.google.com/apis/design/documentation)
- [Using proto3](https://cloud.google.com/apis/design/proto3)
- [Versioning](https://cloud.google.com/apis/design/versioning)
- [Compatibility](https://cloud.google.com/apis/design/compatibility)
- [Directory Structure](https://cloud.google.com/apis/design/directory_structure)
- [File Structure](https://cloud.google.com/apis/design/file_structure)
- [Glossary](https://cloud.google.com/apis/design/glossary)


# Resource-oriented design

 bookmark_border

The goal for this Design Guide is to help developers design **simple, consistent and easy-to-use** networked APIs. At the same time, it also helps converging designs of socket-based RPC APIs with HTTP-based REST APIs.

RPC APIs are often designed in terms of interfaces and methods. As more and more of these are added over time, the end result can be an overwhelming and confusing API surface due to the fact that developers must learn each method individually. Obviously this is both time consuming and error-prone.

The architectural style of [REST](http://en.wikipedia.org/wiki/Representational_state_transfer) was introduced, primarily designed to work well with HTTP/1.1, but also to help tackle this problem. Its core principle is to define named resources that can be manipulated using a small number of methods. The resources and methods are known as _nouns_ and _verbs_ of APIs. With the HTTP protocol, the resource names naturally map to URLs, and methods naturally map to HTTP methods `POST`, `GET`, `PUT`, `PATCH`, and `DELETE`. This results in much fewer things to learn, since developers can focus on the resources and their relationship, and assume that they have the same small number of standard methods.

On the Internet, HTTP REST APIs have been hugely successful. In 2010, about 74% of public network APIs were HTTP REST (or REST-like) APIs, most using JSON as the wire format.

While HTTP/JSON APIs are very popular on the Internet, the amount of traffic they carry is smaller than traditional RPC APIs. For example, about half of Internet traffic in America at peak time is video content, and few people would consider using HTTP/JSON APIs to deliver such content for obvious performance reasons. Inside data centers, many companies use socket-based RPC APIs to carry most network traffic, which can involve orders of magnitude more data (measured in bytes) than public HTTP/JSON APIs.

In reality, both RPC APIs and HTTP/JSON APIs are needed for various reasons, and ideally, an API platform should provide best support for all types of APIs. This Design Guide helps you design and build APIs that conform to this principle. It does so by applying resource-oriented design principles to general API design and defines many common design patterns to improve usability and reduce complexity.

**Note:** This Design Guide explains how to apply REST principles to API designs independent of programming language, operating system, or network protocol. It is NOT a guide solely to creating REST APIs.

## What is a REST API?

A REST API is modeled as _collections_ of individually-addressable _resources_ (the _nouns_ of the API). Resources are referenced with their [resource names](https://cloud.google.com/apis/design/resource_names) and manipulated via a small set of _methods_ (also known as _verbs_ or _operations_).

_Standard methods_ for REST Google APIs (also known as _REST methods_) are `List`, `Get`, `Create`, `Update`, and `Delete`. _Custom methods_ (also known as _custom verbs_ or _custom operations_) are also available to API designers for functionality that doesn't easily map to one of the standard methods, such as database transactions.

**Note:** Custom verbs does not mean creating custom HTTP verbs to support custom methods. For HTTP-based APIs, they simply map to the most suitable HTTP verbs.

## Design flow

The Design Guide suggests taking the following steps when designing resource- oriented APIs (more details are covered in specific sections below):

- Determine what types of resources an API provides.
- Determine the relationships between resources.
- Decide the resource name schemes based on types and relationships.
- Decide the resource schemas.
- Attach minimum set of methods to resources.

## Resources

A resource-oriented API is generally modeled as a resource hierarchy, where each node is either a _simple resource_ or a _collection resource_. For convenience, they are often called a resource and a collection, respectively.

- A collection contains a list of resources of **the same type**. For example, a user has a collection of contacts.
- A resource has some state and zero or more sub-resources. Each sub-resource can be either a simple resource or a collection resource.

For example, Gmail API has a collection of users, each user has a collection of messages, a collection of threads, a collection of labels, a profile resource, and several setting resources.

While there is some conceptual alignment between storage systems and REST APIs, a service with a resource-oriented API is not necessarily a database, and has enormous flexibility in how it interprets resources and methods. For example, creating a calendar event (resource) may create additional events for attendees, send email invitations to attendees, reserve conference rooms, and update video conference schedules.

## Methods

The key characteristic of a resource-oriented API is that it emphasizes resources (data model) over the methods performed on the resources (functionality). A typical resource-oriented API exposes a large number of resources with a small number of methods. The methods can be either the standard methods or custom methods. For this guide, the standard methods are: `List`, `Get`, `Create`, `Update`, and `Delete`.

Where API functionality naturally maps to one of the standard methods, that method **should** be used in the API design. For functionality that does not naturally map to one of the standard methods, _custom methods_ **may** be used. [Custom methods](https://cloud.google.com/apis/design/custom_methods) offer the same design freedom as traditional RPC APIs, which can be used to implement common programming patterns, such as database transactions or data analysis.

## Examples

The following sections present a few real world examples on how to apply resource-oriented API design to large scale services. You can find more examples in the [Google APIs](https://github.com/googleapis/googleapis) repository.

In these examples, the asterisk indicates one specific resource out of the list.

### Gmail API

The Gmail API service implements the Gmail API and exposes most of Gmail functionality. It has the following resource model:

- API service: `gmail.googleapis.com`
    - A collection of users: `users/*`. Each user has the following resources.
        - A collection of messages: `users/*/messages/*`.
        - A collection of threads: `users/*/threads/*`.
        - A collection of labels: `users/*/labels/*`.
        - A collection of change history: `users/*/history/*`.
        - A resource representing the user profile: `users/*/profile`.
        - A resource representing user settings: `users/*/settings`.

### Cloud Pub/Sub API

The `pubsub.googleapis.com` service implements the [Cloud Pub/Sub API](https://cloud.google.com/pubsub), which defines the following resource model:

- API service: `pubsub.googleapis.com`
    - A collection of topics: `projects/*/topics/*`.
    - A collection of subscriptions: `projects/*/subscriptions/*`.

**Note:** Other implementations of the Pub/Sub API may choose different resource naming schemes.



# Resource names

 bookmark_border

In resource-oriented APIs, _resources_ are named entities, and _resource names_ are their identifiers. Each resource **must** have its own unique resource name. The resource name is made up of the ID of the resource itself, the IDs of any parent resources, and its API service name. We'll look at resource IDs and how a resource name is constructed below.

gRPC APIs should use scheme-less [URIs](https://datatracker.ietf.org/doc/html/rfc3986) for resource names. They generally follow the REST URL conventions and behave much like network file paths. They can be easily mapped to REST URLs: see the [Standard Methods](https://cloud.google.com/apis/design/standard_methods) section for details.

A _collection_ is a special kind of resource that contains a list of sub-resources of identical type. For example, a directory is a collection of file resources. The resource ID for a collection is called collection ID.

The resource name is organized hierarchically using collection IDs and resource IDs, separated by forward slashes. If a resource contains a sub-resource, the sub-resource's name is formed by specifying the parent resource name followed by the sub-resource's ID - again, separated by forward slashes.

Example 1: A storage service has a collection of `buckets`, where each bucket has a collection of `objects`:

|API Service Name|Collection ID|Resource ID|Collection ID|Resource ID|
|---|---|---|---|---|
|//storage.googleapis.com|/buckets|/bucket-id|/objects|/object-id|

Example 2: An email service has a collection of `users`. Each user has a `settings` sub-resource, and the `settings` sub-resource has a number of other sub-resources, including `customFrom`:

|API Service Name|Collection ID|Resource ID|Resource ID|Resource ID|
|---|---|---|---|---|
|//mail.googleapis.com|/users|/name@example.com|/settings|/customFrom|

An API producer can choose any acceptable value for resource and collection IDs as long as they are unique within the resource hierarchy. You can find more guidelines for choosing appropriate resource and collection IDs below.

By splitting the resource name, such as `name.split("/")[n]`, one can obtain the individual collection IDs and resource IDs, assuming none of the segments contains any forward slash.

## Full Resource Name

A scheme-less [URI](https://datatracker.ietf.org/doc/html/rfc3986) consisting of a [DNS-compatible](https://datatracker.ietf.org/doc/html/rfc1035) API service name and a resource path. The resource path is also known as _relative resource name_. For example:

```
"//library.googleapis.com/shelves/shelf1/books/book2"
```

The API service name is for clients to locate the API service endpoint; it **may** be a fake DNS name for internal-only services. If the API service name is obvious from the context, relative resource names are often used.

## Relative Resource Name

A URI path ([path-noscheme](https://datatracker.ietf.org/doc/html/rfc3986#appendix-A)) without the leading "/". It identifies a resource within the API service. For example:

```
"shelves/shelf1/books/book2"
```

## Resource ID

A resource ID typically consists of one or more non-empty URI segments ([segment-nz-nc](https://datatracker.ietf.org/doc/html/rfc3986#appendix-A)) that identify the resource within its parent resource, see above examples. The non-trailing resource ID in a resource name must have exactly one URL segment, while the trailing resource ID in a resource name **may** have more than one URI segment. For example:

|Collection ID|Resource ID|
|---|---|
|files|source/py/parser.py|

API services **should** use URL-friendly resource IDs when feasible. Resource IDs **must** be clearly documented whether they are assigned by the client, the server, or either. For example, file names are typically assigned by clients, while email message IDs are typically assigned by servers.

## Collection ID

A non-empty URI segment ([segment-nz-nc](https://datatracker.ietf.org/doc/html/rfc3986#appendix-A)) identifying the collection resource within its parent resource, see above examples.

Because collection IDs often appear in the generated client libraries, they **must** conform to the following requirements:

- **Must** be valid C/C++ identifiers.
- **Must** be in plural form with lowerCamel case. If the term doesn't have suitable plural form, such as "evidence" and "weather", the singular form **should** be used.
- **Must** use clear and concise English terms.
- Overly general terms **should** be avoided or qualified. For example, `rowValues` is preferred to `values`. The following terms **should** be avoided without qualification:
    - elements
    - entries
    - instances
    - items
    - objects
    - resources
    - types
    - values

## Resource Name vs URL

While full resource names resemble normal URLs, they are not the same thing. A single resource can be exposed by different API versions, API protocols, or API network endpoints. The full resource name does not specify such information, so it must be mapped to a specific API version and API protocol for actual use.

To use a full resource name via REST APIs, it **must** be converted to a REST URL by adding the HTTPS scheme before the service name, adding the API major version before the resource path, and URL-escaping the resource path. For example:

```
// This is a calendar event resource name."//calendar.googleapis.com/users/john smith/events/123"// This is the corresponding HTTP URL."https://calendar.googleapis.com/v3/users/john%20smith/events/123"
```

## Resource Name as String

Google APIs **must** represent resource names using plain strings, unless backward compatibility is an issue. Resource names **should** be handled like normal file paths. When a resource name is passed between different components, it must be treated as an atomic value and must not have any data loss.

For resource definitions, the first field **should** be a string field for the resource name, and it **should** be called `name`.

**Note:** The following code examples use [_gRPC Transcoding_](https://github.com/googleapis/googleapis/blob/master/google/api/http.proto) syntax. Please follow the link to see the details.

For example:

```
service LibraryService {  rpc GetBook(GetBookRequest) returns (Book) {    option (google.api.http) = {      get: "/v1/{name=shelves/*/books/*}"    };  };  rpc CreateBook(CreateBookRequest) returns (Book) {    option (google.api.http) = {      post: "/v1/{parent=shelves/*}/books"      body: "book"    };  };}message Book {  // Resource name of the book. It must have the format of "shelves/*/books/*".  // For example: "shelves/shelf1/books/book2".  string name = 1;  // ... other properties}message GetBookRequest {  // Resource name of a book. For example: "shelves/shelf1/books/book2".  string name = 1;}message CreateBookRequest {  // Resource name of the parent resource where to create the book.  // For example: "shelves/shelf1".  string parent = 1;  // The Book resource to be created. Client must not set the `Book.name` field.  Book book = 2;}
```

**Note:** For consistency of resource names, the leading forward slash **must not** be captured by any URL template variable. For example, URL template `"/v1/{name=shelves/*/books/*}"` **must** be used instead of `"/v1{name=/shelves/*/books/*}"`.

## Questions

### Q: Why not use resource IDs to identify a resource?

For any large system, there are many kinds of resources. To use resource IDs to identify a resource, we actually use a resource-specific tuple to identify a resource, such as `(bucket, object)` or `(user, album, photo)`. It creates several major problems:

- Developers have to understand and remember such anonymous tuples.
- Passing tuples is generally harder than passing strings.
- Centralized infrastructures, such as logging and access control systems, don't understand specialized tuples.
- Specialized tuples limit API design flexibility, such as providing reusable API interfaces. For example, [Long Running Operations](https://github.com/googleapis/googleapis/tree/master/google/longrunning) can work with many other API interfaces because they use flexible resource names.

### Q: Why is the resource name field called `name` instead of `id`?

The resource name field is named after the concept of resource "name". In general, we find the concept of `name` is confusing to developers. For example, is filename really just the name or the full path? By reserving the standard field `name`, developers are forced to choose a more proper term, such as `display_name` or `title` or `full_name`.

### Q: How should I generate and parse resource names?

Resource names behave like file paths. You can use `printf()` to generate resource names from resource ids. You can use `split()` to parse resource names into resource ids. Note that some trailing [Resource ID](https://cloud.google.com/apis/design/resource_names#resource_id) can have multiple URI segments separated by `/`, like file path.



# Standard methods

 bookmark_border

This chapter defines the concept of standard methods, which are `List`, `Get`, `Create`, `Update`, and `Delete`. Standard methods reduce complexity and increase consistency. Over 70% of API methods in the [Google APIs](https://github.com/googleapis/googleapis) repository are standard methods, which makes them much easier to learn and use.

The following table describes how to map standard methods to HTTP methods:

|Standard Method|HTTP Mapping|HTTP Request Body|HTTP Response Body|
|---|---|---|---|
|[`List`](https://cloud.google.com/apis/design/standard_methods#list)|`GET <collection URL>`|N/A|Resource* list|
|[`Get`](https://cloud.google.com/apis/design/standard_methods#get)|`GET <resource URL>`|N/A|Resource*|
|[`Create`](https://cloud.google.com/apis/design/standard_methods#create)|`POST <collection URL>`|Resource|Resource*|
|[`Update`](https://cloud.google.com/apis/design/standard_methods#update)|`PUT or PATCH <resource URL>`|Resource|Resource*|
|[`Delete`](https://cloud.google.com/apis/design/standard_methods#delete)|`DELETE <resource URL>`|N/A|`google.protobuf.Empty`**|

*The resource returned from `List`, `Get`, `Create`, and `Update` methods **may** contain partial data if the methods support response field masks, which specify a subset of fields to be returned. In some cases, the API platform natively supports field masks for all methods.

**The response returned from a `Delete` method that doesn't immediately remove the resource (such as updating a flag or creating a long-running delete operation) **should** contain either the long-running operation or the modified resource.

A standard method **may** also return a [long running operation](https://github.com/googleapis/googleapis/blob/master/google/longrunning/operations.proto) for requests that do not complete within the time-span of the single API call.

The following sections describe each of the standard methods in detail. The examples show the methods defined in .proto files with special annotations for the HTTP mappings. You can find many examples that use standard methods in the [Google APIs](https://github.com/googleapis/googleapis) repository.

**Note:** The `google.api.http` annotation shown in the examples below uses the [gRPC transcoding](https://cloud.google.com/endpoints/docs/transcoding) syntax to define URIs.

## List

The `List` method takes a collection name and zero or more parameters as input, and returns a list of resources that match the input.

`List` is commonly used to search for resources. `List` is suited to data from a single collection that is bounded in size and not cached. For broader cases, the [custom method](https://cloud.google.com/apis/design/custom_methods) `Search` **should** be used.

A batch get (such as a method that takes multiple resource IDs and returns an object for each of those IDs) **should** be implemented as a custom `BatchGet` method, rather than a `List`. However, if you have an already-existing `List` method that provides the same functionality, you **may** reuse the `List` method for this purpose instead. If you are using a custom `BatchGet` method, it **should** be mapped to `HTTP GET`.

Applicable common patterns: [pagination](https://cloud.google.com/apis/design/design_patterns#list_pagination), [result ordering](https://cloud.google.com/apis/design/design_patterns#sorting_order).

Applicable naming conventions: [filter field](https://cloud.google.com/apis/design/naming_convention#list_filter_field), [results field](https://cloud.google.com/apis/design/naming_convention#list_response)

HTTP mapping:

- The `List` method **must** use an HTTP `GET` verb.
- The request message field(s) receiving the name of the collection whose resources are being listed **should** map to the URL path. If the collection name maps to the URL path, the last segment of the URL template (the [collection ID](https://cloud.google.com/apis/design/resource_names#CollectionId)) **must** be literal.
- All remaining request message fields **shall** map to the URL query parameters.
- There is no request body; the API configuration **must not** declare a `body` clause.
- The response body **should** contain a list of resources along with optional metadata.

Example:

```
// Lists books in a shelf.rpc ListBooks(ListBooksRequest) returns (ListBooksResponse) {  // List method maps to HTTP GET.  option (google.api.http) = {    // The `parent` captures the parent resource name, such as "shelves/shelf1".    get: "/v1/{parent=shelves/*}/books"  };}message ListBooksRequest {  // The parent resource name, for example, "shelves/shelf1".  string parent = 1;  // The maximum number of items to return.  int32 page_size = 2;  // The next_page_token value returned from a previous List request, if any.  string page_token = 3;}message ListBooksResponse {  // The field name should match the noun "books" in the method name.  There  // will be a maximum number of items returned based on the page_size field  // in the request.  repeated Book books = 1;  // Token to retrieve the next page of results, or empty if there are no  // more results in the list.  string next_page_token = 2;}
```

## Get

The `Get` method takes a resource name, zero or more parameters, and returns the specified resource.

HTTP mapping:

- The `Get` method **must** use an HTTP `GET` verb.
- The request message field(s) receiving the resource name **should** map to the URL path.
- All remaining request message fields **shall** map to the URL query parameters.
- There is no request body; the API configuration **must not** declare a `body` clause.
- The returned resource **shall** map to the entire response body.

Example:

```
// Gets a book.rpc GetBook(GetBookRequest) returns (Book) {  // Get maps to HTTP GET. Resource name is mapped to the URL. No body.  option (google.api.http) = {    // Note the URL template variable which captures the multi-segment resource    // name of the requested book, such as "shelves/shelf1/books/book2"    get: "/v1/{name=shelves/*/books/*}"  };}message GetBookRequest {  // The field will contain name of the resource requested, for example:  // "shelves/shelf1/books/book2"  string name = 1;}
```

## Create

The `Create` method takes a parent resource name, a resource, and zero or more parameters. It creates a new resource under the specified parent, and returns the newly created resource.

If an API supports creating resources, it **should** have a `Create` method for each type of resource that can be created.

HTTP mapping:

- The `Create` method **must** use an HTTP `POST` verb.
- The request message **should** have a field `parent` that specifies the parent resource name where the resource is to be created.
- The request message field containing the resource **must** map to the HTTP request body. If the `google.api.http` annotation is used for the `Create` method, the `body: "<resource_field>"` form **must** be used.
- The request **may** contain a field named `<resource>_id` to allow callers to select a client assigned id. This field **may** be inside the resource.
- All remaining request message fields **shall** map to the URL query parameters.
- The returned resource **shall** map to the entire HTTP response body.

If the `Create` method supports client-assigned resource name and the resource already exists, the request **should** either fail with error code `ALREADY_EXISTS` or use a different server-assigned resource name and the documentation should be clear that the created resource name may be different from that passed in.

The `Create` method **must** take an input resource, so that when the resource schema changes, there is no need to update both request schema and resource schema. For resource fields that cannot be set by the clients, they **must** be documented as "Output only" fields.

Example:

```
// Creates a book in a shelf.rpc CreateBook(CreateBookRequest) returns (Book) {  // Create maps to HTTP POST. URL path as the collection name.  // HTTP request body contains the resource.  option (google.api.http) = {    // The `parent` captures the parent resource name, such as "shelves/1".    post: "/v1/{parent=shelves/*}/books"    body: "book"  };}message CreateBookRequest {  // The parent resource name where the book is to be created.  string parent = 1;  // The book id to use for this book.  string book_id = 3;  // The book resource to create.  // The field name should match the Noun in the method name.  Book book = 2;}rpc CreateShelf(CreateShelfRequest) returns (Shelf) {  option (google.api.http) = {    post: "/v1/shelves"    body: "shelf"  };}message CreateShelfRequest {  Shelf shelf = 1;}
```

## Update

The `Update` method takes a request message containing a resource and zero or more parameters. It updates the specified resource and its properties, and returns the updated resource.

Mutable resource properties **should** be mutable by the `Update` method, except the properties that contain the resource's [name or parent](https://cloud.google.com/apis/design/resource_names#Definitions). Any functionality to _rename_ or _move_ a resource **must not** happen in the `Update` method and instead **shall** be handled by a custom method.

HTTP mapping:

- The standard `Update` method **should** support partial resource update, and use HTTP verb `PATCH` with a `FieldMask` field named `update_mask`. [Output fields](https://cloud.google.com/apis/design/design_patterns#output_fields) that are provided by the client as inputs should be ignored.
- An `Update` method that requires more advanced patching semantics, such as appending to a repeated field, **should** be made available by a [custom method](https://cloud.google.com/apis/design/custom_methods).
- If the `Update` method only supports full resource update, it **must** use HTTP verb `PUT`. However, full update is highly discouraged because it has backwards compatibility issues when adding new resource fields.
- The message field receiving the resource name **must** map to the URL path. The field **may** be in the resource message itself.
- The request message field containing the resource **must** map to the request body.
- All remaining request message fields **must** map to the URL query parameters.
- The response message **must** be the updated resource itself.

If the API accepts client-assigned resource names, the server **may** allow the client to specify a non-existent resource name and create a new resource. Otherwise, the `Update` method **should** fail with non-existent resource name. The error code `NOT_FOUND` **should** be used if it is the only error condition.

An API with an `Update` method that supports resource creation **should** also provide a `Create` method. Rationale is that it is not clear how to create resources if the `Update` method is the only way to do it.

Example:

```
// Updates a book.rpc UpdateBook(UpdateBookRequest) returns (Book) {  // Update maps to HTTP PATCH. Resource name is mapped to a URL path.  // Resource is contained in the HTTP request body.  option (google.api.http) = {    // Note the URL template variable which captures the resource name of the    // book to update.    patch: "/v1/{book.name=shelves/*/books/*}"    body: "book"  };}message UpdateBookRequest {  // The book resource which replaces the resource on the server.  Book book = 1;  // The update mask applies to the resource. For the `FieldMask` definition,  // see https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#fieldmask  FieldMask update_mask = 2;}
```

## Delete

The `Delete` method takes a resource name and zero or more parameters, and deletes or schedules for deletion the specified resource. The `Delete` method **should** return `google.protobuf.Empty`.

An API **should not** rely on any information returned by a `Delete` method, as it **cannot** be invoked repeatedly.

HTTP mapping:

- The `Delete` method **must** use an HTTP `DELETE` verb.
- The request message field(s) receiving the resource name **should** map to the URL path.
- All remaining request message fields **shall** map to the URL _query_ parameters.
- There is no request body; the API configuration **must not** declare a `body` clause.
- If the `Delete` method immediately removes the resource, it **should** return an empty response.
- If the `Delete` method initiates a long-running operation, it **should** return the long-running operation.
- If the `Delete` method only marks the resource as being deleted, it **should** return the updated resource.

Calls to the `Delete` method should be [idempotent](http://tools.ietf.org/html/rfc2616#section-9.1.2) in effect, but do not need to yield the same response. Any number of `Delete` requests **should** result in a resource being (eventually) deleted, but only the first request should result in a success code. Subsequent requests should result in a `google.rpc.Code.NOT_FOUND`.

Example:

```
// Deletes a book.rpc DeleteBook(DeleteBookRequest) returns (google.protobuf.Empty) {  // Delete maps to HTTP DELETE. Resource name maps to the URL path.  // There is no request body.  option (google.api.http) = {    // Note the URL template variable capturing the multi-segment name of the    // book resource to be deleted, such as "shelves/shelf1/books/book2"    delete: "/v1/{name=shelves/*/books/*}"  };}message DeleteBookRequest {  // The resource name of the book to be deleted, for example:  // "shelves/shelf1/books/book2"  string name = 1;}
```


# Custom methods

This chapter will discuss how to use custom methods for API designs.

Custom methods refer to API methods besides the 5 standard methods. They **should** only be used for functionality that cannot be easily expressed via standard methods. In general, API designers **should** choose standard methods over custom methods whenever feasible. Standard Methods have simpler and well-defined semantics that most developers are familiar with, so they are easier to use and less error prone. Another advantage of standard methods is the API platform has better understanding and support for standard methods, such as billing, error handling, logging, monitoring.

A custom method can be associated with a resource, a collection, or a service. It **may** take an arbitrary request and return an arbitrary response, and also supports streaming request and response.

Custom method names **must** follow [method naming conventions](https://cloud.google.com/apis/design/naming_convention#method_names).

## HTTP mapping

For custom methods, they **should** use the following generic HTTP mapping:

```
https://service.name/v1/some/resource/name:customVerb
```

The reason to use `:` instead of `/` to separate the custom verb from the resource name is to support arbitrary paths. For example, undelete a file can map to `POST /files/a/long/file/name:undelete`

The following guidelines **shall** be applied when choosing the HTTP mapping:

- Custom methods **should** use HTTP `POST` verb since it has the most flexible semantics, except for methods serving as an alternative get or list which **may** use `GET` when possible. (See third bullet for specifics.)
- Custom methods **should not** use HTTP `PATCH`, but **may** use other HTTP verbs. In such cases, the methods **must** follow the standard [HTTP semantics](https://tools.ietf.org/html/rfc2616#section-9) for that verb.
- Notably, custom methods using HTTP `GET` **must** be idempotent and have no side effects. For example custom methods that implement special views on the resource **should** use HTTP `GET`.
- The request message field(s) receiving the resource name of the resource or collection with which the custom method is associated **should** map to the URL path.
- The URL path **must** end with a suffix consisting of a colon followed by the _custom verb_.
- If the HTTP verb used for the custom method allows an HTTP request body (this applies to `POST`, `PUT`, `PATCH`, or a custom HTTP verb), the HTTP configuration of that custom method **must** use the `body: "*"` clause and all remaining request message fields **shall** map to the HTTP request body.
- If the HTTP verb used for the custom method does not accept an HTTP request body (`GET`, `DELETE`), the HTTP configuration of such method **must not** use the `body` clause at all, and all remaining request message fields **shall** map to the URL query parameters.

**WARNING**: If a service implements multiple APIs, the API producer **must** carefully create the service configuration to avoid custom verb conflicts between APIs.

```
// This is a service level custom method.rpc Watch(WatchRequest) returns (WatchResponse) {  // Custom method maps to HTTP POST. All request parameters go into body.  option (google.api.http) = {    post: "/v1:watch"    body: "*"  };}// This is a collection level custom method.rpc ClearEvents(ClearEventsRequest) returns (ClearEventsResponse) {  option (google.api.http) = {    post: "/v3/events:clear"    body: "*"  };}// This is a resource level custom method.rpc CancelEvent(CancelEventRequest) returns (CancelEventResponse) {  option (google.api.http) = {    post: "/v3/{name=events/*}:cancel"    body: "*"  };}// This is a batch get custom method.rpc BatchGetEvents(BatchGetEventsRequest) returns (BatchGetEventsResponse) {  // The batch get method maps to HTTP GET verb.  option (google.api.http) = {    get: "/v3/events:batchGet"  };}
```

## Use Cases

Some additional scenarios where custom methods may be the right choice:

- **Reboot a virtual machine.** The design alternatives could be "create a reboot resource in collection of reboots" which feels disproportionately complex, or "virtual machine has a mutable state which the client can update from RUNNING to RESTARTING" which would open questions as to which other state transitions are possible. Moreover, reboot is a well-known concept that can translate well to a custom method which intuitively meets developer expectations.
- **Send mail.** Creating an email message should not necessarily send it (draft). Compared to the design alternative (move a message to an "Outbox" collection) custom method has the advantage of being more discoverable by the API user and models the concept more directly.
- **Promote an employee.** If implemented as a standard `update`, the client would have to replicate the corporate policies governing the promotion process to ensure the promotion happens to the correct level, within the same career ladder etc.
- **Batch methods.** For performance critical methods, it **may** be useful to provide custom batch methods to reduce per-request overhead. For example, [accounts.locations.batchGet](https://developers.google.com/my-business/reference/rest/v4/accounts.locations/batchGet).

A few examples where a standard method is a better fit than a custom method:

- Query resources with different query parameters (use standard `list` method with standard list filtering).
- Simple resource property change (use standard `update` method with field mask).
- Dismiss a notification (use standard `delete` method).

## Common Custom Methods

The curated list of commonly used or useful custom method names is below. API designers **should** consider these names before introducing their own to facilitate consistency across APIs.

| Method Name | Custom verb | HTTP verb | Note                                                                                                                                                                                                                                    |
| ----------- | ----------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Cancel`    | `:cancel`   | `POST`    | Cancel an outstanding operation, such as [`operations.cancel`](https://github.com/googleapis/googleapis/blob/master/google/longrunning/operations.proto#L100).                                                                          |
| `BatchGet`  | `:batchGet` | `GET`     | Batch get of multiple resources. See details in [the description of List](https://cloud.google.com/apis/design/standard_methods#list).                                                                                                  |
| `Move`      | `:move`     | `POST`    | Move a resource from one parent to another, such as [`folders.move`](https://cloud.google.com/resource-manager/reference/rest/v2/folders/move).                                                                                         |
| `Search`    | `:search`   | `GET`     | Alternative to List for fetching data that does not adhere to List semantics, such as [`services.search`](https://cloud.google.com/service-infrastructure/docs/service-consumer-management/reference/rest/v1/services/search).          |
| `Undelete`  | `:undelete` | `POST`    | Restore a resource that was previously deleted, such as [`services.undelete`](https://cloud.google.com/service-infrastructure/docs/service-management/reference/rest/v1/services/undelete). The recommended retention period is 30-day. |
|             |             |           |                                                                                                                                                                                                                                         |


# Standard fields

 bookmark_border

This section describes a set of standard message field definitions that should be used when similar concepts are needed. This will ensure the same concept has the same name and semantics across different APIs.

| Name               | Type                                                                                               | Description                                                                                                                                                                                                |
| ------------------ | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`             | `string`                                                                                           | The `name` field should contain the [relative resource name](https://cloud.google.com/apis/design/resource_names#relative_resource_name).                                                                  |
| `parent`           | `string`                                                                                           | For resource definitions and List/Create requests, the `parent` field should contain the parent [relative resource name](https://cloud.google.com/apis/design/resource_names#relative_resource_name).      |
| `create_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The creation timestamp of an entity.                                                                                                                                                                       |
| `update_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The last update timestamp of an entity. Note: update_time is updated when create/patch/delete operation is performed.                                                                                      |
| `delete_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The deletion timestamp of an entity, only if it supports retention.                                                                                                                                        |
| `expire_time`      | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The expiration timestamp of an entity if it happens to expire.                                                                                                                                             |
| `start_time`       | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The timestamp marking the beginning of some time period.                                                                                                                                                   |
| `end_time`         | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The timestamp marking the end of some time period or operation (regardless of its success).                                                                                                                |
| `read_time`        | [`Timestamp`](https://github.com/google/protobuf/blob/master/src/google/protobuf/timestamp.proto)  | The timestamp at which a particular an entity should be read (if used in a request) or was read (if used in a response).                                                                                   |
| `time_zone`        | `string`                                                                                           | The time zone name. It should be an [IANA TZ](http://www.iana.org/time-zones) name, such as "America/Los_Angeles". For more information, see https://en.wikipedia.org/wiki/List_of_tz_database_time_zones. |
| `region_code`      | `string`                                                                                           | The Unicode country/region code (CLDR) of a location, such as "US" and "419". For more information, see http://www.unicode.org/reports/tr35/#unicode_region_subtag.                                        |
| `language_code`    | `string`                                                                                           | The BCP-47 language code, such as "en-US" or "sr-Latn". For more information, see http://www.unicode.org/reports/tr35/#Unicode_locale_identifier.                                                          |
| `mime_type`        | `string`                                                                                           | An IANA published MIME type (also referred to as media type). For more information, see https://www.iana.org/assignments/media-types/media-types.xhtml.                                                    |
| `display_name`     | `string`                                                                                           | The display name of an entity.                                                                                                                                                                             |
| `title`            | `string`                                                                                           | The official name of an entity, such as company name. It should be treated as the formal version of `display_name`.                                                                                        |
| `description`      | `string`                                                                                           | One or more paragraphs of text description of an entity.                                                                                                                                                   |
| `filter`           | `string`                                                                                           | The standard filter parameter for List methods. See [AIP-160](https://google.aip.dev/160).                                                                                                                 |
| `query`            | `string`                                                                                           | The same as `filter` if being applied to a search method (ie [`:search`](https://cloud.google.com/apis/design/custom_methods#common_custom_methods))                                                       |
| `page_token`       | `string`                                                                                           | The pagination token in the List request.                                                                                                                                                                  |
| `page_size`        | `int32`                                                                                            | The pagination size in the List request.                                                                                                                                                                   |
| `total_size`       | `int32`                                                                                            | The total count of items in the list irrespective of pagination.                                                                                                                                           |
| `next_page_token`  | `string`                                                                                           | The next pagination token in the List response. It should be used as `page_token` for the following request. An empty value means no more result.                                                          |
| `order_by`         | `string`                                                                                           | Specifies the result ordering for List requests.                                                                                                                                                           |
| `progress_percent` | `int32`                                                                                            | Specifies the progress of an action in percentage (0-100). The value `-1` means the progress is unknown.                                                                                                   |
| `request_id`       | `string`                                                                                           | A unique string id used for detecting duplicated requests.                                                                                                                                                 |
| `resume_token`     | `string`                                                                                           | An opaque token used for resuming a streaming request.                                                                                                                                                     |
| `labels`           | `map<string, string>`                                                                              | Represents Cloud resource labels.                                                                                                                                                                          |
| `show_deleted`     | `bool`                                                                                             | If a resource allows undelete behavior, the corresponding List method must have a `show_deleted` field so client can discover the deleted resources.                                                       |
| `update_mask`      | [`FieldMask`](https://github.com/google/protobuf/blob/master/src/google/protobuf/field_mask.proto) | It is used for `Update` request message for performing partial update on a resource. This mask is relative to the resource, not to the request message.                                                    |
| `validate_only`    | `bool`                                                                                             | If true, it indicates that the given request should only be validated, not executed.                                                                                                                       |

### System Parameters

Besides the standard fields, Google APIs also support a set of common request parameters available across all API methods. These parameters are known as _system parameters_. For more information, see [System Parameters](https://cloud.google.com/apis/docs/system-parameters).


## Handling Errors

Below is a table containing all of the gRPC error codes defined in [`google.rpc.Code`](https://github.com/googleapis/googleapis/blob/master/google/rpc/code.proto) and a short description of their cause. To handle an error, you can check the description for the returned status code and modify your call accordingly.

|HTTP|gRPC|Description|
|---|---|---|
|200|`OK`|No error.|
|400|`INVALID_ARGUMENT`|Client specified an invalid argument. Check error message and error details for more information.|
|400|`FAILED_PRECONDITION`|Request can not be executed in the current system state, such as deleting a non-empty directory.|
|400|`OUT_OF_RANGE`|Client specified an invalid range.|
|401|`UNAUTHENTICATED`|Request not authenticated due to missing, invalid, or expired OAuth token.|
|403|`PERMISSION_DENIED`|Client does not have sufficient permission. This can happen because the OAuth token does not have the right scopes, the client doesn't have permission, or the API has not been enabled.|
|404|`NOT_FOUND`|A specified resource is not found.|
|409|`ABORTED`|Concurrency conflict, such as read-modify-write conflict.|
|409|`ALREADY_EXISTS`|The resource that a client tried to create already exists.|
|429|`RESOURCE_EXHAUSTED`|Either out of resource quota or reaching rate limiting. The client should look for google.rpc.QuotaFailure error detail for more information.|
|499|`CANCELLED`|Request cancelled by the client.|
|500|`DATA_LOSS`|Unrecoverable data loss or data corruption. The client should report the error to the user.|
|500|`UNKNOWN`|Unknown server error. Typically a server bug.|
|500|`INTERNAL`|Internal server error. Typically a server bug.|
|501|`NOT_IMPLEMENTED`|API method not implemented by the server.|
|502|N/A|Network error occurred before reaching the server. Typically a network outage or misconfiguration.|
|503|`UNAVAILABLE`|Service unavailable. Typically the server is down.|
|504|`DEADLINE_EXCEEDED`|Request deadline exceeded. This will happen only if the caller sets a deadline that is shorter than the method's default deadline (i.e. requested deadline is not enough for the server to process the request) and the request did not finish within the deadline.|


