# JavaScript SDK

The Javascript SDK provides a set of client-side calls for integrating a custom external application into the ABS Platform.


### Initializing the SDK

To initialize the API, include the Javascript SDK into your web application

http://hub.blueye.com/js/api.js

The SDK inserts a div element with the ID abs-root, containing an iframe with the ID abs-frame, into your web application’s source. The ABS object included in the SDK provides access to the various API requests describe in the section below.

### Authentication

Please contact your account manager to obtain an authorization key required to initialize the API.


```javascript
			ABS.init({
				apiKey: '1a1e31b4d4a3b5191ca22a6919ade490'
			}, function(response) {
				if(response.success) {
					alert(‘Successfully initialized the API’);
				}
				else {
					alert(response.message);
				}
			});
```

### Facebook Connect

Provides access to the ABS Platform’s implementation of various Facebook API requests.

```javascript
			ABS.api(‘initFacebook’,  { 
				appId: ‘YOUR_FACEBOOK_APP_ID’ 
				}, function(response) { 
				//handle response 
			});
```

### Register Facebook Open Graph Action

Register an Open Graph action to be used with your custom application.

```javascript
			ABS.api(‘registerAction’,  { 
				appId: ‘FACEBOOK_APP_ID’,
				fb_namespace:  ‘FACEBOOK_APP_NAMESPACE’,
				fb_action: ‘FACEBOOK_ACTION_NAME,
				fb_object: ‘FACEBOOK_ACTION_OBJECT’,
				label:  ‘ALIAS_FOR_ACTION’ /* i.e. hiked a trail */  
			}, function(response) { 
				//JSON response containing ABS action type ID
				//i.e. { success:1, id:45 }
			});
```

### Publish Facebook Open Graph Action

Publish an open graph action triggered from you custom application.

```javascript
			ABS.api(‘publishAction’,  { 
				fb_action_type_id: ‘FACEBOOK_ACTION_TYPE_ID’,
				object_id:  ‘UNIQUE_OBJECT_ID_IN_CUSTOM_APP’,
				object_name:  ‘UNIQUE_OBJECT_NAME_IN_CUSTOM_APP’,
				object_descr:  ‘OBJECT_DESCRIPTION,
				object_url:  ‘DIRECT_OBJECT_URL’
			}, function(response) {
				//JSON response containing ABS action ID
				//i.e. { success:1, id:1298 }
			});
```

### Get Custom App Analytics

Retrieve your application’s ABS and Facebook analytics.

```javascript
			ABS.api(‘getAnalytics’, function(response) {
				//JSON response containing header level data, array of object level data, 
				//and Facebook Insights data
			});
```


### Analytics Header Fields
<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>avg_time_spent</td>
<td>Average time spent in app</td>
<td>Decimal</td>
</tr>
<tr>
<td>num_actions</td>
<td>Total actions published from app</td>
<td>Integer</td>
</tr>
<tr>
<td>num_views</td>
<td>Total times app has been loaded</td>
<td>Integer</td>
</tr>
</table>
### Analytics Object Level Fields
<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>avg_time_spent</td>
<td>Average time spent in object</td>
<td>Decimal</td>
</tr>
<tr>
<td>num_views</td>
<td>Total views of objects</td>
<td>Integer</td>
</tr>
<tr>
<td>num_clicks</td>
<td>Total clicks of links / buttons within object</td>
<td>Integer</td>
</tr>
<tr>
<td>num_shares</td>
<td>Total shares / likes of object</td>
<td>Integer</td>
</tr>
<tr>
<td>actions</td>
<td>Contains all custom action stats for object</td>
<td>JSON Object</td>
</tr>
</table>

#### Facebook Insights
Please visit the following link for a list of all stats available through the Facebook Insights API:

https://developers.facebook.com/docs/reference/fql/insights/ 



