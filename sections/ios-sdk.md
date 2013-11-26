# iOS Mobile SDK
The iOS Mobile SDK allows you to integrating you custom mobile application into The Blueye Hub's data collection and reporting infrastructure. Users can then be segmented and targeted via various channels in the Hub's media platform.

### Installing the SDK

Download the SDK <a href="https://hub.blueye.com/resources/BlueyeHub.framework.zip" target="_blank">here</a> and extract the files anywhere on your local machine.

To connect to the Hub, the mobile SDK requriess an API key that is unique to your application. To obtain your key, please create a new app after logging in to the Hub Developer Console. In your app settings, be sure to select 'Mobile App' and enter a Google Analytics ID, which is required for event tracking.
<img src="http://hub.blueye.com/img/docs/dev_console.png" />

## Add the Hub SDK to your iOS project by right clicking Frameworks in the project navigator, selecting 'Add Files to...' and selecting the folder extracted when downloading the SDK (make sure to just select the folder level and not an individual file).


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
