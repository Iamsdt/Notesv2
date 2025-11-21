## 🎯 Architecture Pattern: Clean Architecture with Riverpod

---

## 📚 Library Roles & Responsibilities

### **1. State Management & Dependency Injection**

|Library|Primary Role|Responsibilities|Architecture Layer|Key Use Cases|
|---|---|---|---|---|
|**flutter_riverpod**|State Management & DI Container|• Global state management<br>• Dependency injection<br>• Provider lifecycle management<br>• Reactive state updates|All Layers|• Provide repositories<br>• Provide services<br>• Manage app state<br>• Replace get_it/injectable|
|**hooks_riverpod**|Riverpod + Hooks Integration|• Combine hooks with providers<br>• Simplified provider consumption<br>• Widget-level provider access|Presentation|• Build UI with providers<br>• Access state in widgets<br>• React to state changes|
|**riverpod_annotation**|Code Generation for Providers|• Generate provider boilerplate<br>• Type-safe providers<br>• Reduce manual code<br>• Auto-dispose management|All Layers|• Create providers easily<br>• Generate notifiers<br>• Dependency injection setup|
|**flutter_hooks**|Local Widget State|• Manage widget lifecycle<br>• Handle text controllers<br>• Animation controllers<br>• Focus nodes management|Presentation|• Form handling<br>• Local animations<br>• Ephemeral UI state<br>• Replace StatefulWidget|

---

### **2. Data Layer - Remote Data Source**

|Library|Primary Role|Responsibilities|Architecture Layer|Key Use Cases|
|---|---|---|---|---|
|**dio**|HTTP Client|• API communication<br>• Request/Response handling<br>• Interceptor management<br>• Error handling<br>• Timeout configuration|Data Layer|• REST API calls<br>• File uploads/downloads<br>• Authentication headers<br>• Base URL configuration|
|**pretty_dio_logger**|Development Logging|• Request logging<br>• Response debugging<br>• Error visibility<br>• Network monitoring|Data Layer|• Debug API calls<br>• Track network issues<br>• Development only<br>• Performance monitoring|
|**jwt_decoder**|Token Management|• Parse JWT tokens<br>• Extract claims<br>• Validate expiration<br>• User info extraction|Data Layer|• Check token validity<br>• Get user roles<br>• Refresh token logic<br>• Auth state determination|

---

### **3. Data Layer - Network Monitoring**

|Library|Primary Role|Responsibilities|Architecture Layer|Key Use Cases|
|---|---|---|---|---|
|**connectivity_plus**|Connection Type Detection|• Detect WiFi/Mobile/None<br>• Connection type monitoring<br>• Real-time status stream<br>• Platform-specific info|Data Layer|• Show connection type<br>• Switch behavior by network<br>• Warn on mobile data<br>• Monitor connection changes|
|**internet_connection_checker**|Actual Internet Validation|• Ping real servers<br>• Verify actual connectivity<br>• Check internet reachability<br>• Periodic status checks|Data Layer|• Validate real internet access<br>• Detect captive portals<br>• Confirm data transfer ability<br>• More reliable than connectivity_plus alone|

**Note:** Use both together for robust network detection:

- `connectivity_plus` = Fast, tells you if device has network interface connected
- `internet_connection_checker` = Accurate, tells you if internet actually works (solves false positives when connected to WiFi without internet)

---

### **4. Data Layer - Local Data Source**

| Library                    | Primary Role             | Responsibilities                                                                                      | Architecture Layer | Key Use Cases                                                                       |
| -------------------------- | ------------------------ | ----------------------------------------------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------- |
| **shared_preferences**     | Simple Key-Value Storage | • Store preferences<br>• Cache simple data<br>• Non-sensitive storage<br>• Fast synchronous access    | Data Layer         | • Theme settings<br>• Language preference<br>• Onboarding status<br>• User settings |
| **flutter_secure_storage** | Encrypted Storage        | • Secure sensitive data<br>• Platform encryption<br>• Token storage<br>• Credential management        | Data Layer         | • Auth tokens<br>• API keys<br>• Passwords<br>• Sensitive user data                 |
| **path_provider**          | File System Access       | • Get app directories<br>• Access cache folder<br>• Documents directory<br>• Temporary files location | Data Layer         | • File downloads<br>• Image caching<br>• Local database path<br>• User documents    |

---

### **5. Domain Layer - Models & Entities**

| Library                | Primary Role           | Responsibilities                                                                                                                | Architecture Layer | Key Use Cases                                                                  |
| ---------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------ |
| **freezed**            | Immutable Data Classes | • Create immutable entities<br>• Generate copyWith<br>• Union types/sealed classes<br>• Pattern matching<br>• Equality/hashCode | Domain Layer       | • Business entities<br>• Value objects<br>• State classes<br>• API models      |
| **freezed_annotation** | Freezed Annotations    | • Mark classes for generation<br>• Configure freezed behavior<br>• Custom serialization hints                                   | Domain Layer       | • Annotate models<br>• Configure generation<br>• Custom converters             |
| **json_annotation**    | JSON Serialization     | • JSON to Dart mapping<br>• Serialization metadata<br>• Type conversion<br>• Custom converters                                  | Data & Domain      | • API response models<br>• DTO creation<br>• Type-safe JSON<br>• Field mapping |

---

### **6. Presentation Layer - Navigation**

| Library       | Primary Role        | Responsibilities                                                                                                               | Architecture Layer | Key Use Cases                                                                             |
| ------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------ | ----------------------------------------------------------------------------------------- |
| **go_router** | Declarative Routing | • Type-safe navigation<br>• Deep linking<br>• Route guards<br>• Nested navigation<br>• Redirection logic<br>• Query parameters | Presentation       | • App navigation<br>• Auth guards<br>• Bottom nav with nested routes<br>• Web URL routing |

---

### **7. Presentation Layer - Localization**

|Library|Primary Role|Responsibilities|Architecture Layer|Key Use Cases|
|---|---|---|---|---|
|**flutter_localizations**|Flutter i18n Support|• Provide Flutter widgets localization<br>• Material/Cupertino translations<br>• Built-in locale support|Presentation|• System widget translations<br>• Date/number formatting<br>• RTL support|
|**easy_localization**|App Localization|• Custom translations<br>• Language switching<br>• Plural/gender support<br>• Asset-based translations<br>• Fallback locale|Presentation|• Multi-language app<br>• Translation management<br>• Runtime locale change<br>• JSON/CSV translations|

---

### **8. Configuration & Environment**

|Library|Primary Role|Responsibilities|Architecture Layer|Key Use Cases|
|---|---|---|---|---|
|**flutter_dotenv**|Environment Variables|• Load .env files<br>• Separate dev/prod config<br>• API keys management<br>• Environment-specific values|Core/Config|• API base URLs<br>• API keys<br>• Feature flags<br>• Environment separation|

---

### **9. Debugging & Logging**

|Library|Primary Role|Responsibilities|Architecture Layer|Key Use Cases|
|---|---|---|---|---|
|**loggy**|Structured Logging|• Log levels (debug, info, error)<br>• Contextual logging<br>• Custom log formatting<br>• Log filtering|All Layers|• Error tracking<br>• Debug information<br>• User action logging<br>• Performance monitoring|

---

## 🏗️ Architecture Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                        │
│  go_router, flutter_hooks, hooks_riverpod, easy_localization│
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ↓
┌─────────────────────────────────────────────────────────────┐
│                     DOMAIN LAYER                             │
│         freezed, freezed_annotation, riverpod               │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ↓
┌─────────────────────────────────────────────────────────────┐
│                      DATA LAYER                              │
│  dio, jwt_decoder, connectivity_plus, internet_connection_   │
│  checker, shared_preferences, flutter_secure_storage,        │
│  json_annotation, path_provider                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 🔄 Data Flow Pattern

|Flow Direction|Libraries Involved|Purpose|
|---|---|---|
|**User Action → State**|hooks_riverpod → riverpod_annotation|User triggers action in UI, updates provider state|
|**Check Network Status**|connectivity_plus + internet_connection_checker|Verify both connection type AND actual internet access|
|**State → Remote API**|dio + jwt_decoder|Provider calls repository, makes API request|
|**Remote Response → Entity**|json_annotation + freezed|Convert JSON to domain entity|
|**Entity → Local Storage**|shared_preferences / flutter_secure_storage|Cache response or save data locally|
|**Local Storage → State**|riverpod + freezed|Load cached data into provider state|
|**State → UI**|hooks_riverpod + flutter_hooks|Provider notifies widgets, UI rebuilds|
|**Navigation**|go_router + riverpod|State changes trigger navigation|
|**Localization**|easy_localization|Display translated text based on locale|
|**Logging**|loggy + pretty_dio_logger|Track errors, API calls, user actions throughout flow|

---

## 🌐 Network Monitoring Strategy

| Scenario                                     | connectivity_plus | internet_connection_checker | Recommended Action                |
| -------------------------------------------- | ----------------- | --------------------------- | --------------------------------- |
| WiFi connected, Internet working             | ✅ Connected       | ✅ Internet Available        | Proceed with API calls            |
| WiFi connected, No internet (captive portal) | ✅ Connected       | ❌ No Internet               | Show "No Internet" message        |
| Mobile data, Internet working                | ✅ Connected       | ✅ Internet Available        | Proceed (warn if large downloads) |
| Airplane mode                                | ❌ None            | ❌ No Internet               | Show offline mode                 |
| Switching networks                           | Stream updates    | Periodic checks             | Queue requests, retry when stable |

**Best Practice:**

- Use `connectivity_plus` stream for instant UI feedback
- Use `internet_connection_checker` before critical API calls to confirm actual connectivity
- Combine both in a network service provided via riverpod

---
