# Map Module

This API provides access to the ABS Platform’s Map Module. This API resides outside of the Javascript SDK and is accessed via direct URL calls, with all fields set using key/value query string parameters.

All requests require your map’s unique authorization token (field ‘token’) in addition to the specific fields listed below for each request.

### Display Map

http://platform.alwaysbesocial.com/api/YOUR_MAP_IDENTIFIER

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>w</td>
    <td>Map width</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>h</td>
    <td>Map height</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>lt</td>
    <td>Map center latitude position</td>
    <td>Decimal</td>
  </tr>
  <tr>
    <td>ln</td>
    <td>Map center longitude position</td>
    <td>Decimal</td>
  </tr>
  <tr>
    <td>z</td>
    <td>Zoom level of map</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>m</td>
    <td>Comma delimited list of the IDs of markers to show on the map. If excluded, all map markers will be shown. Use a value of -1 to show no markers</td>
    <td>Integers</td>
</table>

### Create Marker

http:// platform.alwaysbesocial.com/api.php?action=externalMap.createMarker

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>lat</td>
    <td>The marker’s latitude position</td>
    <td>Decimal</td>
  </tr>
  <tr>
    <td>lng</td>
    <td>The marker’s longitude position</td>
    <td>Decimal</td>
  </tr>
  <tr>
    <td>address</td>
    <td>The address to show in the map’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>title</td>
    <td>The title to show in the marker’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>copy</td>
    <td>The description to show in the marker’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>link</td>
    <td>URL of a link to include in the marker’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>icon_id</td>
    <td>The marker icon’s image ID</td>
    <td>Integer</td>
  </tr>
</table>

Returns a JSON object containing the marker’s ID – { success:1, marker_id:243 }

### Update Marker

http://platform.alwaysbesocial.com/api.php?action=externalMap.updateMarker

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>lat</td>
    <td>The marker’s latitude position</td>
    <td>Decimal</td>
  </tr>
  <tr>
    <td>lng</td>
    <td>The marker’s longitude position</td>
    <td>Decimal</td>
  </tr>
  <tr>
    <td>address</td>
    <td>The address to show in the map’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>title</td>
    <td>The title to show in the marker’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>copy</td>
    <td>The description to show in the marker’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>link</td>
    <td>URL of a link to include in the marker’s info window</td>
    <td>String</td>
  </tr>
  <tr>
    <td>icon_id</td>
    <td>The marker icon’s image ID</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>id</td>
    <td>The marker’s unique ID</td>
    <td>Integer</td>
  </tr>
</table>

Returns a JSON object containing the marker’s ID – { success:1, marker_id:243 }

### Remove Marker

http://platform.alwaysbesocial.com/api.php?action= externalMap.destroyMarker

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>marker_id</td>
    <td>The marker’s ID</td>
    <td>Integer</td>
  </tr>
</table>

Returns a JSON object – { success:1 }

### Remove All Markers

http://platform.alwaysbesocial.com/api.php?action=externalMap.destroyAllMarkers

Returns a JSON object – { success:1 }

### Create Review

http://platform.alwaysbesocial.com/api.php?action=externalMap.createReview

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>marker_id</td>
    <td>The ID of the marker being reviewed</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>review</td>
    <td>The review message</td>
    <td>String</td>
  </tr>
  <tr>
    <td>rating</td>
    <td>Rating for review 1 – 5</td>
    <td>Integer</td>
  </tr>
</table>

Returns a JSON object containing the review’s ID – { success:1, review_id:243 }

### Update Review

http://platform.alwaysbesocial.com/api.php?action=externalMap.updateReview

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>marker_id</td>
    <td>The ID of the marker being reviewed</td>
    <td>Integer</td>
  </tr>
  <tr>
    <td>review</td>
    <td>The review message</td>
    <td>String</td>
  </tr>
  <tr>
    <td>rating</td>
    <td>Rating for review</td>
    <td>Integer</td>
</table>
Returns a JSON object containing the review’s ID – { success:1, review_id:243 }

### Remove Review

http://platform.alwaysbesocial.com/api.php?action=externalMap.destroyReview

<table>
  <tr>
    <th>Field</th>
    <th>Description</th>
    <th>Type</th>
  </tr>
  <tr>
    <td>review_id</td>
    <td>The review’s ID</td>
    <td>Integer</td>
  </tr>
</table>
Returns a JSON object – { success:1 }



