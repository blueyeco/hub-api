# Data API

The Blueye Hub Data API can be utilized for a wide variety of applications. The flexibility of the data architecture provides support for many different data schemas, while storing the data in a unified manner that allows for sharing of data between applications. Built-in analytics allows developers to concentrate on core application implementation while auto-tracking the relevant user actions needed to power the Loyalty Hub Conversion Engine and Customer Insights.


### Importing Data

The data can be imported manually or via csv upload using the Developer Data Management Tool. We can also pull data in from your proprietary API, on request, as this may require some additional customization.

Each group of similar items is considered a "data set". Related data sets can be linked to each other in a hierarchical pattern, meaning each data set can have a parent and any number of children. In addition to standard properties (i.e. title, description, value) and custom properties (those you define), each individual item in a data set has a number of connections that facilitate the Loyalty Hub's support of many different type of applications. For example the 'geo location' connection allows you to define fields such as latitude, longitude, and address, while the 'media' connection supports the uploading and attachment of image and video data to an item.


### Retrieving Data

Once data has been imported it can be retrieved in your application by invoking the 'blhSet' method of the Loyalty Hub API and passing in the unique data set ID.
