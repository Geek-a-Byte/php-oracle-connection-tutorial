# php-oracle-connection-tutorial

## ``step 1: Setup Xampp``

- [ ] install xampp for PHP 8.0.28 / PHP 8.0.28 from [here](https://www.apachefriends.org/download.html) (download 64 bit).
- [ ] start the apache server. if no error shows, then go to this url: "http://localhost:80/dashboard/"
- [ ] if error showed: ``Apache shutdown unexpectedly. This may be due to a blocked port, missing dependencies...`` then press the config button right after the apache button, click on the "Apache (httpd.conf)" option, ctrl+F (search) for Listen 80 in that file, replace 80 with 8085. 
- [ ] restart the apache server. if no error shows, then go to this url: "http://localhost:8085/dashboard/"
- [ ] if error showed: ``Port 443 in use by ""C:\Program Files (x86)\VMware\VMware Workstation\vmware-hostd.exe" -u "C:\ProgramData\VMware\hostd\config.xml"" with PID 6360!`` then press the config button right after the apache button, click on the "Apache (httpd-ssl.conf)" option, ctrl+F (search) for Listen 443 in that file, replace 443 with 4430
- [ ] restart the apache server. if no error shows, then go to this url: "http://localhost:8085/dashboard/"
