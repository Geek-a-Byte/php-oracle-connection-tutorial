# php-oracle-connection-tutorial
## this tutorial is only applicable for oracle 19c
follow this mainly: https://www.youtube.com/watch?v=tXoszm_v5NA&t=1s&ab_channel=techiezero

## ``step 0: download oracle 19c and sql developer``
- assuming you have Windows x64 (64-bit).
- [ ] https://www.oracle.com/database/technologies/oracle19c-windows-downloads.html
- [ ] https://www.oracle.com/database/sqldeveloper/technologies/download/
- [ ] https://www.youtube.com/watch?v=GUpvXMHqe2U&ab_channel=GeekyScript
- [ ] if you need reinstall oracle all over again, make sure to uninstall the previous version correctly, follow this: http://www.rebellionrider.com/how-to-uninstall-oracle-database-19c/

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

## ``step 3: Download oci8 3.2.1 for Windows``

- [ ] Download dll files (the thread safe one for x86) for oci from [here](https://pecl.php.net/package/oci8/3.2.1/windows)
![image](https://github.com/Geek-a-Byte/php-oracle-connection-tutorial/assets/59027621/b46b8294-2634-48a5-9cef-537b6b7d8839)
- [ ] Copy and paste the extracted files in C:\xampp\apache\bin and C:\xampp\php\ext
![image](https://github.com/Geek-a-Byte/php-oracle-connection-tutorial/assets/59027621/436920f2-d6e9-4281-9033-7688786be669)
- [ ] now go to xampp, press config right after the apache option and select php.ini file
- [ ] remove ; before "extension=oci8_19  ; Use with Oracle Database 19 Instant Client"
- [ ] Make sure in the php.ini file the extension_dir ="C:\xampp\php\ext".

## ``step 4: create new user for oracle db``

- [ ] open sql developer
- [ ] first alter session
```sql

alter session set "_ORACLE_SCRIPT"=true;

```

- [ ] create a new user 

```sql

CREATE USER obama identified by obama;

```

- [ ] see if the user is created or not
```sql

SELECT * FROM dba_users WHERE username='OBAMA';

```

## ``Grant all privileges to obama``

```sql

grant all privileges to obama

```

## ``Step 5: test with oracle``

- [ ] now go to the htdocs folder in this location: "C:\xampp\htdocs"
- [ ] create a connection.php file 
- [ ] and paste this snippet:

```PHP

<?php

error_reporting(E_ALL);
ini_set('display_errors', 'On');

$username = "OBAMA";                  // Use your username
$password = "obama";             // and your password
$database = "localhost/xe";   // and the connect string to connect to your database

$query = "select * from dual";

$c = oci_connect($username, $password, $database);
if (!$c) {
    $m = oci_error();
    trigger_error('Could not connect to database: '. $m['message'], E_USER_ERROR);
}

$s = oci_parse($c, $query);
if (!$s) {
    $m = oci_error($c);
    trigger_error('Could not parse statement: '. $m['message'], E_USER_ERROR);
}
$r = oci_execute($s);
if (!$r) {
    $m = oci_error($s);
    trigger_error('Could not execute statement: '. $m['message'], E_USER_ERROR);
}

echo "<table border='1'>\n";
$ncols = oci_num_fields($s);
echo "<tr>\n";
for ($i = 1; $i <= $ncols; ++$i) {
    $colname = oci_field_name($s, $i);
    echo "  <th><b>".htmlspecialchars($colname,ENT_QUOTES|ENT_SUBSTITUTE)."</b></th>\n";
}
echo "</tr>\n";

while (($row = oci_fetch_array($s, OCI_ASSOC+OCI_RETURN_NULLS)) != false) {
    echo "<tr>\n";
    foreach ($row as $item) {
        echo "<td>";
        echo $item!==null?htmlspecialchars($item, ENT_QUOTES|ENT_SUBSTITUTE):"&nbsp;";
        echo "</td>\n";
    }
    echo "</tr>\n";
}
echo "</table>\n";


```
