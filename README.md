# Productivity Tools

This is just a collection of tools that I made up because they seemed
useful.  They all use a single configuration file expected to be in
~/.config.yml.  Documentation for the individual pieces are with them.


## Notifications

Simple library for sending notifications to your phone consisting of 2
parts.  The first is `notify-me` a script for sending yourself
notifications through the Pushover API.  It depends on the
following configuration options:

- notifications:  
  - pushover:  
    application: YOUR-APP-KEY  
    user: YOUR-USER-KEY  

The second part is a reminder system that uses the script `remind-me` to
schedule notifications and the daemon `reminderd` to send them over
time.  `reminderd` expects `notify-me` to be in the PATH.  To set up
`reminderd` on Linux simply use the cron.  On OS X do the following:

1. Create a valid .plist file in $HOME/Library/LaunchAgents specifying
   the path to reminderd.  Call this file com.reminderd.plist.

   An example file [here](http://alvinalexander.com/mac-os-x/mac-osx-startup-crontab-launchd-jobs)

2. Activate this by running `launchctl load com.reminderd.plist`

3. If you want to deactivate this for some reason simply run
   `launchctl unload com.reminderd.plist`
