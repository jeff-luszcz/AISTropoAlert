

# AISTropoAlert
Script to send a Mastodon alert when far away ships are seen using AIS ship reports

**Copyright 2023 Jeffrey Luszcz**

[https://github.com/jeff-luszcz/AISTropoAlert](https://github.com/jeff-luszcz/AISTropoAlert)

This script is licensed under the terms of the Apache 2.0 license

SPDX-License-Identifier: Apache License 2.0

## About
This BASH script reads the input from a specific AIS-Catcher web server 
and checks to see if any reports are further than a user specified distance
Seeing ships that are farther away than normal may indicate the Tropospheric Ducting
or other long distance propagation at VHF/UHF frequencies is ongoing. This is of interest to Amateur Radio operators

See [https://en.wikipedia.org/wiki/Tropospheric_propagation](https://en.wikipedia.org/wiki/Tropospheric_propagation)

### Requirements
* This script requires the **curl** command line tool
* This script requires the **jq** command line tool
* This script requires **AIS-Catcher** to be running its web server interface
* This script requires AIS-Catcher to have **Lat-Long flags** or GPS enabled (e.g. share_loc on LAT lat.dddd LON long.dddd )
* A **Mastodon account**
* A **Mastodon token**


###Installation instructions;

Install [AIS-Catcher](https://github.com/jvde-github/AIS-catcher) if needed


Install jq if needed

    sudo apt install jq

Install curl if needed

    sudo apt install curl


Place the BASH script in a location on your file system (e.g. ~/bin/AISTropoAlert.sh)

Make the script executable

      chmod +x AISTropoAlert.sh


Replace the variable tokens in the AISTropoAlert.sh script with your information

1. DIST, a distance that represents far away ship reports (e.g. 10 or 20 miles or further)
2. URL, the URL of your AIS-Catcher web interface e.g. raspberrrypi.local:8383
3. MASTODON_URL, the URL of the posting API for your Mastodon server (e.g. https://mastodon.social/api/v1/statuses )
4. MASTODON_TOKEN, your secret Mastodon token, see instructions at [here](https://dev.to/bitsrfr/getting-started-with-the-mastodon-api-41jj) on how to generate a Token for yourself


Edit the status message with your location (default message says **[replaceme]**)

Create a cronjob for this script
    
    crontab -e
    
put in the following for your cron job

    */15 * * * * /home/yourname/bin/AISTropoAlert.sh

This will run this script every 15 minutes, edit yourname to be your user name or directory name

I recommend running AIS-Catcher as a service so it will always be running even after a reboot

When ships appear outside your distance limit, this script should make a posting to your Mastodon user
The text that is posted can be customized by editing the status line as seen in the curl call in the script
Te default status will post message in the format below:

    Possible Tropo Near Boston: AIS reports from 7.064232 miles away seen 
    at Fri 26 May 2023 12:00:02 PM EDT. Alerts triggered when ships seen over 2 miles away.




### Future improvements
Show total ship count currently seen
