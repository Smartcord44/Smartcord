Smartcord.cc is an Open Source Verification system for discord members. It is allowed to use it private and it is allowed to Sell it IF YOU RELEASE UR VERSION ON GITHUB AND YOU HAVE TO ADD CREDITS!.

We DONT Help you with ur selfhost version so PLEASE Dont dm us bc we will just ignore it!


Features
- Multi server
- Restore members (nothing else, this was one of the early versions of Smartcord)
- IP logging
- Discord webhook notifications
- Handles rate limiting and access token expiry. Most bots don't and break when you try to pull members, not Smartcord
- VPN block
- IP blacklisting

How to setup
PHP and MySQL. Should work on most PHP versions. I tested on PHP 7.4 and PHP 8.0, worked on both. **You must have a VPS. Shared hosting such as NameCheap will not work, as you have to run c# application also**

Please setup your MySQL database now and import the structure from the Smartcord.sql file

- Change the Smartcord.com on line 20 of the /website source/verify/index.php file to example.com (where example.com is your website's domain)
- Replace botTokenHere with your Discord bot token on line 14 of the /website source/includes/connection.php file
- (optional - only needed if you do NOT use cloudflare) change HTTP_CF_CONNECTING_IP to REMOTE_ADDR (do NOT do this if you're using cloudflare) at line 77, line 82, line 120, line 211, and line 290 of the /website source/verify/index.php file
- (optional - only needed if you have more than 1,000 people verify a day) change proxyCheckKeyHere to a proxycheck API key if you have so many users you need to pay on line 84 of the /website source/verify/index.php file
- Change OAuth2 authorization link on line 419 of the /website source/verify/index.php file you get your authorization link from Discord developer portal, like this https://imgur.com/a/G3q4oDM
- Change captcha keys here line 38 and line 101 of the /website source/register/index.php file or remove the captcha. I don't recommend removing captcha if you plan to sell this. Captcha is very neccesary for public websites. But if it's not a commercial site, you should remove lines 100-109 and then register will work
- Set MySQL connection info at line 5 of the /website source/includes/connection.php file
- If you have other users than yourself owning servers on this source and you want to log their actions, replace discordWebhookHere with your webhook url on line 445, line 499, line 573 of the /website source/dashboard/account/settings/index.php file and line 23 of the /website source/includes/connection.php file
- If you plan to sell this source, replace 8hCOmd6 with your Shoppy.GG product ID on line 243 of the /website source/dashboard/account/upgrade/index.php file and then on Shoppy.GG, set these settings for the product https://imgur.com/a/XkRC3Pe and then make sure you set your Shoppy.GG webhook secret on line 18 of the /website source/includes/connection.php file
- Replace DiscordBotClientID with your Discord bot's application ID on line 12 of the /website source/includes/connection.php file
- Replace DiscordBotClientSecret with your Discord bot's client secret on line 13 of the /website source/includes/connection.php file
- Replace https://Smartcord.com/auth/ with https://example.com/auth/ and use your website's domain instead of example.com on line 16 of the /website source/includes/connection.php file
- Replace https://Smartcord.com/verify/ with https://example.com/verify/ and use your website's domain instead of example.com on line 17 of the /website source/includes/connection.php file

Now for c# part

- Change https://Smartcord.com/auth/ to https://example.com/verify/ and use your website's domain instead of example.com on line 113 of the /bot source/Smartcord/Commands/Pull.cs file
- (important, you don't want Discord to think you're a bot Smartcord owns and ban you) Change Smartcord (public release, 1.0.0.0) to the name of your site or something on line 38 of the /bot source/Smartcord/Miscellaneous/Utilities.cs file
- Replace rest_admin with database username, replace rest_main with database name on line 8 of the /bot source/Smartcord/Services/Database.cs file
- Replace databasePasswordHere with database password on line 127 of the /bot source/Smartcord/Properties/Resources.resx file
- Replace clientSecretHere your Discord bot's client secret on line 124 of the /bot source/Smartcord/Properties/Resources.resx file
- Replace discordIdHere with your Discord bot's application ID on line 121 of the /bot source/Smartcord/Properties/Resources.resx file
- Replace botTokenHere with your Discord bot's token on line 139 of the /bot source/Smartcord/Properties/Resources.resx file

Note that this is written for Debian 11. For any other distro this is self explanatory. If you can't figure this out then leave.

wget https://packages.microsoft.com/config/debian/11/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb

sudo apt-get update; \
sudo apt-get install -y apt-transport-https && \
sudo apt-get update && \
sudo apt-get install -y dotnet-sdk-5.0 dotnet-runtime-5.0

For this next part make sure you are in the bot's root directory.

dotnet restore
dotnet build

You now have an executable!

Create a service using systemctl, make sure to replace the paths.

[Unit]
Description=Nebula Mods Inc. Restorecord
After=multi-user.target
[Service]
WorkingDirectory=/path/to/working/directory
ExecStart=/path/to/bot/executable
SyslogIdentifier=Restorecord
Type=idle
Restart=always
RestartSec=15
RestartPreventExitStatus=0
[Install]
WantedBy=multi-user.target

Once you set this up, the bot should come online and slash commands should work, do / and you'll see slash commands

Here's a YouTube video showing how to use the bot https://www.youtube.com/watch?v=dVWPEdJY0zA


How to give yourself lifetime premium (replace yourUsernameHere with your username):

UPDATE `users` SET `role` = 'premium',`expiry` = 2224663363 WHERE `username` = 'yourUsernameHere'
Security issues/bugs
Don't care, not fixing. This is not my issue anymore, I'm simply releasing for whoever wants it. 
