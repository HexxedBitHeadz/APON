https://www.opensourcecms.com/ovidentia/
http://10.11.1.73:8080/php/index.php?tg=login&cmd=authform&msg=Login&err=
-   Username: admin@admin.bab
-   Password: 012345678
Go to "Sites" on the left side, click on the only site name available, then click "File upload configuration".
Change the upload path to:  `C:\wamp\www\MYuploads`
Click "Record".
Go to "File Manager" on the left side.  Make a new folder.
Click on the "Rights" link.
Add "Ovidentia users" to Upload.
Now we should see "File Manager" on the right side.  Click on the folder created earlier, then click the "upload" tab at the top.
[[0._PHP Webshells#wwolf]]
Upload your php file.
To find out where the upload goes, go back to "Sites" > "File upload configuration" and change the upload path to anything else.
Revisit "File manager" on the right side, and click on your folder.  You will receive an error in red, giving you the path.  Now just visit:
`http://10.11.1.73:8080/MYuploads/fileManager/collectives/DG0/webshell/webshell.php`