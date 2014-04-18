# Blueye Hub HTTP API

The HTTP API provides a set of server-side calls for integrating a custom external application into the Hub Platform.


### Connecting Your Application

The endpoint for all HTTP calls is https://blueyehub.com/sdk
To initialize a connection to The Hub, make the following HTTP post call with your unique api key:

```javascript

http://blueyehub/sdk/connect?api_key=YOUR_API_KEY

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
Endpoint: http://blueyehub/sdk/customaudiences?token=YOUR_TOKEN
```

#### Create a new custom audience
```javascript
Endpoint: http://blueyehub/sdk/customaudiences
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
