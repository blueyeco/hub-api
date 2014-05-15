# Web SDK for Javascript

The Javascript SDK provides a set of client-side calls for integrating a custom external application into the Hub Platform.


### One line SDK Initialization

To initialize the SDK asynchronously, include the following line of code just before the page closing &lt;/head&gt; tag:

```javascript

<script type="text/javascript">window.hubAsyncInit=function(){HUB.init({apiKey:"YOUR_API_KEY"})};(function(e,t,n){if(!window.HUB){window.HUB={track:function(a,b,c){window.HUB.q.push([a,b,c])},q:[]};window.HUB.setUser=window.HUB.track;}var r,i=e.getElementsByTagName(t)[0];if(e.getElementById(n)){return}r=e.createElement(t);r.id=n;r.src="//blueyehub.com/js/api.js";i.parentNode.insertBefore(r,i)})(document,"script","blueyehub-sdk")</script>

```	

Please contact your account manager to obtain YOUR_API_KEY required to initialize the SDK.

The SDK inserts a div element with the ID hub-root, containing an iframe with the ID hub-frame, into your web application’s source. The HUB object included in the SDK provides access to the various API requests described in the following sections below.

### Manual Initialization

If you prefer to directly initialize the SDK, you can do so by including the file https://blueyehub.com/js/api.js in your web page and making a call to the HUB.init method as shown below.

When initializing the SDK manually, optional user identifying information in the form of a user id, email address, or name can be passed in. This allows the Hub to tie any actions tracked in your app to a unique user to facilitate advanced audience segmentation in the Hub developer console.


```javascript
			HUB.init({
				apiKey: '1a1e31b4d4a3b5191ca22a6919ade490'
				uid:345, /* optional */
				email:'johndoe@gmail.com', /* optional */
				name:'John Doe' /* optional */
			}, function(response) {
				if(response.success) {
					alert(‘Successfully initialized the SDK’);
				}
				else {
					alert(response.message);
				}
			});
```

Passing in user information in the init call allows you to skip the next step of "Creating a User Profile".

### Creating a User Profile

If you used the one line asynchorous method to initialize the SDK, remember to create a user profile so that all actions can be tied to unique individuals for advanced targeting and segmentation. This method is also useful if you called Hub.init manually but neglected to pass in user information.

```javascript
			HUB.setUser({ uid:345, name:"John Doe", email:"johndoe@gmail.com" }, function(res) {
				console.log(res);
			});
```

### App Action Tracking

Easily track any app activity by simply calling the HUB.track method. An optional JSON object of any custom properties associated with the action can be passed as the second parameter to the track method. It is highly advised that a user profile be created prior to using this method so that these actions are auto-tied to individual users.

```javascript
			HUB.track('sign up click', { mycustomprop:'test', mycustomprop2:'blue' });
```

### Facebook Connect 

The Web SDK simplifies the process of connecting your app to Facebook, by providing pass-through functions that abstract some of the complexities of connecting to and retrieving data from Facebook. To enable Hub Facebook Connect for you app, enter your Facebook app ID in your application settings on the Hub Developer Console. 

<img src="https://blueyehub.com/img/docs/hub_app_settings.png" />

In addition, please modify your Facebook app settings (http://developers.facebook.com) to use blueyehub.com as the 'App Domain' and http://hub.blueye.com/api/custom as the Website with Facebook 'Login Site URL'.

<img src="https://blueyehub.com/img/docs/fb_app_settings.png" />

Once the steps above are complete, you can use the API calls below to obtain information about the current Facebook user.

#### Basic Facebook User Info

```javascript
			HUB.api(‘getFacebookUser’, {}, function(response) { 
				//response JSON object containing a Facebook user object
				//i.e. { success:1, user:{ id:"3107076", first_name:"John", last_name:"Doe", ... }
				//Please visit https://developers.facebook.com/docs/graph-api/reference/user/ for fill list of fields
			});
```

#### User's Facebook Friends

```javascript
			HUB.api(‘getFacebookFriends’, {}, function(response) { 
				//response JSON object containing the current Facebook user object and an array of friends
				//i.e. { success:1, user:{}, friends:[] }
				//Please visit https://developers.facebook.com/docs/graph-api/reference/user/ for complete list of fields
			});
```


#### User's Facebook Photo Albums

```javascript
			HUB.api(‘getFacebookAlbums’, {}, function(response) { 
				//response JSON object containing an array of Facebook albums
				//i.e. { success:1, data:[] }
				//Please visit https://developers.facebook.com/docs/reference/api/album/ for complete list of fields
			});
```


#### User's Facebook Photos

```javascript
			HUB.api(‘getFacebookPhotos’, { album_id:facebookAlbumId }, function(response) { 
				//response JSON object containing an array of Facebook photos
				//i.e. { success:1, data:[] }
				//Please visit https://developers.facebook.com/docs/reference/api/album/ for complete list of fields
			});
```

### Register Facebook Open Graph Action

Register an Open Graph action to be used with your custom application. Please ensure that the action / object has also been created in your Facebook app settings (https://developers.facebook.com/docs/opengraph/). <b>Please note this call should only be made once for each action, and you will need to save the returned ID for making subsequent publishing calls.</b>

```javascript
			HUB.api(‘registerFacebookAction’,  { 
				fb_namespace:  ‘FACEBOOK_APP_NAMESPACE’,
				fb_action: ‘FACEBOOK_ACTION_NAME,
				fb_object: ‘FACEBOOK_ACTION_OBJECT’,
				label:  ‘ALIAS_FOR_ACTION’ /* i.e. hiked a trail */  
			}, function(response) { 
				//JSON response containing HUB action type ID
				//i.e. { success:1, id:45 }
			});
```

### Publish Facebook Open Graph Action

Publish an open graph action triggered from you custom application.

```javascript
			HUB.api(‘publishFacebookAction’,  { 
				fb_action_type_id: ‘FACEBOOK_ACTION_TYPE_ID’,
				object_id:  ‘UNIQUE_OBJECT_ID_IN_CUSTOM_APP’,
				object_name:  ‘UNIQUE_OBJECT_NAME_IN_CUSTOM_APP’,
				object_descr:  ‘OBJECT_DESCRIPTION,
				object_url:  ‘DIRECT_OBJECT_URL’
			}, function(response) {
				//JSON response containing HUB action ID
				//i.e. { success:1, id:1298 }
			});
```

### Share on Facebook

```javascript
			HUB.facebookShare(title, link_url, descr, img_url);
```

### Share on Twitter

```javascript
			HUB.twitterShare(text, img_or_link_url);
```

#### Facebook Insights
Please visit the following link for a list of all stats available through the Facebook Insights API:

https://developers.facebook.com/docs/reference/fql/insights/ 

# Data API

The Blueye Hub Data API can be utilized for a wide variety of applications. The flexibility of the data architecture provides support for many different data schemas, while storing the data in a unified manner that allows for sharing of data between applications. Built-in analytics allows developers to concentrate on core application implementation while auto-tracking the relevant user actions needed to power the Hub Conversion Engine and Customer Insights.


### Importing Data

The data can be imported manually or via csv upload using the Developer Data Management Tool. We can also pull data in from your proprietary API, on request, as this may require some additional customization.

Each group of similar items is considered a "data set". Related data sets can be linked to each other in a hierarchical pattern, meaning each data set can have a parent and any number of children. In addition to standard properties (i.e. title, description, value) and custom properties (those you define), each individual item in a data set has a number of connections that facilitate the Hub's support of many different type of applications. For example the 'geo location' connection allows you to define fields such as latitude, longitude, and address, while the 'media' connection supports the uploading and attachment of image and video data to an item.


### Retrieving Data

Once data has been imported it can be retrieved in your application by invoking the 'dataSet' method of the Hub API and passing in the unique data set ID.

```javascript
	HUB.api('dataSet', { id:61 }, function(response) {
		$.each(response.data, function(i, item) {
			$('.my_container').append(item);
		});
	});
```

You'll notice that we immediately appended the returned item to our HTML container. This is because the API returns an array of HTML jQuery Div objects, not typical JSON. This approach allows us to embed the appropriate event handlers directly into your data objects needed to handle auto click-tracking as well as live editing. So basically, you as a developer don't need to worry about item level analytics, and as an added bonus, a CMS is automatically built into your app!

In most cases, you'll probably need to manipulate the properties an/or style of each item. Since the items returned are jQuery objects, you can manipulate them as you please via the standard jQuery functions (i.e. you could simply call item.addClass or item.css to add you own app specific styling). The actual item properties (those defined when uploading the data) can be retrieved using the jQuery data method. For instance, to access the item 'title' property, call item.data('title').

### Data Set Children

Many of the applications you'll create require the user to walk through a step by step experience / commerce builder, each time accessing a new data set in the hierarchy. Provided you've taken the time to properly organize you data hierarchy, presenting the new leg of data to the user is as simple as calling the same 'dataSet' method, but this time passing in the prior steps data set ID as the parent ID. Typically, the next data set will not only be a child of the prior one, but more specifically, a child of a specific item (that which was clicked by the user in the previous step). In this case, also pass in the the parent item ID.

<table>
    <tr>
        <th>Field</th>
        <th>Description</th>
        <th>Type</th>
    </tr>
    <tr>
      <td>parent_id</td>
      <td>Parent data set ID</td>
      <td>Integer</td>
    </tr>
    <tr>
      <td>parent_item</td>
      <td>Parent item ID in parent data set</td>
      <td>Integer</td>
    </tr>
    <tr>
      <td>force_items</td>
      <td>Force items (rather than data set header info) to be returned in cases where there are multiple child data sets (defaults to 0)</td>
      <td>Boolean</td>
    </tr>
</table>

```javascript
	HUB.api('dataSet', { parent_id:61, parent_item:1307, force_items:1 }, 
		function(response) {
			$.each(response.data, function(i, item) {
				$('.my_container').append(item);
			});
		}
	);
```

### User Item Selections

At some point you'll want to record that a user made a final selection. This could occur in a commerce builder, poll, or even contest.

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>id</td>
    <td>Top level data set ID</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>item_data</td>
    <td>Any custom data you wish to store with this item selections</td>
    <td>JSON</td>
  </tr>
  <tr>
    <td>clear</td>
    <td>Whether or not to clear the user's previous selections (defaults to 0)</td>
    <td>Boolean</td>
  </tr>
</table>

```javascript
	HUB.api('selectItem', { id:61, item_data:{ 'friends':[34, 12, 45] }, user_id:fbId, clear:1 }, 
		function(res) {
			//returns JSON response, i.e. { success:1 }
		}
	);
```

To return items selected using the above API call, make a call to 'selectedItems' with the top level data set ID and user's ID


```javascript
	HUB.api('selectedItems', { id:61, user_id:fbId }, function(res) {
		if(res.data.length > 0) {
			//NOTE: this returns JSON data, not jQuery objects!
		}
	});
```

### UGC

The Hub also provide supports for the myriad of applications that can be created around the concept of User Generated Content. Examples include anything ranging from a contest to a simple contact form. Through our API, users can create their own data items using the same flexible data structure we've built for application managed data. None of the fields below are required, and custom properties are also allowed.


<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>user_id</td>
<td>App user ID if exists</td>
<td>String</td>
</tr>
<tr>
<td>fb_id</td>
<td>FB user ID if exists</td>
<td>String</td>
</tr>
<tr>
<td>short_text</td>
<td>Text with a maximum of 200 characters</td>
<td>String</td>
</tr>
<tr>
<td>long_text</td>
<td>Text with maximum 500 characters</td>
<td>String</td>
</tr>
<tr>
<td>media_url</td>
<td>Image or video URL</td>
<td>String</td>
</tr>
<tr>
<td>image</td>
<td>Id of html file input field. This allows you to upload an image directly, rather than using the media_url field.</td>
<td>String</td>
</tr>
<tr>
<td>data</td>
<td>Any custom data in JSON format</td>
<td>JSON</td>
</tr>
</table>

```javascript
	var data = { name:"John Doe", email:"john@gmail.com", media_url:"http://test.com/me.png" };
	
	HUB.api('ugc', { fb_id:'3107076', 'short_txt':'My contest entry', data:data }, function(res) {
		//returns JSON response, i.e. { success:1, ugc_id:23 }
	});
```

### Retrieving UGC

UGC can be retrieved by user_id, fb_id, or for the entire app. You must specify the individual fields you want retrieved. Please see the example below for more details.

<table>
<tr>
<th>Field</th>
<th>Description</th>
<th>Type</th>
</tr>
<tr>
<td>start</td>
<td>The first index to return in the response data array. This is useful when paging through data. (optional)</td>
<td>Integer</td>
<tr>
<td>limit</td>
<td>How many records to return. The default number is 50. (optional)</td>
<td>Integer</td>
</tr>
<tr>
<td>fields</td>
<td>a comma delimited list of fields to return. These are the same field names set when pushing the UGC data.</td>
<td>String</td>
</tr>
<tr>
<td>user_id</td>
<td>User ID specified when UGC was created (optional)</td>
<td>String</td>
</tr>
<tr>
<td>fb_id</td>
<td>Facebook ID specified when UGC was created (optional)</td>
<td>String</td>
</tr>
</table>

```javascript
	HUB.api('getUGC', { limit:12, fields:'user_id,fb_id,media_url,short_txt' }, 
		function(res) {
			//returns JSON response, i.e. { success:1, data:[] }
		}
	);
```

