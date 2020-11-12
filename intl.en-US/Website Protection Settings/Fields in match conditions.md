---
keyword: [whitelist, custom, protection policy, match condition, match field, match content, logical operator]
---

# Fields in match conditions

You must add match conditions to rules when you configure a whitelist and customize protection policies for Web Application Firewall \(WAF\). This topic describes the fields that you can use in the match conditions and their descriptions.

## Match conditions and actions

In the WAF console, you can customize rules for whitelists and protection policies. A custom rule consists of match conditions and actions. When you create a rule, you must specify the match fields, logical operators, and match content to add match conditions. You also need to select an action that is triggered when requests match the conditions you specify.

-   **Match conditions**

    Each match condition consists of a match field, logical operator, and match content. The match content does not support regular expressions. You can add a maximum of five match conditions to a custom rule, and the logical relation among the conditions is AND. The custom rule works only when all the match conditions are met.

-   **Action**

    When you configure a whitelist rule, you must select features for Modules Bypassing Check so that requests that meet match conditions bypass the corresponding checks. When you configure custom protection policies, you must select an action that is triggered for requests that meet match conditions. For more information, see the following topics:

    -   [Configure a website whitelist](/intl.en-US/Website Protection Settings/Whitelist/Configure a website whitelist.md)
    -   [Configure a whitelist for Web Intrusion Prevention](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Web Intrusion Prevention.md)
    -   [Configure a whitelist for Access Control/Throttling](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Access Control/Throttling.md)
    -   [Configure a whitelist for Bot Management](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Bot Management.md)
    -   [Configure a whitelist for Data Security](/intl.en-US/Website Protection Settings/Whitelist/Configure a whitelist for Data Security.md)
    -   [Create a custom protection policy](/intl.en-US/Website Protection Settings/Access control and throttling/Create a custom protection policy.md)

## Supported match fields

The following table lists the match fields that are supported in match conditions.

|Match field|Edition|Logical operator|Description|
|-----------|-------|----------------|-----------|
|**IP**|Pro edition or higher|Has and Does not have|The source IP address of an access request. You can enter IP addresses or CIDR blocks, for example, 1.1.1.1/24. **Note:** You can enter a maximum of 50 IP addresses or CIDR blocks. Separate them with commas \(,\). |
|**URL**|Pro edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   URI Path Match
-   Regular Expression

|The URL of an access request.|
|**Referer**|Pro edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than
-   Does not exist

|The URL of the source page from which the access request is redirected.|
|**User-Agent**|Pro edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than

|The browser information of the client that initiates access requests. The information includes the browser, rendering engine, and version.|
|**Params**|Pro edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than

|The parameter part in the request URL, usually the part that follows the question mark \(?\) in the URL. For example, in `www.abc.com/index.html? action=login`, `action=login` is the parameter part.|
|**Cookie**|Business edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than
-   Does not exist

|The cookie information in an access request.|
|**Content-Type**|Business edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than

|The HTTP content type \(MIME\) in the response.|
|**Content-Length**|Business edition or higher|Value less than, Value equals, and Value more than|The number of bytes in the response.|
|**X-Forwarded-For**|Business edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than
-   Does not exist

|The actual IP address of the client that initiates access requests. X-Forwarded-For \(XFF\) is an HTTP header field. It is used to identify the originating IP address of a client that connects to the server through an HTTP proxy or a Server Load Balancer \(SLB\) instance. XFF is only included in the access requests that are forwarded by the HTTP proxy or SLB instance.|
|**Post-Body**|Business edition or higher|-   Includes and Does not include
-   Equals and Does not equal

|The content of an access request.|
|**Http-Method**|Business edition or higher|Equals and Does not equal|The request method, such as GET, POST, DELETE, PUT, and OPTIONS.|
|**Header**|Business edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   Length equals, Length more than, and Length less than
-   Does not exist

|The header of an access request, which is used to customize the HTTP header.|
|**URLPath**|Business edition or higher|-   Includes and Does not include
-   Equals and Does not equal
-   URI Path Match
-   Regular Expression

|The URL path of an access request.|

## Logical operators

|Logical operator|Description|
|----------------|-----------|
|Has and Does not have|Whether the match field has the match content.|
|Includes and Does not include|Whether the match field includes the match content.|
|Equals and Does not equal|Whether the match field equals the match content.|
|Length equals, Length more than, and Length less than|The length of the match field is equal to, greater than, or less than that of the match content.|
|Does not exist|The match field does not exist.|
|Value less than, Value equals, and Value more than|The value of the match field is less than, equal to, or greater than that of the match content.|
|URI Path Match|The prefix of the match field contains the match content.|
|Regular Expression|The match field matches the regular expression defined in the match content.|

