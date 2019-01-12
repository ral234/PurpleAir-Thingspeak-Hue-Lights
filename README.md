# PurpleAir-Thingspeak-Hue-Lights

This application is intended to use PurpleAir sensor data to control a Phillips Hue light beacon from Thingspeak

Step 1:  Install PurpleAir sensor:   see instructions at purpleair.com/install
  Note the name given to the sensor during installation.
  It may take several hours for the sensor data to show up on the purple air map.  
  
Step 2:  Open the page purpleair.com/json and search for the sensor name from step 1. 
  Save a copy of the JSON data pertaining to the sensor.  The Thingspeak IDs (<CHANNEL_ID>) and Read Keys (<CHANNEL_READ_KEY>) are
  needed to access data from the private thingspeak.com channel.
  Use https://api.thingspeak.com/channels/<CHANNEL_ID>/feeds.json?api_key=<CHANNEL_READ_KEY>&results=2 to view the last 2 results
  and see their format, data, etc.   
  
Step 3:  Login to thingspeak.com and verify that the data is accessible.  Since this is a private channel, the channel can't be accessed 
  directly, but the data can be used in a Matlab Analysis, React, ThingHTTP, or other application.
  Create additional channels to store processed data or other parameters that need to be maintained or modified over time.  

Step 4:  Create a Hue Developers Account at https://www.developers.meethue.com/
  Create a new app and note the App name, client key, client secret.  
  Read the Hue API documentation at: https://developers.meethue.com/develop/hue-api/remote-authentication/
  
Step 5:  Create a new app id in Hue developer.  Note the app name(id), Client ID, and Client Secret for later use.  

Step 6: Whitelist the application following the instructions at: https://developers.meethue.com/develop/hue-api/remote-api-quick-start-guide/  This will return a user name that will be used to later create a set of access tokens.   As part of this process you will need to push the button on your hue bridge to authorize access.  

Step 7:  Use HTTPie to initiate the authentication sequence.  The response to this request contains a redirect to Hue requiring you to login to your account and authorize user access to your bridge.  
 
Run this using HTTPiefrom python37-32> 
http --print=HBhb GET https://api.meethue.com/oauth2/auth? clientid==ExWVqNNQoX8JCblajnNzCxLgPjlOSc4s appid==testaqidisplay deviceid==pyhttptester state==startauthreq response_type==code devicename==mypypc

 Copy the redirect link and paste into a web browser.  Follow instructions to authorize access.  This will then redirect back to a nonexistant application, but will provide a code in the browser line.  Copy this code and paste into New Hue Token with Access Code in the uri after code=<    >&...  and execute.  This will create and store a new set of Hue tokens.  
 

