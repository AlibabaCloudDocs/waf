# Data visualization {#concept_hkz_kgq_p2b .concept}

Based on the detailed website logs collected by WAF, WAF provides the data visualization service. By converting the data into a visual big screen, you can monitor and understand the real-time attack and defense situations of your website. This provides you with visual and transparent data analysis and decision-making capabilities to keep your website security.

## Features {#section_w5s_1hq_p2b .section}

Currently, the WAF data visualization service provides the following two visual screens for your choice:

**Note:** More WAF data visualization screens are coming.

**Note:** Because of the particularity of visual screens, only Google Chrome browser 56 and a later version is supported.

## WAF Real-time Attack and Defense Situation Screen {#section_tvy_lq3_y2b .section}

WAF real-time attack and defense situation screen is updated every second. It displays current day's website visit and overall interception situations for all your websites that protected by WAF. This screen focus on displaying the stability of the website service and the quality of the network service.

**Note:** The data range on this screen is from 0:00 to the current time of today.

|Display item|Description|
|------------|-----------|
|Inbound Bandwidth|Inbound bandwidth traffic \(Unit: bps\).|
|Outbound Bandwidth|Outbound bandwidth traffic \(Unit: bps\).|
|QPS|Current website traffic \(Unit: QPS\).|
|Interception Ratio|The percentage of the website requests that are intercepted by WAF.|
|Today's Interceptions|The number of the website requests that are intercepted by WAF.|
|Mobile OS Distribution|OS distribution for the visit requests from mobile clients.|
|PC Browser Distribution|Browser distribution for the visit requests from PC clients.|
|Top 10 Source IPs|The top 10 source IPs that have most visits and their visit volumes.|
|Top 5 Visited URLs|The top 5 URLs that is visited and their visit volumes.|
|Exception Monitoring|The exception HTTP response status code returned and their occurrences.|
|Visit Statistics \(Mainland China\)|The visit statistics heat map shows the source distribution of the visit requests in the last hour.|
|Request|Shows the visit request trending \(Unit: QPS\). Additionally, this chart shows the trend in the number of requests intercepted by WAF, including precise access control interception, anti-fraud interception, web attack interception and HTTP flood attack interception.|
|Bandwidth|Shows the inbound and outbound bandwidth trending \(Unit: bps\).|

The white points on the earth in the middle of the screen show the global WAF server room.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15576/155800683510401_en-US.png)

## WAF Security Data Platform Screen {#section_bgy_1dj_y2b .section}

WAF security data platform screen displays security information about web attacks, HTTP flood attack, and precise access control interceptions.

**Note:** By clicking the Domains to be Monitored area at the lower-left corner of the screen, you can choose the domains that you want to monitor. You can also choose to monitor all the domains.

|Display item|Description|
|------------|-----------|
|Total Visits|The number of total visits of the selected domains on the day.|
|Web Attacks|The number of web attacks intercepted by WAF for the selected domains on the day.|
|HTTP Flood Attacks|The number of HTTP flood attacks intercepted by WAF for the selected domains on the day.|
|Precise Access Control|The number of requests intercepted by the WAF precise access control rules for the selected domains on the day.|
|Top Web Attack Source IP|Top attack source IPs, the region of the IPs, and their attack volumes. Additionally, hover the mouse over the top attack source IP to view the web attack type distribution and the tags of the source IP.|
|Regional heat map|The regional heat map on the upper-right corner shows the distribution of the regions that the attack source belongs to.|

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15576/155800683510406_en-US.png)

The radar chart in the middle of the WAF security data platform screen shows the visits, web attack interception, HTTP flood attack interception, and precise access control interceptions every 15 minutes as an interval. Additionally, you can select a time period in the radar chart, and click the floating window, to view detailed security data information for that time period.

**Note:** Click the date at the bottom of the large screen to select to display the security data for the specified date.

|Display item|Description|
|------------|-----------|
|Visits|Website visits \(Unit: QPS\).|
|Web Attacks|The number of web attacks intercepted by WAF.|
|HTTP Flood Attacks|The number of HTTP flood attacks intercepted by WAF.|
|Precise Access Control|The number of requests intercepted by precise access control rules in WAF.|
|Top Web Attack Source IP|Top attack source IPs, the region of the IPs, and their attack volumes. Additionally, hover the mouse over the top attack source IP to view the web attack type distribution and the tags of the source IP.|
|Web Attack Types|The distribution of web attack types intercepted.|
|Top Attack Regions|The top 5 attack source regions.|
|Top Hit Rules|The top 5 WAF protection rules that were hit.|

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15576/155800683510408_en-US.png)

## Enable the Data Visualization service {#section_pgs_cbm_z2b .section}

To enable the Data Visualization service, follow these steps:

1.  Log on to the [Alibaba Cloud Security WAF management console](https://yundun.console.aliyun.com/?p=waf).
2.  Go to **Reports** \> **Data Visualization**, select the region of your WAF instance, and click **Purchase Now**。

    **Note:** If the region of your WAF instance is International, you must upgrade it to the Business or Enterprise version.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15576/155800683511139_en-US.png)

3.  On the WAF instance upgrade page, select **Single Screen** or **Multiple Screens**.

    |Options|Description|Pricing|
    |-------|-----------|-------|
    |Single Screen|Only one data visualization screen is supported.|USD 300/month|
    |Multiple Screen|All WAF data visualization screens are supported.|USD 600/month|

    **Note:** The Data Visualization service inherits the expiration time of your current WAF instance. According to the service option you selected and the expiration time of the current WAF instance, the system automatically calculates the payment for you. After you enable the Data Visualization service, you have to renew the Data Visualization service when you renew your WAF instance.

4.  Click to select the **Web Application Firewall Service of Terms**, and click **Pay**.
5.  On the **Data Visualization**page, click one data visualization screen to enjoy the WAF Data Visualization service.

    **Note:** If you purchased the Single Screen service, select one data visualization screen, and click **Enable Now**.


