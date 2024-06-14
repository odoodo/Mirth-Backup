Creates a backup of a mirth configuration

<h1>Code Template: Automatic Mirth Backup</h1>
<b>Purpose:</b><br/>
<b>This code template creates a backup of a mirth configuration like if you click "backup config" in the settings tab of the mirth administrator and stores it in the filesystem.</b><br/>
<br/>
It backs up the whole mirth configuration and also the configuration map. Everything is compressed into a zip archive and can optionally be secured with 256bit AES encryption.<br/>
<br/>
<b>Parameters:</b><br/>
<ul>
  <li><b>username</b><br/>
The username that the channel should use to connect to the server that should be backed-up. Dedicated user is recommended.</li>
  <li><b>password</b><br/>
The password that the channel should use to connect to the server that should be backed-up.
  <li><b>server</b><br/>
The ip or name of the mirth server that should be backed-up. It can also contain a custom port (default is 8443). This parameter will become part of the backup name.</li>
  <li><b>backupFolder</b><br/>
Path to the folder where the backup should be created. None-existing parts of the path will be created. Further, all backups of the same day will be placed in a dedicated subfolder.</li>
  <li><b>archivePassword</b><br/>
If a password is set, the resulting archive will be secured by 256bit AES encryption (Optional)</li>
</ul>

<b>Examples:</b><br/>
Create a backup archive without encryption:
```js
backupMirthServer('admin', 'admin', 'MyMirthProdInstance', 'c:\temp');
```
Create a 256bit AES encrypted backup archive:
```js
backupMirthServer('admin', 'admin', 'MyMirthProdInstance', 'c:\temp', 'MySecurePassword!');
```

<b>Configuration:</b>
1. Place the zip4J library in the custom-lib folder of mirth. (It is needed for zip encryption - further info can be found on the website)
2. Press the button "Reload Resources" under Settings -> Resources in Mirth Administrator
3. Import the attached code templates

<h1>Code Template: Cleanup Directory</h1>
<b>Purpose:</b><br/>
Intelligently remove outdated backups from your backup folder to avoid exceeding the capacity of the backup drive.

This function should be called in the backup channel after all Mirth servers have been backuped.

<b>Parameters:</b><br/>
<ul>
<li><b>path</b><br/>
The path to the directory that should be cleaned up. (This usually is the path of the backup folder)</li>
<li><b>maxFileAge</b><br/>
Subdirectories that are older than the here specified number of days (1st day is today) will be deleted if number of resulting directories is not below the minimum specified by minNumberOfBackups</li>
<li><b>minNumberOfBackups</b><br/>
The minimum number of backups that should be kept even if the maximum file age is exceeded (optional)</li>
</ul>

<b>Examples:</b><br/>
Remove all backups that are older than 40 days:
```js
cleanupDirectory('c:\temp', 40);
```
Remove all backups that are older than 20 days but retain at least the 10 last backups:
```js
cleanupDirectory('c:\temp', 20, 10);
```

