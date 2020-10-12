---
keyword: [whitelist, custom, protection policy, match condition, match field, match content, logical operator]
---

# Fields in match conditions

You need to add match conditions to rules when you configure a whitelist and customize protection policies for Web Application Firewall \(WAF\). This topic describes the fields that can be used in the match conditions and their descriptions.

## Match conditions and actions

In the WAF console, you can customize whitelist rules and access control rules. A custom rule consists of match conditions and actions. When you create a rule, you need to specify the match fields, logical operators, and match content to add match conditions. You also need to select an action that is triggered when requests match the conditions you specify.

-   **Match conditions**

    Each match condition consists of a match field, logical operator, and match content. The match content does not support regular expressions. You can add a maximum of five match conditions to a custom rule, and the logical relation among the conditions is AND. It means that the custom rule works when all the match conditions are met.

-   **Action**

    When you configure a whitelist rule, you must select a module for Modules Bypassing Check, it means that requests are not checked by the module you select. An action that you select when you configure custom protection policies is triggered for requests that meet match conditions. For more information, see the following topics:

    -   [Configure the website whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the website whitelist.md)
    -   [Configure the web intrusion prevention whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the web intrusion prevention whitelist.md)
    -   [Configure the access control and throttling whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the access control and throttling whitelist.md)
    -   [Configure the bot management whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the bot management whitelist.md)
    -   [Configure the data security whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure the data security whitelist.md)
    -   [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)

## Match fields supported

The following table lists the supported match fields in match conditions. **Advanced fields** are supported in only WAF **Business** or higher.

|Match field|Advanced field|Logical operator|Description|
|-----------|--------------|----------------|-----------|
|**IP**|No|Has and Does not have|The source IP address of the access request. You can enter IP addresses or CIDR blocks, for example, 1.1.1.1/24. **Note:** You can enter a maximum of 50 IP addresses or CIDR blocks. Separate them with commas \(,\). |
|**URL**|No|-   Includes and Does not include
-   Equals to and Does not equal to
-   URI Path Match
-   Regular Expression

|The URL of the access request.|
|**Referer**|No|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than
-   Does not exist

|The URL of the source page from which the access request is redirected.|
|**User-Agent**|No|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than

|The browser information of the client that initiates access requests. The information includes the browser, rendering engine, and version.|
|**Params**|No|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than

|The parameter part in the request URL, usually the part that follows the question mark \(?\) in the URL. For example, in `www.abc.com/index.html? action=login`, `action=login` is the parameter part.|
|**Cookie**|Yes|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than
-   Does not exist

|The cookie information in the access request.|
|**Content-Type**|Yes|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than

|The HTTP content type \(MIME\) specified in the response.|
|**Content-Length**|Yes|Value less than, Value equals, and Value more than|The number of bytes in the response.|
|**X-Forwarded-For**|Yes|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than
-   Does not exist

|The IP address of the client that initiates the access request. X-Forwarded-For \(XFF\) is used to identify the HTTP request header field of the initial IP address of the client initiating the access request that is forwarded through an HTTP proxy or a Server Load Balancer \(SLB\) instance. XFF is only included in the access requests that are forwarded by the HTTP proxy or SLB instances.|
|**Post-Body**|Yes|-   Includes and Does not include
-   Equals to and Does not equal to

|The content of the response.|
|**Http-Method**|Yes|Equals to and Does not equal to|The request method, such as GET, POST, DELETE, PUT, and OPTIONS.|
|**Header**|Yes|-   Includes and Does not include
-   Equals to and Does not equal to
-   Length equals, Length more than, and Length less than
-   Does not exist

|The header of the request, which is used to customize the HTTP header.|
|**URLPath**|Yes|-   Includes and Does not include
-   Equals to and Does not equal to
-   URI Path Match
-   Regular Expression

|The URL of the access request.|

## Logical operator descriptions

|Logical operator|Description|
|----------------|-----------|
|Has and Does not have|Whether the match field has the match content.|
|Includes and Does not include|Whether the match field includes the match content.|
|Equals to and Does not equal to|Whether the match field equals the match content.|
|Length equals, Length more than, and Length less than|Whether the length of the match field is equal to, greater than, or less than that of the match content.|
|Does not exist|The match field does not exist.|
|Value less than, Value equals, and Value more than|The value of the match field is less than, equal to, or greater than that of the match content.|
|URI Path Match|The prefix of the match field contains the match content.|
|Regular Expression|The match field matches the regular expression defined in the match content.|

