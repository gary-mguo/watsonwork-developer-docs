---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-action-context'
is: 'experimental'
---


# Get action context information 

If you have registered a Client action handler callback for your App, then when your App is called through this callback, 
it will receive an action handler context token. Your App needs to use this token with this API to extract the proper 
action context.

### Path
```
GET /v1/apps/{appId}/getActionContext/{actionHandlerContextToken}
```
**actionHandlerContextToken** has only 5 minutes lifetime, and can only be used once. It will be deleted once it is used. 

#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|Authorization required|Authorization header, in form of Bearer {access_token}. The access_token is issued as result of an oauth flow by Watson Work Services|String|
|**Path**|appId required|Unique id of an app|String|
|**Path**|actionHandlerContextToken required|token generated by caller before|String|

#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|The configuration data is returned and deleted successfully.|ConfigurationData(see below)|
|**401**|Unauthorized.||
|**403**|Forbidden.||
|**404**|Not Found. The app with the given `appId` or the configuration data for the given `configurationToken` 
could not be found.||
|**500**|Internal server error.||

#### Produces

* `application/json`

#### Action Output Entity

The result from this call provides the following payload.

|Name|Description|Schema|
|---|---|---|
|**type**  <br>*required*|The action type for users to be aware of the configuration context. It should be either space-app-config-requested or team-app-config-requested.|string|
|**appId**  <br>*optional*|Id of the app for which the configuration data has been generated.|string|
|**userId**  <br>*required*|Id of the user by which the configuration data has been generated.|string|
|**actioncontext**  <br>*required*|The action context structure according to the action type.|[ActionContext](#actioncontext)|


<a name="actioncontext"></a>

#### Action Context

Here are the set of currently supported actions. There will be more supported action types in future.

#### Space Configuration Action Context

The `space-app-config-requested` action type occurs when users invoke the action to configure an app for a space. 

The **actionContext** format for `space-app-config-requested` action type

|Name|Description|Schema|
|---|---|---|
|**spaceId** <br>*required*|Id of the space where the user invoked the app configuration |string|
|**teamId** <br>*required*|Id of team where the space belongs|string|

#### Team Configuration Action Context


The `team-app-config-requested` action type occurs when users invoke the action to configure an app for a team. 

The **actionContext** format for `team-app-config-requested` action type

|Name|Description|Schema|
|---|---|---|
|**teamId** <br>*required*|Id of the team where the user invoked the app configuratoin |string|



