# Data API

The Blueye Hub Data API can be utilized for a wide variety of applications. The flexibility of the data architecture provides support for many different data schemas, while storing the data in a unified manner that allows for sharing of data between applications. Built-in analytics allows developers to concentrate on core application implementation while auto-tracking the relevant user actions needed to power the Loyalty Hub Conversion Engine and Customer Insights.


### Importing Data

The data can be imported manually or via csv upload using the Developer Data Management Tool. We can also pull data in from your proprietary API, on request, as this may require some additional customization.

Each group of similar items is considered a "data set". Related data sets can be linked to each other in a hierarchical pattern, meaning each data set can have a parent and any number of children. In addition to standard properties (i.e. title, description, value) and custom properties (those you define), each individual item in a data set has a number of connections that facilitate the Loyalty Hub's support of many different type of applications. For example the 'geo location' connection allows you to define fields such as latitude, longitude, and address, while the 'media' connection supports the uploading and attachment of image and video data to an item.


### Retrieving Data

Once data has been imported it can be retrieved in your application by invoking the 'blhSet' method of the Loyalty Hub API and passing in the unique data set ID.

```javascript
	ABS.api('blhSet', { id:61 }, function(response) {
		$.each(response.data, function(i, item) {
			$('.my_container').append(item);
		});
	});
```

You'll notice that we immediately appended the returned item to our HTML container. This is because the API returns an array of HTML jQuery Div objects, not typical JSON. This approach allows us to embed the appropriate event handlers directly into your data objects needed to handle auto click-tracking as well as live editing. So basically, you as a developer don't need to worry about item level analytics, and as an added bonus, a CMS is automatically built into your app!

In most cases, you'll probably need to manipulate the properties an/or style of each item. Since the items returned are jQuery objects, you can manipulate them as you please via the standard jQuery functions (i.e. you could simply call item.addClass or item.css to add you own app specific styling). The actual item properties (those defined when uploading the data) can be retrieved using the jQuery data method. For instance, to access the item 'title' property, call item.data('title').

### Data Set Children

Many of the applications you'll create require the user to walk through a step by step experience / commerce builder, each time accessing a new data set in the hierarchy. Provided you've taken the time to properly organize you data hierarchy, presenting the new leg of data to the user is as simple as calling the same 'blhSet' method, but this time passing in the prior steps data set ID as the parent ID. Typically, the next data set will not only be a child of the prior one, but more specifically, a child of a specific item (that which was clicked by the user in the previous step). In this case, also pass in the the parent item ID.

<table>
    <tr>
        <td>Field</td>
        <td>Description</td>
        <td>Type</td>
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
	ABS.api('blhSet', { parent_id:61, parent_item:1307, force_items:1 }, 
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
	ABS.api('blhSelectItem', { id:61, item_data:{ 'friends':[34, 12, 45] }, user_id:fbId, clear:1 }, 
		function(res) {
			//returns JSON response, i.e. { success:1 }
		}
	);
```

To return items selected using the above API call, make a call to 'blhSelectedItems' with the top level data set ID and user's ID


```javascript
	ABS.api('blhSelectedItems', { id:61, user_id:fbId }, function(res) {
		if(res.data.length > 0) {
			//NOTE: this returns JSON data, not jQuery objects!
		}
	});
```

### UGC

The Loyalty Hub also provide supports for the myriad of applications that can be created around the concept of User Generated Content. Examples include anything ranging from a contest to a simple contact form. Through our API, users can create their own data items using the same flexible data structure we've built for application managed data. None of the fields below are required, and custom properties are also allowed.


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
