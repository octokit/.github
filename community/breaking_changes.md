What are breaking and non breaking changes in the context of the [Octokit](https://github.com/octokit) and [Terraform](https://github.com/integrations/terraform-provider-github) SDKs?

While the answer to that question might not always be clear we tend to follow what GitHub considers as breaking changes, 
while also taking some inspiration from our friends at [Square](https://developer.squareup.com/docs/build-basics/versioning-overview)
and [Stripe](https://stripe.com/docs/upgrades#what-changes-does-stripe-consider-to-be-backwards-compatible).

We use the [Semver](https://semver.org/) specification for all of or SDKs. 
This means that when breaking changes are introduced we will "bump" the `MAJOR` version number on the SDK.

To help us detect these types of things we have a label (`Type: Breaking change`).
![Screenshot 2022-11-10 at 11 23 26 AM](https://user-images.githubusercontent.com/139819/201164127-861f658b-6039-48f8-b4fb-3054f710cc1a.png)

There could be a few reasons why you might want to add this label to your Pull Request or Issue.  Use the following list to help you better understand if you should add it or not.

- __Non-breaking changes__:
  - Adding new SDK APIs
  - Adding optional parameters to existing SDK APIs 
  - Adding new properties to existing SDK APIs models 
  - Changing the order of properties in existing SDK APIs models 
  - Changing the length or format of opaque strings (eg IDs, error messages, other human-readable strings)
  - Adding new string constants to enums
  - Adding new webhook event types/models
  - Deprecating a SDK APIs, response field, or parameter (not removing)
- __Breaking changes__: 
  - Adding new required parameters to existing SDK APIs
  - Removing an existing SDK API
  - Removing a field from a response model
  - Renaming a field in a response model
  - Changing the type of a response model field or parameter 
  - Adding a validation rule to an existing parameter 
  - Changing the HTTP status code returned by an SDK API method

Note:  Whenever breaking changes are introduced in the [OpenAPI descriptions for the GitHub REST API](https://github.com/github/rest-api-description), 
there will almost always be a corresponding breaking change in our SDKs
