# iOS Mobile SDK
The iOS Mobile SDK allows you to integrating you custom mobile application into The Blueye Hub's data collection and reporting infrastructure. Users can then be segmented and targeted via various channels in the Hub's media platform.

Initializing the SDK

To initialize the SDK, include the following Javascript file into your web application

http://hub.blueye.com/js/api.js

The SDK inserts a div element with the ID hub-root, containing an iframe with the ID hub-frame, into your web application’s source. The HUB object included in the SDK provides access to the various API requests describe in the section below.

Authentication

Please contact your account manager to obtain an authorization key required to initialize the SDK.

            HUB.init({
                apiKey: '1a1e31b4d4a3b5191ca22a6919ade490'
            }, function(response) {
                if(response.success) {
                    alert(‘Successfully initialized the SDK’);
                }
                else {
                    alert(response.message);
                }
            });
