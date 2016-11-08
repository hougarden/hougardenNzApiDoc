**1. Calling API with 'username' and 'password' to get token.**

**Sample PHP code:**
```php
<?php
$userLogin = "http://test3.hougarden.com/api/v1/token/self";
$params = [
    "username" => "xxxxxxxxxxx",
    "password" => "xxxxxx"
];
$session = curl_init($userLogin);
curl_setopt($session, CURLOPT_POST, true);
curl_setopt($session, CURLOPT_POSTFIELDS, $params);
curl_setopt($session, CURLOPT_HEADER, false);
curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
$response = json_decode(curl_exec($session), true);
curl_close($session);
$token = $response['token'];
```
>sample response:
```json
{"token":"eyJhbGciOiJSUzI1NiJ9.eyJ1c2VybmFtZSI6IjEwMTc2TFDC112OTc2Mjk2MjM3OSIsInRva2VuX2hhc2giOiJlODgzZjEwZjNlNDc3NjY5OTBiYTY1MDFjODAyZjc4YiIsImV4cCI6MTQ3ODY0NTY4MiwiaWF0IjoxNDc4NjQyMDgyfQ.ZZ8RiOYj7gvCdJP3t9CHe6nS_M0yL8_JUSmB3T5V2smhkk9-JFpQma4ndY64Hjuz9eR9rvd-JhnAAwGgB4l__n8-prsHg6TSRSLbNpm5_i6WXGR2lr5T062lmwIXG2t7kjMQupYXZa89xMCAtpbiAyKwouMqcEEFyeSUYJhV0YHGq3LSVzmNdLPEVlJc13KrntYfeIeJLkzHCaOUMLmKvzPDQwcRmv4MAHPIbsOo_gpRKM94jrTPOfr-1WlXIlVj9ruU8zs18Z8kcAwFqls_Gi-Wbsp16KYW5ssdIgR91123F0fECqQ41IykFiiyD7WFXubAdS_Bocl638gnYM3IYRfu11eB7GhEYDpfREsBoKh9bsUgYgG-npOr2IaFChIH4BBfWGwEyrsPwiXWoWVVAane0fELeVdYWLaUM_Y-GyfkqJXDIEBR5dqdlo0GvZUcNxOQcjiuIm_KUpqimsNKhDvr6zhM1He1RV7gX1wYBrOOYmXcy1go_MUjcpHqiNEehh0_dYoMPPpFc0K7k5lA98A7KNGFnb6c38z6rnlnuZkI3VTXBdEo4h0p2W258EDF6Wo3Vg0Yx-AXtD9eg83mpHqLu7DIy0UomT6PdoFePs7y4k43w6rvj_sDM9nFwY9xIDMAoyieCzsqZPGcVhDaem8DOl1Q9vFZ27kkRXQZP3Q","refreshToken":"b30d6bbdacdcbc5467f61ca4cb38376584f70f50fd765b2c74404afe16b6a92214925af26002742ab1c6e232adedf58350493b1422e93a680aaa30a253d3b051"}
```

**2.Add 'token' into Http Headers and post json listing data to data receiver API. It will return a 201 response if success.**

**Sample PHP code:**
```php
$url =  "http://test3.hougarden.com/api/v1/data-receiver";
$headers = [
    "Content-Type: application/json",
    "Authorization: User ".$token,
];
$listing = [
    'uniqueID' => 'HG90890-123',
    'headline' => 'A Masterpiece of fine living',
    // more fields to be added
];

$session = curl_init();
curl_setopt($session, CURLOPT_URL, $url);
curl_setopt($session, CURLOPT_POST, true);
curl_setopt($session, CURLOPT_POSTFIELDS, json_encode($listing));
curl_setopt($session, CURLOPT_HEADER, true);
curl_setopt($session, CURLOPT_HTTPHEADER, $headers);
curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($session);
curl_close($session);
```
