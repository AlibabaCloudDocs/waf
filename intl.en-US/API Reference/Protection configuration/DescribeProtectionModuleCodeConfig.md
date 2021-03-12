# DescribeProtectionModuleCodeConfig

Queries the codes of regions that can be configured in a region-based IP address blacklist. These codes include the codes of administrative regions in China and the codes of countries and areas.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=waf-openapi&api=DescribeProtectionModuleCodeConfig&type=RPC&version=2019-09-10)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeProtectionModuleCodeConfig|The operation that you want to perform. Set the value to **DescribeProtectionModuleCodeConfig**. |
|CodeType|Integer|Yes|14|The type of code that you want to query. Set the value to **14**, which indicates the codes of regions that can be configured in a region-level IP address blacklist of WAF. |
|InstanceId|String|Yes|waf-cn-zz11sr5\*\*\*\*|The ID of the WAF instance.

 **Note:** You can call the [DescribeInstanceInfo](~~140857~~) operation to query the ID of the WAF instance. |
|CodeValue|Integer|No|0|The type of region code that you want to query. Valid values:

 -   **0**: codes of administrative regions in China
-   **1**: codes of countries and areas

 **Note:** If you do not specify this parameter, both types of regions are queried. |
|ResourceGroupId|String|No|rg-acfm2pz25js\*\*\*\*|The ID of the resource group to which the WAF instance belongs in Resource Management. This parameter is empty by default, which indicates that the WAF instance belongs to the default resource group.

 For more information about resource groups, see [Create a resource group](~~94485~~). |

All Alibaba Cloud API operations must include common request parameters. For more information about common request parameters, see [Common parameters](~~162719~~).

For more information about sample requests, see the **"Examples"** section of this topic.

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CodeConfigs|String|\[\{"code":0,"name":"310000,530000,150000,110000,TW\_01,220000,510000,120000,640000,340000,370000,140000,440000,450000,650000,320000,360000,130000,410000,330000,460000,420000,430000,MO\_01,620000,350000,540000,520000,210000,500000,610000,630000,HK\_01,230000","env":"online"\}\]|The code configurations. This parameter is a string consisting of JSON arrays. Each element in a JSON array is a JSON struct that represents a region code of one type and includes the following fields:

 -   **code**: the type of region code. Data type: integer. Valid values: **0** and **1**. The value 0 indicates the codes of administrative regions in China. The value 1 indicates the codes of countries and areas.
-   **name**: the configured region codes that belong to the specified type. Data type: string. Multiple region codes are separated with commas \(,\). For more information about region codes, see the descriptions that follows the **Response parameters** section. |
|RequestId|String|64D24280-1AD9-4D41-8844-872168E59BF3|The ID of the request. |

**Codes of administrative regions in China**

```

{
  "310000": "Shanghai",
  "610000": "Shaanxi",
  "360000": "Jiangxi",
  "230000": "Heilongjiang"
  "530000": "Yunnan",
  "140000": "Shanxi",
  "440000": "Guangdong",
  "320000": "Jiangsu",
  "110000": "Beijing",
  "MO_01": "Macau (China)",
  "620000": "Gansu",
  "370000": "Shandong",
  "150000": "Nei Mongol",
  "450000": "Guangxi",
  "410000": "Henan",
  "500000": "Chongqing",
  "120000": "Tianjin",
  "630000": "Qinghai",
  "460000": "Hainan",
  "640000": "Ningxia",
  "330000": "Zhejiang",
  "HK_01": "Hong Kong (China)",
  "420000": "Hubei",
  "430000": "Hunan",
  "130000": "Hebei",
  "510000": "Sichuan",
  "350000": "Fujian",
  "210000": "Liaoning",
  "220000": "Jilin",
  "340000": "Anhui",
  "520000": "Guizhou",
  "TW_01": "Taiwan (China)"
}

```

Codes of countries and areas

```

{
  "KE": "Kenya",
  "KG": "Kyrgyzstan",
  "KH": "Kampuchea",
  "KI": "Kiribati",
  "KM": "Comoros",
  "KN": "Saint Kitts and Nevis",
  "KP": "North Korea",
  "KR": "South Korea",
  "KW": "Kuwait",
  "KY": "Cayman Islands",
  "KZ": "Kazakhstan",
  "LA": "Laos",
  "LB": "Lebanon",
  "LC": "Saint Lucia",
  "LI": "Liechtenstein",
  "LK": "Sri Lanka",
  "LR": "Liberia",
  "LS": "Lesotho",
  "LT": "Lithuania",
  "LU": "Luxembourg",
  "LV": "Latvia",
  "LY": "Libya",
  "MA": "Morocco",
  "MC": "Monaco",
  "MD": "Moldova",
  "ME": "Montenegro",
  "MF": "Saint Martin",
  "MG": "Madagascar",
  "MH": "Marshall Islands",
  "MK": "Macedonia",
  "ML": "Mali",
  "MM": "Myanmar",
  "MN": "Mongolia",
  "MO": "Macau (China)",
  "MP": "Northern Mariana Islands",
  "MQ": "Martinique",
  "MR": "Mauritania",
  "MS": "Montserrat",
  "MT": "Malta",
  "MU": "Mauritius",
  "MV": "Maldives",
  "MW": "Malawi",
  "MX": "Mexico",
  "MY": "Malaysia",
  "MZ": "Mozambique",
  "NA": "Namibia",
  "NC": "New Caledonia",
  "NE": "Niger",
  "NF": "Norfolk Island",
  "NG": "Nigeria",
  "NI": "Nicaragua",
  "NL": "Netherlands",
  "NO": "Norway",
  "O1": "Other countries",
  "NP": "Nepal",
  "NR": "Nauru",
  "NU": "Niue",
  "NZ": "New Zealand",
  "GA": "Gabon",
  "GB": "United Kingdom",
  "WS": "Samoa",
  "GD": "Grenada",
  "GE": "Georgia",
  "GF": "French Guiana",
  "GG": "Guernsey",
  "GH": "Ghana",
  "GI": "Gibraltar",
  "GL": "Greenland",
  "GM": "The Gambia,
  "GN": "Guinea",
  "GP": "Guadeloupe",
  "GQ": "Equatorial Guinea",
  "GR": "Greece",
  "GS": "South Georgia and the South Sandwich Islands",
  "GT": "Guatemala",
  "GU": "Guam",
  "GW": "Guinea-Bissau",
  "GY": "Guyana",
  "HK": "Hong Kong (China)",
  "HM": "Heard Island and McDonald Islands",
  "HN": "Honduras",
  "HR": "Croatia",
  "HT": "Haiti",
  "YE": "Yemen",
  "HU": "Hungary",
  "YT": "Mayotte",
  "ID": "Indonesia",
  "IE": "Ireland",
  "IL": "Israel",
  "IM": "Isle of Man",
  "IN": "India",
  "IO": "British Indian Ocean Territory",
  "ZA": "South Africa",
  "IQ": "Iraq",
  "IR": "Iran",
  "IS": "Iceland",
  "IT": "Italy",
  "ZM": "Zambia",
  "JE": "Jersey",
  "ZW": "Zimbabwe",
  "JM": "Jamaica",
  "JO": "Jordan",
  "JP": "Japan",
  "SI": "Slovenia",
  "SJ": "Svalbard and Jan Mayen Islands",
  "BY": "Belarus",
  "SK": "Slovakia",
  "BZ": "Belize",
  "SL": "Sierra Leone",
  "SM": "San Marino",
  "SN": "Senegal",
  "SO": "Somalia",
  "CA": "Canada",
  "SR": "Suriname",
  "SS": "South Sudan",
  "CC": "Cocos (Keeling) Islands",
  "ST": "Sao Tome and Principe",
  "CD": "Democratic Republic of the Congo",
  "CF": "Central African Republic",
  "SV": "El Salvador",
  "CG": "Republic of the Congo",
  "CH": "Switzerland",
  "SX": "Sint Maarten",
  "SY": "Syrian Arab Republic",
  "CI": "Côte d'Ivoire",
  "SZ": "Eswatini",
  "CK": "Cook Islands",
  "CL": "Chile",
  "CM": "Cameroon",
  "CN": "China",
  "CO": "Colombia",
  "TC": "Turks and Caicos Islands",
  "CR": "Costa Rica",
  "TD": "Chad",
  "CU": "Cuba",
  "TF": "French Southern and Antarctic Lands",
  "CV": "Cabo Verde",
  "TG": "Togo",
  "CW": "Curacao",
  "TH": "Thailand",
  "CX": "Christmas Island",
  "TJ": "Tajikistan",
  "CY": "Cyprus",
  "CZ": "Czech Republic",
  "TK": "Tokelau",
  "TL": "East Timor",
  "TM": "Turkmenistan",
  "TN": "Tunisia",
  "TO": "Tonga",
  "TR": "Turkey",
  "TT": "Trinidad and Tobago",
  "DE": "Germany",
  "TV": "Tuvalu",
  "TW": "Taiwan (China)",
  "DJ": "Djibouti",
  "TZ": "Tanzania",
  "DK": "Denmark",
  "DM": "Dominica",
  "DO": "Dominican Republic",
  "UA": "Ukraine",
  "UG": "Uganda",
  "DZ": "Algeria",
  "UM": "United States Minor Outlying Islands",
  "US": "United States",
  "EC": "Ecuador",
  "EE": "Estonia",
  "EG": "Egypt",
  "EH": "Western Sahara",
  "UY": "Uruguay",
  "UZ": "Uzbekistan",
  "VA": "Vatican City",
  "VC": "Saint Vincent and the Grenadines",
  "ER": "Eritrea",
  "ES": "Spain",
  "VE": "Venezuela",
  "ET": "Ethiopia",
  "EU": "Europe",
  "VG": "British Virgin Islands",
  "VI": "United States Virgin Islands",
  "VN": "Vietnam",
  "VU": "Vanuatu",
  "FI": "Finland",
  "FJ": "Fiji",
  "FK": "Falkland Islands",
  "FM": "Federated States of Micronesia",
  "FO": "Faroe Islands",
  "FR": "France",
  "WF": "Wallis and Futuna Islands",
  "OM": "Oman",
  "PA": "Panama",
  "PE": "Peru",
  "PF": "French Polynesia",
  "PG": "Papua New Guinea",
  "PH": "Philippines",
  "PK": "Pakistan",
  "PL": "Poland",
  "PM": "Saint Pierre and Miquelon",
  "PN": "Pitcairn Islands",
  "PR": "Puerto Rico",
  "PS": "Palestine",
  "PT": "Portugal",
  "PW": "Palau",
  "PY": "Paraguay",
  "QA": "Qatar",
  "A1": "Anonymous proxy",
  "A2": "Satellite transmission",
  "AD": "Andorra",
  "AE": "United Arab Emirates",
  "AF": "Afghanistan",
  "AG": "Antigua and Barbuda",
  "AI": "Anguilla",
  "AL": "Albania",
  "AM": "Armenia",
  "AO": "Angola",
  "AP": "Asia-Pacific",
  "AQ": "Antarctica",
  "AR": "Argentina",
  "AS": "American Samoa",
  "RE": "Reunion",
  "AT": "Austria",
  "AU": "Australia",
  "AW": "Aruba",
  "AX": "Aland Islands",
  "AZ": "Azerbaijan",
  "RO": "Romania",
  "BA": "Bosnia and Herzegovina",
  "BB": "Barbados",
  "RS": "Serbia",
  "BD": "Bangladesh",
  "BE": "Belgium",
  "RU": "Russia",
  "BF": "Burkina Faso",
  "RW": "Rwanda",
  "BG": "Bulgaria",
  "BH": "Bahrain",
  "BI": "Burundi",
  "BJ": "Benin",
  "BL": "Saint Barthelemy",
  "BM": "Bermuda",
  "BN": "Brunei",
  "BO": "Bolivia",
  "SA": "Saudi Arabia",
  "BQ": "Caribbean Netherlands",
  "SB": "Solomon Islands",
  "BR": "Brazil",
  "SC": "Seychelles",
  "SD": "Sudan",
  "BS": "Bahamas",
  "SE": "Sweden",
  "BT": "Bhutan",
  "BV": "Bouvet Island",
  "SG": "Singapore",
  "SH": "Saint Helena",
  "BW": "Botswana"
}


```

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DescribeProtectionModuleCodeConfig
&CodeType=14
&InstanceId=waf-cn-zz11sr5****
&CodeValue=0
&<common request parameters>
```

Sample success responses

`XML` format

```
<DescribeProtectionModuleCodeConfigResponse>
	  <RequestId>64D24280-1AD9-4D41-8844-872168E59BF3</RequestId>
	  <CodeConfigs>
		    <code>0</code>
		    <name>310000,530000,150000,110000,TW_01,220000,510000,120000,640000,340000,370000,140000,440000,450000,650000,320000,360000,130000,410000,330000,460000,420000,430000,MO_01,620000,350000,540000,520000,210000,500000,610000,630000,HK_01,230000</name>
	  </CodeConfigs>
</DescribeProtectionModuleCodeConfigResponse>
```

`JSON` format

```
{
	"RequestId": "64D24280-1AD9-4D41-8844-872168E59BF3",
	"CodeConfigs": [
		{
			"code": 0,
			"name": "310000,530000,150000,110000,TW_01,220000,510000,120000,640000,340000,370000,140000,440000,450000,650000,320000,360000,130000,410000,330000,460000,420000,430000,MO_01,620000,350000,540000,520000,210000,500000,610000,630000,HK_01,230000"
		}
	]
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/waf-openapi).

