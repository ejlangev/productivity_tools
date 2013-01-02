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

   An example file: 

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
    "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
      <key>Label</key>
      <string>com.devdaily.crontabtest</string>

      <key>ProgramArguments</key>
      <array>
        <string>/Users/al/bin/crontab-test.sh</string>
      </array>

      <key>Nice</key>
      <integer>1</integer>

      <key>StartInterval</key>
      <integer>60</integer>

      <key>RunAtLoad</key>
      <true/>

      <key>StandardErrorPath</key>
      <string>/tmp/AlTest1.err</string>

      <key>StandardOutPath</key>
      <string>/tmp/AlTest1.out</string>
  </dict>
  </plist>

2. Activate this by running `launchctl load com.reminderd.plist`

3. If you want to deactivate this for some reason simply run
   `launchctl unload com.reminderd.plist`
