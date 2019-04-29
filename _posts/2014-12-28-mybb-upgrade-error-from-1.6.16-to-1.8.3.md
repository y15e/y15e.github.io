---
layout: post
title: "MyBB upgrade error from 1.6.16 to 1.8.3"
---

I use MyBB forum application in my private project. Current version is 1.6.16, it is too old so I tried to upgrade to the latest 1.8.3.

1. Download the latest MyBB package file.

   ```
   $ wget http://resources.mybb.com/downloads/mybb_1803.zip
   ```

2. Extract the zip file and copy to existing directory.

   ```
   $ cd ./downloaded_directory
   $ unzip mybb_1803.zip
   $ rsync -av ./Upload/ /existsing/mybb/directory/
   ```

3. Open the url in browser for upgrade.

   ```
   http://my-personal-project-hostname/install/upgrade.php
   ```

Then I got following error.

> MyBB has experienced an internal SQL error and cannot continue.
> 
> SQL Error:
> 1366 - Incorrect string value: '\x94W' for column 'ip' at row 1
> Query:
> REPLACE INTO mybb_sessions SET \`uid\`='1',\`sid\`='577294dda4c2090968dbbe2f2951183d', \`time\`='1419722669',\`ip\`=X'caa29457',\`location\`='/install/upgrade.php?', \`useragent\`='Mozilla/5.0 (X11; Linux i686) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.',\`location1\`='0',\`location2\`='0', \`nopermission\`='0'

![MyBB upgrade error](/assets/img/mybb-upgrade-error.jpg)

I don't know how to fix this so the version is still 1.6.16.
