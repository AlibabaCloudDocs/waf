# Mark WAF back-to-origin flow {#concept_qnm_clr_bgb .concept}

When you add a website domain configuration in Web Application Firewall for protection, you can set the flow mark for the website domain. When the traffic of the website domain passes through WAF, WAF adds the specified flow mark to the requests. Thus, the origin server can easily collect corresponding information.

According to the HTTP header field name and the field value that you specify in the flow mark, when the traffic passes through WAF, WAF adds the fields and values to the HTTP Header of all requests. By marking the traffic, you can easily identify traffic that are forwarded by WAF, and then configure precise origin server protection policies \(Access Control\), or analyze protection effects.

**Note:** If the user-defined HTTP Header field that you specified as flow mark already exists in the request, WAF still overwrites the field value with the specified flow mark field value in the request.

## Procedure {#section_vdh_fct_bgb .section}

1.  Log on to the [Alibaba Cloud WAF console](https://partners-intl.console.aliyun.com/#/waf).
2.  On the top of the page, select the region: **Mainland China**, **International**.
3.  Go to the **Management** \> **Website Configuration** page, choose a domain configuration record, and click **Edit**.

    **Note:** You can also specify flow mark when adding a new website domain configuration record.

4.  In the Flow Mark configuration item, enter the Header field name and the field value.

    **Note:** Do not specify a user-defined HTTP Header field that has already been used. Otherwise, the value of this field in the request is overwritten by the flow mark field value by WAF.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/78548/154451478034038_en-US.png)

5.  Click **OK**. After the configuration takes effect, WAF adds the specified HTTP header fields and values when forwarding requests to the website domain.

