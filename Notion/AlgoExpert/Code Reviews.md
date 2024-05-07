---
Owner: Shudipto Trafder
tags:
  - Codebase
Last edited time: 2023-12-30T23:29
---
> [!important]  
> This template documents how to review code. Helpful for new and remote employees to get and stay aligned.  

Philosophy

Preparing Code for Review

Commit Messages

Github PR Descriptions

Performing Code Reviews

How to Review

Examples

# Philosophy

Why do you perform code reviews? What are your guiding principles for these reviews?

You may want to mention other pages here. Like Engineering Guidelines. To link to another page inline, type `@` followed by the name of the page: [🤖Engineering Guidelines](https://www.notion.so/Engineering-Guidelines-ca05d305097e475a87ea7b4a7d3e633c?pvs=21)

# Preparing Code for Review

Preparation sets your reviewers up for success.

### Commit Messages

Make sure your commit messages are descriptive.

### Github PR Descriptions

Your PR descriptions should be an extension of your commit messages. Write about both what the commit changes, and how you implemented the change.

# Performing Code Reviews

### How to Review

- Make two passes over the PR if it's substantial.
    - On the first pass, come to an understanding of the code change at a high level.
    - On the second pass, pay more attention to semantic details.

# Examples

```JavaScript
var commentCount = 0;
```

You might suggest that this be a `let` instead of `var`.