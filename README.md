```json
{
    uniqueID: "HG90890-123",
    status: "current",
    type: "commercial",
    category: "House",
    authority: "auction",
    headline: "A Masterpiece of fine living",
    description: "A fuller description of this listing. May include unix-style newlines like that. Limited HTML and Markdown permitted.",
    auctionDate: "2003-12-04T18:30",
    tenderDate: "2003-12-04T18:30",
    bathrooms: 2,
    bedrooms: 3,
    carSpaces: 1,
    yearBuilt: "1980's",
    newConstruction: 1,
    publishAddress: 1,
    balcony: 1,
    externalLink: "http://www.realestate.com.au/onlinetours/VictoriaSt.tour",
    videoLink: "http://www.realestate.com.au/videos/VictoriaSt.avi",
    availabilityLink: "http://www.realestate.com.au/holidayavailability/property123cal.html",
    listingType: "sale",
    propertyExtent: "whole",
    area: 750,
    floorArea: 500,
    price: 500000,
    searchPrice: 450000,
    priceView: "Buyers above $700,000's",
    soldDate: "2005-03-03",
    soldPrice: 600000,
    createdDate: "2009-12-18",
    updatedDate: "2009-12-18",
    listingDate: "2010-01-01",
    statusChangeDate: "2010-03-31",
    images: [
        "http://realestate.com.au/picsatrea01.jpg",
        "http://realestate.com.au/picsatrea02.jpg",
        "http://realestate.com.au/picsatrea03.jpg"
    ],
    position: [
        175.389,
        -36.21
    ],
    address: {
        lotNumber: "12",
        streetNumber: "2/102",
        subNumber: "Unit 2",
        site: "Victoria Gardens Shopping Complex",
        street: "Franklin Road",
        suburb: "Greenland",
        district: "Auckland City",
        region: "Auckland",
        postcode: "3000"
    },
    allowances: {
        petFriendly: 1,
        furnished: 0,
        smokers: 0
    },
    openHomes: [
        {
            timeStart: "2010-10-12T01:30",
            timeEnd: "2010-10-12T03:30"
        }
    ]
}
```
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


$url =  "http://test3.hougarden.com/api/v1/data-receiver";
$headers = [
    "Content-Type: application/json",
    "Authorization: User ".$token,
];
$params = ['nanan' => 1];

$session = curl_init();
curl_setopt($session, CURLOPT_URL, $url);
curl_setopt($session, CURLOPT_POST, true);
curl_setopt($session, CURLOPT_POSTFIELDS, json_encode($params));
curl_setopt($session, CURLOPT_HEADER, true);
curl_setopt($session, CURLOPT_HTTPHEADER, $headers);
curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($session);
curl_close($session);
var_dump($response);
```