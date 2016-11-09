**1. Calling API with 'username' and 'password' to get token.**

>sample PHP code:
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
{
"token":"eyJhbGciOiJSUzI1NiJ9.eyJ1c2VybmFtZSI6IjEwMTc2TFDC112OTc2Mjk2MjM3OSIsInRva2VuX2hhc2giOiJlODgzZjEwZjNlNDc3NjY5OTBiYTY1MDFjODAyZjc4YiIsImV4cCI6MTQ3ODY0NTY4MiwiaWF0IjoxNDc4NjQyMDgyfQ.ZZ8RiOYj7gvCdJP3t9CHe6nS_M0yL8_JUSmB3T5V2smhkk9-JFpQma4ndY64Hjuz9eR9rvd-JhnAAwGgB4l__n8-prsHg6TSRSLbNpm5_i6WXGR2lr5T062lmwIXG2t7kjMQupYXZa89xMCAtpbiAyKwouMqcEEFyeSUYJhV0YHGq3LSVzmNdLPEVlJc13KrntYfeIeJLkzHCaOUMLmKvzPDQwcRmv4MAHPIbsOo_gpRKM94jrTPOfr-1WlXIlVj9ruU8zs18Z8kcAwFqls_Gi-Wbsp16KYW5ssdIgR91123F0fECqQ41IykFiiyD7WFXubAdS_Bocl638gnYM3IYRfu11eB7GhEYDpfREsBoKh9bsUgYgG-npOr2IaFChIH4BBfWGwEyrsPwiXWoWVVAane0fELeVdYWLaUM_Y-GyfkqJXDIEBR5dqdlo0GvZUcNxOQcjiuIm_KUpqimsNKhDvr6zhM1He1RV7gX1wYBrOOYmXcy1go_MUjcpHqiNEehh0_dYoMPPpFc0K7k5lA98A7KNGFnb6c38z6rnlnuZkI3VTXBdEo4h0p2W258EDF6Wo3Vg0Yx-AXtD9eg83mpHqLu7DIy0UomT6PdoFePs7y4k43w6rvj_sDM9nFwY9xIDMAoyieCzsqZPGcVhDaem8DOl1Q9vFZ27kkRXQZP3Q",
"refreshToken":"b30d6bbdacdcbc5467f61ca4cb38376584f70f50fd765b2c74404afe16b6a92214925af26002742ab1c6e232adedf58350493b1422e93a680aaa30a253d3b051"
}
```


**2. Add 'token' into Http Headers and post json listing data to data receiver API. It will return a 201 response if success.**

>sample PHP code:
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


**3. Sample listing json data structure:**

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
        },
        {
            timeStart: "2010-10-13T01:30",
            timeEnd: "2010-10-13T03:30"
        }
    ],
    agents: [
        {
            code: "BFT_1234",
            title: "Mr",
            first_name: "Glen",
            last_name: "Barnes",
            bio: "Allow myself to introduce myself...",
            phone_numbers: {
                office_ddi: "+64 (9) 555-1212",
                mobile: "+64 (21) 555-1212",
                after_hours: "+64 (21) 555-1212",
                fax: "+64 (9) 0800-123456"
            },
            addresses: {
                postal: {
                    address: "PO Box 1234, Private Bag, Freemans Bay",
                    city: "Auckland",
                    postcode: "1011"
                },
                street: {
                    address: "Level 2, 11 Franklin Road, Freemans Bay",
                    city: "Auckland",
                    postcode: "1011"
                }
            },
            links: {
                website: "steve.tinyhomes.co.nz",
                blog: "voices.realestate.co.nz/tinysteve",
                linked_in: "www.linkedin.com/in/tinysteve",
                google_profile: "www.google.com/profiles/tinysteve",
                twitter: "tinyhomes",
                facebook_profile: "www.facebook.com/profile.php?id=666111666"
            },
            image: "http://realestate.com.au/picsatrea01.jpg"
        },
        {
        code: "Gray",
        title: "Mr",
        first_name: "Glen",
        last_name: "Barnes",
        bio: "Allow myself to introduce myself...",
        phone_numbers: {
        office_ddi: "+64 (9) 555-1212",
        mobile: "+64 (21) 555-1212",
        after_hours: "+64 (21) 555-1212",
        fax: "+64 (9) 0800-123456"
        },
        addresses: {
        postal: {
        address: "PO Box 1234, Private Bag, Freemans Bay",
        city: "Auckland",
        postcode: "1011"
        },
        street: {
        address: "Level 2, 11 Franklin Road, Freemans Bay",
        city: "Auckland",
        postcode: "1011"
        }
        },
        links: {
        website: "steve.tinyhomes.co.nz",
        blog: "voices.realestate.co.nz/tinysteve",
        linked_in: "www.linkedin.com/in/tinysteve",
        google_profile: "www.google.com/profiles/tinysteve",
        twitter: "tinyhomes",
        facebook_profile: "www.facebook.com/profile.php?id=666111666"
        },
        image: "http://realestate.com.au/picsatrea01.jpg"
        }
    ],
    office: {
        code: "8821-0",
        name: "Marks Realty Ltd (Licensed: REAA 2008) - Unprofessionals, Inangahua Junction",
        image: "http://realestate.com.au/picsatrea01.jpg",
        website: "www.unproinj.co.nz",
        phone_numbers: {
            phone: "03 123 4529",
            fax: "03 245 9193"
        },
        addresses: {
            postal: {
            address: "P O Box 1",
            city: "Inangahua Junction",
            postcode: "9840"
            },
            street: {
            address: "2 High Street",
            city: "Inangahua Junction",
            postcode: ""
            }
        }
    }
}
```


**4. Data fields:**

| Parameter | Data Type | Description |
| ------| ------ | ------ |
| uniqueID | String Required | Information supplied to uniquely identify a property. The value must be unique representing different properties. |
| status | String Required | current, withdrawn, offmarket, sold, leased |
| type | String Required | House, Unit, Townhouse, Apartment, Flat ... |
| category | String Required | House, Unit, Townhouse, Apartment, Flat ... |
| authority | String Required | auction, exclusive, multilist, conjunctional, open, sale, setsale, eoi, forsale, offers, tender |
| headline | String Required | A Masterpiece of fine living |
| description | String | The description of the property, able to include multiple paragraphs of text. This field is for plain text only. |
| auctionDate | String | Timestamp UTC |
| tenderDate | String | Timestamp UTC |
| bathrooms | Integer |  |
| bedrooms | Integer |  |
| carSpaces | Integer | carSpaces or carports or garages |
| yearBuilt | String | year of construction |
| newConstruction | Integer | 1, 0 Specifies if the listed property is a new construction or an established property. |
| publishAddress | Integer | 1, 0 Specifies if the location of the property is shown. |
| balcony | Integer | 1, 0 Indicates whether the property has a balcony. |
| externalLink | String | Properties may have links to other material such as 360 degree views or virtual tours. |
| videoLink | String | Properties may have links to a video display of the listing. |
| availabilityLink | String | Holiday rental properties may have links to an external URI source of availability - generally in the form of an online calendar. |
| listingType | String Required | sale, lease, both |
| propertyExtent | String | whole, part This field refers to the section of the building that is for lease. Is the whole building for lease or only a part - if none received - default to not applicable. |
| area | Integer | Represents a measurement of area being offered for sale / lease. |
| floorArea | Integer | Represents a measurement of living area being offered for sale / lease. |
| price | Integer |  |
| searchPrice | Integer | Price for searching reference |
| priceView | String | A human-readable string displayed to describe the price of the property. |
| soldDate | String | soldDate indicates the date the property was sold. |
| soldPrice | Integer | The price for which the property was sold. |
| createdDate | String |  |
| updatedDate | String |  |
| listingDate | String |  |
| statusChangeDate | String |  |
| position | Float | Coordinates of the property |
| lotNumber | String | The prefix to the streetNumber of the listing. |
| streetNumber | String | The number of the property on the street, not including the street name itself. |
| subNumber | String | The prefix to the streetNumber or lotNumber of the listing. |
| site | String | Display the name or site of the commercial listing |
| street | String Required |  |
| suburb | String Required | The name of the suburb or town where the property is physically located. |
| district | String Required |  |
| region | String Required | Auckland, Bay Of Plenty, Canterbury, Coromandel ... |
| postcode | String |  |
| petFriendly | Integer | 1, 0 Specifies if pets are allowed in the listed property or not. |
| furnished | Integer | 1, 0 Specifies if the listed property is furnished or not. |
| smokers | Integer | 1, 0 Specifies if smokers are welcome in the listed property or not. |
| timeStart | String | Timestamp UTC |
| timeEnd | String | Timestamp UTC |


##More 

**1. For status, type, category, authority, suburb, district and region fields, you can either post String data or Integer Id with related information**

**2. API url, username, password may change in the future**

**3. A single token will be expired within 1 hour, but you can retrive another token by using the refresh token.**

>sample PHP code:
```php
<?php
$refreshTokenUrl = "http://test3.hougarden.com/api/v1/token/refresh";
$params = [
    "refreshToken" => "b30d6bbdacdcbc5467f61ca4cb38376584f70f50fd765b2c74404afe16b6a92214925af26002742ab1c6e232adedf58350493b1422e93a680aaa30a253d3b051"
];
$session = curl_init(refreshTokenUrl);
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
{
"token":"eyJhbGciOiJSUzI1NiJ9.eyJ1c2VybmFtZSI6IjEwMTc2TFDC112OTc2Mjk2MjM3OSIsInRva2VuX2hhc2giOiJlODgzZjEwZjNlNDc3NjY5OTBiYTY1MDFjODAyZjc4YiIsImV4cCI6MTQ3ODY0NTY4MiwiaWF0IjoxNDc4NjQyMDgyfQ.ZZ8RiOYj7gvCdJP3t9CHe6nS_M0yL8_JUSmB3T5V2smhkk9-JFpQma4ndY64Hjuz9eR9rvd-JhnAAwGgB4l__n8-prsHg6TSRSLbNpm5_i6WXGR2lr5T062lmwIXG2t7kjMQupYXZa89xMCAtpbiAyKwouMqcEEFyeSUYJhV0YHGq3LSVzmNdLPEVlJc13KrntYfeIeJLkzHCaOUMLmKvzPDQwcRmv4MAHPIbsOo_gpRKM94jrTPOfr-1WlXIlVj9ruU8zs18Z8kcAwFqls_Gi-Wbsp16KYW5ssdIgR91123F0fECqQ41IykFiiyD7WFXubAdS_Bocl638gnYM3IYRfu11eB7GhEYDpfREsBoKh9bsUgYgG-npOr2IaFChIH4BBfWGwEyrsPwiXWoWVVAane0fELeVdYWLaUM_Y-GyfkqJXDIEBR5dqdlo0GvZUcNxOQcjiuIm_KUpqimsNKhDvr6zhM1He1RV7gX1wYBrOOYmXcy1go_MUjcpHqiNEehh0_dYoMPPpFc0K7k5lA98A7KNGFnb6c38z6rnlnuZkI3VTXBdEo4h0p2W258EDF6Wo3Vg0Yx-AXtD9eg83mpHqLu7DIy0UomT6PdoFePs7y4k43w6rvj_sDM9nFwY9xIDMAoyieCzsqZPGcVhDaem8DOl1Q9vFZ27kkRXQZP3Q",
"refreshToken":"b30d6bbdacdcbc5467f61ca4cb38376584f70f50fd765b2c74404afe16b6a92214925af26002742ab1c6e232adedf58350493b1422e93a680aaa30a253d3b051"
}
```
