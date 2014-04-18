# Blueye Hub HTTP API

The HTTP API provides a set of server-side calls for integrating a custom external application into the Hub Platform.


### Connecting Your Application

The endpoint for all HTTP calls is https://blueyehub.com/sdk
To initialize a connection to The Hub, make the following HTTP post call with your unique api key:

```javascript

https://blueyehub/sdk/connect?api_key=YOUR_API_KEY

Response: { "success":1, "token":"YOUR_TOKEN" }

```

Please contact your account manager to obtain YOUR_API_KEY required to initialize the SDK. 
If the response is successful, a unique token will be returned and used in all subsequent HTTP requests. Note that this token may change over time so it is required to connect to the SDK to first obtain a new token, at the beginning of each session.

## Facebook Ads API

The Hub HTTP API provides a window into the Facebook Ads API to allow you to programtically automate tasks you would otherwise perform directly in The Hub platform.

### Custom Audiences

Through the Hub HTTP API, you can manage your Facebook custom audiences, fow which the Hub exposes four endpoints to do so.

#### Retrieve all of your custom audiences
```javascript
Endpoint: https://blueyehub/sdk/customaudiences?token=YOUR_TOKEN
```
Required Post Parameters:
<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>token</td>
<td>Your current session token obtained from making an sdk/connect call</td>
<td>String</td>
</tr>
</table>

#### Create a new custom audience
```javascript
Endpoint: https://blueyehub/sdk/customaudiences/create
```
Required Post Parameters:
<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>token</td>
<td>Your current session token obtained from making an sdk/connect call</td>
<td>String</td>
</tr>
<tr>
<td>name</td>
<td>the name of your custom audience</td>
<td>String</td>
</tr>
</table>

#### Add users to a custom audience
```javascript
Endpoint: https://blueyehub/sdk/customaudiences/addusers
```
Required Post Parameters:
<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>token</td>
<td>Your current session token obtained from making an sdk/connect call</td>
<td>String</td>
</tr>
<tr>
<td>audience ID</td>
<td>FB's unqiue ID for this audience</td>
<td>String</td>
</tr>
<tr>
<td>users</td>
<td>array of hashed values per FB documentation https://developers.facebook.com/docs/reference/ads-api/custom-audience-targeting</td>
<td>json array</td>
</tr>
</table>

Example:
```javascript
https://blueyehub/sdk/customaudiences/addusers?token=c95633d8597a4a14a9078a83b7e7c17e&audience_id=6014146538248&users=[{ "email_hash":"SHA256_email_hash_1" }, { "email_hash":"SHA256_email_hash_2" }]
```

#### Remove users from a custom audience
```javascript
Endpoint: https://blueyehub/sdk/customaudiences/removeusers
```
Required Post Parameters:
<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>token</td>
<td>Your current session token obtained from making an sdk/connect call</td>
<td>String</td>
</tr>
<tr>
<td>audience ID</td>
<td>FB's unqiue ID for this audience</td>
<td>String</td>
</tr>
<tr>
<td>users</td>
<td>array of hashed values per FB documentation https://developers.facebook.com/docs/reference/ads-api/custom-audience-targeting</td>
<td>json array</td>
</tr>
</table>

Example:
```javascript
https://blueyehub/sdk/customaudiences/removeusers?token=c95633d8597a4a14a9078a83b7e7c17e&audience_id=6014146538248&users=[{ "email_hash":"SHA256_email_hash_1" }, { "email_hash":"SHA256_email_hash_2" }]
```
