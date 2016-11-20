
```php
<?php
$file = '/tmp/test.xml';
$remote_file = 'data/test.xml';

$ftp_server = "ftp9.hougarden.com";
$ftp_port = 5100;
$ftp_user_name = "xxxxx";
$ftp_user_pass = "xxxxxxx";

$conn_id = ftp_connect($ftp_server, $ftp_port);
$login_result = ftp_login($conn_id, $ftp_user_name, $ftp_user_pass);
ftp_pasv($conn_id, true);

if (ftp_put($conn_id, $remote_file, $file, FTP_ASCII)) {
 echo "successfully uploaded $file\n";
} else {
 echo "There was a problem while uploading $file\n";
}

ftp_close($conn_id);

```

