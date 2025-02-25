In the event that we need to backport changesets across our various [SDKs](https://github.com/octokit) we take a fairly ridged approach to where those changes get backported to.

In general, **we will backport to the last major version release**.  There are exceptions:
1. If the change is causing issues in a specific release and no others then the backport will target that release and any future ones (where appropriate)
2. If the change is related to a Security Advisory that is causing data corruption.
3. If the change is related to a Security Advisory where any personally identifiable information is involved.
4. If the change is related to a Security Advisory that is causing system wide issues / network related issues.
5. If the change is related to an issue in a language framework or Security Advisory within that language's ecosystem.
6. If the change is in our JavaScript SDKs. In this case the patch will be applied to the latest non ESM version (see the table below).


#### Backporting process (Octokit.js)

Note: The following uses information from a historical backport as an example.

- Start with the patched library (ex. [request-error.js](https://github.com/octokit/request-error.js)), get the last [non ESM version](https://github.com/octokit/.github/pull/95)
- Semantic release handles maintenance release
- Create a major.x version (i.e. 5.x if one does not exist, [5.x](https://github.com/octokit/request-error.js/tree/5.x) does exist for request-error.js, so we'll use that) - using fix and feat conventions
```
> git checkout 5.x
> git checkout -b 5.x-fix-regex 5.x
```
* Find the commit of the changeset (i.e. from the [patch release](https://github.com/octokit/request-error.js/commit/d558320874a4bc8d356babf1079e6f0056a59b9e))
- Try to cherry pick. ex.
```
> git cherry-pick d558320874a4bc8d356babf1079e6f0056a59b9e
```
- Use same message as the fix / feat. ex.
* "fix: ReDos  regex vulnerability, reported by @user"
```
> git commit --amend -m 'fix: ReDos  regex vulnerability, reported by @user'
```
- Create a PR against 5.x
```
gh pr create -B 5.x -t 'fix: ReDos  regex vulnerability, reported by @user' -b 'backport of https://github.com/octokit/request-error.js/releases/tag/v6.1.7'
```
- Once CI runs green then merge and let semantic release take over.
- Update the table below with the new version from the backport.

Rule: If the library does not have a leaf (but is a leaf itself) then the lib needs to be back ported

| JS SDK/Library                                                  	| Last Non-ESM Version                                                                    	|
|-----------------------------------------------------------------	|-------------------------------------------------------------------------------------	|
| [openapi-types.ts](https://github.com/octokit/openapi-types.ts)                     	| [v12.8.0](https://github.com/octokit/openapi-types.ts/releases/tag/v12.8.0) |
| [graphql-schema](https://github.com/octokit/graphql-schema)                       	| [v14.58.0](https://github.com/octokit/graphql-schema/releases/tag/v14.58.0) |
| [fixtures](https://github.com/octokit/fixtures)                             	| [v21.5.0](https://github.com/octokit/fixtures/releases/tag/v21.5.0) 	|
| [openapi](https://github.com/octokit/openapi)                              	| [v12.0.0](https://github.com/octokit/openapi/releases/tag/v12.0.0) 	|
| [app-permissions](https://github.com/octokit/app-permissions)                      	| [v1.10.1](https://github.com/octokit/app-permissions/releases/tag/v1.10.1) 	|
| [create-octokit-project.js](https://github.com/octokit/create-octokit-project.js)            	| [v3.0.1](https://github.com/octokit/create-octokit-project.js/releases/tag/v3.0.1) 	|
| [fixtures-server](https://github.com/octokit/fixtures-server)                      	| [v6.0.25](https://github.com/octokit/fixtures-server/releases/tag/v6.0.25) 	|
| [octokit-next.js](https://github.com/octokit/octokit-next.js)                      	| N/A                                                                                 	|
| [graphql-action](https://github.com/octokit/graphql-action)                       	| N/A                                                                                 	|
| [tsconfig](https://github.com/octokit/tsconfig)                             	| N/A                                                                                 	|
| [request-action](https://github.com/octokit/request-action)                       	| N/A                                                                                 	|
| [sandbox](https://github.com/octokit/sandbox)                              	| N/A                                                                                 	|
| [webhooks-methods.js](https://github.com/octokit/webhooks-methods.js)                  	| [v4.1.0](https://github.com/octokit/webhooks-methods.js/releases/tag/v4.1.0)                  	|
| [action.js](https://github.com/octokit/action.js)                            	| [v6.1.0](https://github.com/octokit/action.js/releases/tag/v6.1.0)                            	|
| [auth-oauth-device.js](https://github.com/octokit/auth-oauth-device.js)                 	| [v6.0.1](https://github.com/octokit/auth-oauth-device.js/releases/tag/v6.0.1)                 	|
| [request.js](https://github.com/octokit/request.js)                           	| [v8.4.0](https://github.com/octokit/request.js/releases/tag/v8.4.0)                           	|
| [auth-oauth-app.js](https://github.com/octokit/auth-oauth-app.js)                    	| [v7.0.1](https://github.com/octokit/auth-oauth-app.js/releases/tag/v7.0.1)                    	|
| [plugin-paginate-graphql.js](https://github.com/octokit/plugin-paginate-graphql.js)           	| [v4.0.1](https://github.com/octokit/plugin-paginate-graphql.js/releases/tag/v4.0.1)           	|
| [plugin-paginate-rest.js](https://github.com/octokit/plugin-paginate-rest.js)              	| [v9.2.0](https://github.com/octokit/plugin-paginate-rest.js/releases/tag/v9.2.0)              	|
| [oauth-methods.js](https://github.com/octokit/oauth-methods.js)                     	| [v4.0.1](https://github.com/octokit/oauth-methods.js/releases/tag/v4.0.1)                     	|
| [request-error.js](https://github.com/octokit/request-error.js)                     	| [v5.1.1](https://github.com/octokit/request-error.js/releases/tag/v5.1.1)                     	|
| [core.js](https://github.com/octokit/core.js)                              	| [v5.1.0](https://github.com/octokit/core.js/releases/tag/v5.1.0)                              	|
| [endpoint.js](https://github.com/octokit/endpoint.js)                          	| [v9.0.6](https://github.com/octokit/endpoint.js/releases/tag/v9.0.6)                          	|
| [webhooks.js](https://github.com/octokit/webhooks.js)                          	| [v12.2.0](https://github.com/octokit/webhooks.js/releases/tag/v12.2.0)                         	|
| [plugin-throttling.js](https://github.com/octokit/plugin-throttling.js)                 	| [v8.2.0](https://github.com/octokit/plugin-throttling.js/releases/tag/v8.2.0)                 	|
| [graphql.js](https://github.com/octokit/graphql.js)                           	| [v7.0.2](https://github.com/octokit/graphql.js/releases/tag/v7.0.2)                           	|
| [plugin-rest-endpoint-methods.js](https://github.com/octokit/plugin-rest-endpoint-methods.js)      	| [v10.4.0](https://github.com/octokit/plugin-rest-endpoint-methods.js/releases/tag/v10.4.0)     	|
| [octokit.js](https://github.com/octokit/octokit.js)                           	| [v3.2.1](https://github.com/octokit/octokit.js/releases/tag/v3.2.1)                           	|
| [app.js](https://github.com/octokit/app.js)                               	| [v14.1.0](https://github.com/octokit/app.js/releases/tag/v14.1.0)                              	|
| [auth-oauth-user.js](https://github.com/octokit/auth-oauth-user.js)                   	| [v4.0.1](https://github.com/octokit/auth-oauth-user.js/releases/tag/v4.0.1)                   	|
| [auth-action.js](https://github.com/octokit/auth-action.js)                       	| [v4.1.0](https://github.com/octokit/auth-action.js/releases/tag/v4.1.0)                       	|
| [auth-unauthenticated.js](https://github.com/octokit/auth-unauthenticated.js)              	| [v5.0.1](https://github.com/octokit/auth-unauthenticated.js/releases/tag/v5.0.1)              	|
| [plugin-enterprise-cloud.js](https://github.com/octokit/plugin-enterprise-cloud.js)           	| [v12.6.0](https://github.com/octokit/plugin-enterprise-cloud.js/releases/tag/v12.6.0)          	|
| [auth-token.js](https://github.com/octokit/auth-token.js)                        	| [v4.0.0](https://github.com/octokit/auth-token.js/releases/tag/v4.0.0)                        	|
| [auth-app.js](https://github.com/octokit/auth-app.js)                          	| [v6.1.1](https://github.com/octokit/auth-app.js/releases/tag/v6.1.1)                          	|
| [oauth-app.js](https://github.com/octokit/oauth-app.js)                         	| [v6.1.0](https://github.com/octokit/oauth-app.js/releases/tag/v6.1.0)                         	|
| [rest.js](https://github.com/octokit/rest.js)                              	| [v20.1.0](https://github.com/octokit/rest.js/releases/tag/v20.1.0)                             	|
| [plugin-retry.js](https://github.com/octokit/plugin-retry.js)                      	| [v6.1.0](https://github.com/octokit/plugin-retry.js/releases/tag/v6.1.0)                      	|
| [plugin-enterprise-server.js](https://github.com/octokit/plugin-enterprise-server.js)          	| [v18.0.0](https://github.com/octokit/plugin-enterprise-server.js/releases/tag/v18.0.0)         	|
| [oauth-authorization-url.js](https://github.com/octokit/oauth-authorization-url.js)           	| [v6.0.2](https://github.com/octokit/oauth-authorization-url.js/releases/tag/v6.0.2)           	|
| [plugin-request-log.js](https://github.com/octokit/plugin-request-log.js)                	| [v4.0.1](https://github.com/octokit/plugin-request-log.js/releases/tag/v4.0.1)                	|
| [plugin-enterprise-compatibility.js](https://github.com/octokit/plugin-enterprise-compatibility.js)   	| [v4.1.0](https://github.com/octokit/plugin-enterprise-compatibility.js/releases/tag/v4.1.0)   	|
| [openapi-webhooks](https://github.com/octokit/openapi-webhooks)                     	| [v1.0.0](https://github.com/octokit/openapi-webhooks/releases/tag/v1.0.0)                     	|
| [plugin-create-or-update-text-file.js](https://github.com/octokit/plugin-create-or-update-text-file.js) 	| [v4.0.2](https://github.com/octokit/plugin-create-or-update-text-file.js/releases/tag/v4.0.2) 	|
| [webhooks](https://github.com/octokit/webhooks)                             	| [v7.3.1](https://github.com/octokit/webhooks/releases/tag/v7.3.1)                             	|
| [types.ts](https://github.com/octokit/types.ts)                             	| [v11.1.0](https://github.com/octokit/types.ts/releases/tag/v11.1.0)                            	|
| [auth-callback.js](https://github.com/octokit/auth-callback.js)                    	| [v4.0.0](https://github.com/octokit/auth-callback.js/releases/tag/v4.0.0)                     	|


