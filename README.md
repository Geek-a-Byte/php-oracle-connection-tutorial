# php-oracle-connection-tutorial
## this tutorial is only applicable for oracle 19c

## ``step 0: download oracle 19c and sql developer``
- assuming you have Windows x64 (64-bit).
- [ ] https://www.oracle.com/database/technologies/oracle19c-windows-downloads.html
- [ ] https://www.youtube.com/watch?v=GUpvXMHqe2U&ab_channel=GeekyScript
- [ ] https://www.oracle.com/database/sqldeveloper/technologies/download/

## ``step 1: Setup Xampp``

- [ ] install xampp for PHP 8.0.28 / PHP 8.0.28 from [here](https://www.apachefriends.org/download.html) (download 64 bit).
- [ ] start the apache server. if no error shows, then go to this url: "http://localhost:80/dashboard/"
- [ ] if error showed: ``Apache shutdown unexpectedly. This may be due to a blocked port, missing dependencies...`` then press the config button right after the apache button, click on the "Apache (httpd.conf)" option, ctrl+F (search) for Listen 80 in that file, replace 80 with 8085. 
- [ ] restart the apache server. if no error shows, then go to this url: "http://localhost:8085/dashboard/"
- [ ] if error showed: ``Port 443 in use by ""C:\Program Files (x86)\VMware\VMware Workstation\vmware-hostd.exe" -u "C:\ProgramData\VMware\hostd\config.xml"" with PID 6360!`` then press the config button right after the apache button, click on the "Apache (httpd-ssl.conf)" option, ctrl+F (search) for Listen 443 in that file, replace 443 with 4430. see [here](https://stackoverflow.com/questions/21182512/how-to-stop-vmware-port-error-of-443-on-xampp-control-panel-v3-2-1)
- [ ] restart the apache server. if no error shows, then go to this url: "http://localhost:8085/dashboard/"

## ``step 2: Install Instantclient-basic-nt-12.1.0.2.0``

- [ ] go to this url: https://www.oracle.com/database/technologies/instant-client/microsoft-windows-32-downloads.html
- [ ] and select this one to install (remember that the version is important.)
![image](https://github.com/Geek-a-Byte/php-oracle-connection-tutorial/assets/59027621/b5de9dcb-4d8c-404e-93f5-f7709f0b8739)
- [ ] extract the downloaded file and copy and paste the extracted folder in the C drive. 
- [ ] now my Xampp php is in location (default): "C:\xampp\php"
- [ ] and my instantClient is in location: "C:\instantclient_12_1"
- [ ] now go to edit the environment system variables option.
- [ ] add this two path under system variable Path:
 ![image](https://github.com/Geek-a-Byte/php-oracle-connection-tutorial/assets/59027621/4d6c414a-7d20-4b83-92a0-41150160ec87)

## ``step 3: Download php_oci8.dll and php_oci8_11g.dll``

- [ ] Download php_oci8.dll and php_oci8_11g.dll from [here](https://www.dll-files.com/php_oci8.dll.html) and [here](https://www.dll-files.com/php_oci8_11g.dll.html).
- [ ] Copy and paste the php_oci8.dll and php_oci8_11g.dll in C:\xampp\apache\bin and C:\xampp\php\ext
- [ ] now go to xampp, press config right after the apache option and select php.ini file
- [ ] add these two lines: extension=php_oci8.dll  extension=php_oci8_11g.dll
![Screenshot 2023-05-28 224500](https://github.com/Geek-a-Byte/php-oracle-connection-tutorial/assets/59027621/4d692fdc-08b5-42e9-ac6c-96ddb2229b96)
- [ ] Make sure in the php.ini file the extension_dir =”C:\xampp\php\ext”.

