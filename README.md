# Rust Server Utility with Remote Restart
Utility for automating updates and remotely restarting [Rust](https://playrust.com/) server.
Created and Compiled with [AutoIT](https://www.autoitscript.com)
Originally written for use on [Gamercide's](https://gamercide.org) Server

 Automate your Rust Server Management with this Utility! Written using AutoIT with full Source available.
 
 **UPDATE CHECK REQUIRES THE SCRIPT CAN WRITE TO SteamCMD directory**
 
# Rust Server Utility Features
*   Manage Multiple servers with multiple Utilities (See Below)
*   Monitors for crashes and Restarts Server if process closes
*   Optionally Restart the server daily at a certain time (Up to 6 different times through the day)
*   Optionally Use Remote Restart Utility to Restart server remotely using unique passwords (Optionally Set Users) and port
*   Optionally Use SteamCMD for automatic updates ( SteamCMD will be downloaded if not found )
*   Optionally Compare running server version with released version for automatic Update (In 5 to XX minute intervals)
    * *UPDATE CHECK REQUIRES THE SCRIPT CAN WRITE TO SteamCMD directory*
*   Optionally run verification every time SteamCMD is ran
*   Optionally restart server on excessive memory use.
*   Optionally Notify Discord Channel before Restart using Webhook
*   Optionally Notify Multiple Twitch Channels using IRC
*   Log Excessive memory use. Set to a very large number if you don't wish to log anything
*   Set Game Name, Game IP, Game port, Game description, max players, world size, and more.
*   Rotate X number of logs created by utility every X hours
*   Optionally Download Oxide when server restarts or is updated.
*   Optionally generate new random server seed on the first Thursday of each month.

# Rust Remote Restart Features
*   If enabled on the server, use to remotely restart the server.
*   Set Password in INI file to save, or type each time.
*   Restart using IP or Domain Name

This utility, when SteamCMD and daily restarts are enabled, will keep the server up to date on a daily basis.  You can also use  SteamCMD and remote restart to update the server anytime you send the restart request. If CheckForUpdate is enabled this utility will pull the latest version from SteamCMD and compare it to the local app manifest.  If it finds a newer version, it will automatically restart to update the server.

A few things to note. The Game Server IP will be the IP you wish to bind to. This may be a local IP if your server is behind a router.  Also, the game can take a long time to gracefully shut down. So, when the restart is initiated, the utility attempts to gracefully shut down the server. If the server will not shut down gracefully after 1 minute the process is forcefully closed. When SteamCMD is used, a full cycle from the time the command is sent to the time the server is back on line can take 10 minutes or more.  Finally, the remote restart port needs to be allowed through your firewall. 

# Running Multiple Servers on the Same Machine
Place a copy of the EXE in a different Rust_Server directory, update the INI file to make sure you have no port conflicts, and run the script.  A couple of things you might want to do to help manage two or more running at once. Change the RustServerUtility.exe names to something Utility1 and Utility2 or something like that. Also, you probably should set the Minute about 30 minutes apart from each so they are not restarting at the same time.

### Using Update Check on Multiple Servers
If you plan on running multiple servers on the same machine, I suggest you create different SteamCMD folders for each server. Due to the way the update is checked, if your servers checked at the same time, it could cause a conflict. This could result in an update being missed for all servers.  

# How to Use Discord Bot
* UseDiscordBot
 * Set to yes to notify Discord Channel before Server Restart
* DiscordWebHookURL
 * This is your Webhook  URL provided by discord. ( Instructions below for Desktop Application )
    1. Right Click on your server
    2. Open Server Settings > Webhooks
    3. Click Create Webhook
    4. Select which Channel you want the bot to announce to (Important)
    5. Under Webhook URL Click the Copy Button next to the URL
    6. Paste the entire Webhook to the INI after DiscordWebHookURL=
       * To use multiple webhooks, separate each full webhook URL with a comma `,`
* DiscordBotName
 * This will override the Name you setup in your webhook. Leave Blank to use default.
* DiscordBotUseTTS
 * Yes will make the bot announce with Text to Speech. No will turn off TTS
* DiscrodBotAvatarLink
 * This is a fully qualified URL to an Image for the Bot Avatar. Will override default. Leave blank for default.
The Bot will announce immediately upon restart time. Notifying how long users have based on the time you set. The bot will then announce 1 minute before the server restarts. Finally, the bot will announce exactly as the restart command is sent. Announcements will be sent for Daily Restarts and Update Restarts. Remote Restarts are considered Admin controlled and immediately restart the server without notice.
```
[Use Discord Bot to Send Message Before Restart? yes/no]
UseDiscordBot=yes
DiscordWebHookURL=https://discordapp.com/api/webhooks/AAAAAAA/AAAAAA,https://discordapp.com/api/webhooks/BBBBBB/BBBBB
DiscordBotName=Rust Test Bot
DiscordBotUseTTS=yes
DiscordBotAvatarLink=
```

# How to use Twitch Bot
* UseTwitchBot
 * Set to yes to notify Twitch Channels before Server Restart
* TwitchNick
 * This is your Twitch nickname. It can be an account created for a bot , or your personal account.
* ChatOAuth
 * This is the key needed to connect to chat over IRC. You need to generate one for this to work.
    1. Go to this URL https://twitchapps.com/tmi
    2. Connect to your account.
    3. Copy the generated key.
    4. Paste the entire key to the INI after ChatOAuth=
* TwitchChannels
  * These are the channels you wish to send the announcement to. You can send to just one or you can send to multiple channels. Separate each channel with a comma `,` `TwitchChannels=channel1,channel2`

The Bot will announce immediately upon restart time. Notifying how long users have based on the time you set. The bot will then announce 1 minute before the server restarts. Finally, the bot will announce exactly as the restart command is sent. Announcements will be sent for Daily Restarts and Update Restarts. Remote Restarts are considered Admin controlled and immediately restart the server without notice.
```
[Use Twitch Bot to Send Message Before Restart? yes/no]
UseTwitchBot=no
TwitchNick=twitchbotusername
ChatOAuth=oauth:1234 (Generate OAuth Token Here: https://twitchapps.com/tmi)
TwitchChannels=channel1,channel2,channel3
```
# Notificatin In Game
* NotifyInGame
 * Set to yes to notify in Game before Server Restart.
 
```
[Send Message to in Game Players Before Restart? yes/no]
NotifyInGame=yes
```

# Notification Time
* TimeBeforeRestart
 * Set the time in minutes before restarting. This will be used for all notification methods.

```
[Set the Delay Time Before Restarting when using any Notification Method (minutes)]
TimeBeforeRestart=5
```

## Using Multiple Restart Codes

You can set multiple anonymous user passwords by separating each with a comma `,`
`RestartCode=pass1,pass2,pass3`

You can specify the user in the password string by separating user from password with underscore `_`
`RestartCode=User1_Pass1,User2_Pass2`

Or you can mix methods
`RestartCode=User1_Pass1,pass2,User2_Pass2`

On the Remote Restart Utility the user will enter the full string regardless of using the username or not. The user name is there mainly for logging purposes. To trigger a restart the full string between the comma , has to match.

## Examples:
`RestartCode=pass1,pass2,pass3,Admin1_pass4`
* User enters *pass1* in Restart Utility:
  * Server resets and Log displays: Anonymous user @ IP triggered restart using pass1 ( Hidden by default )
* User enters *Admin1_pass4* in Restart Utility
  * Server resets and Log displays: Admin1 @ IP triggered restart using pass4 ( Hidden by default )
* User enters *wrongpassword* in Restart Utility
  * Server does NOT reset and Log displays: Restart Attempt @ IP using string *wrongpassword* (failed attempts are always shown in full)
* User enters *Admin1_wrongpassword*
  * Server does NOT reset and Log displays: Restart Attempt @ IP using string *Admin1_wrongpassword* (failed attempts are always shown in full)

# Hide Passwords in Log
Additionally, I have added the option to Obfuscate passwords in the log files. Currently that is done by replacing all except 4 characters starting with the 4th character with *

`ObfuscatePass="no"` to display full passwords in log.

## Example:
`ObfuscatePass="yes"` and `AdminPass=aPasWd123`

Log displays `AdminPass=***sWd1**`

# END
