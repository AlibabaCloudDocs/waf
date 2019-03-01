# How to handle ECS intrusion? {#concept_zcm_kvl_q2b .concept}

The ECS instances can still encounter intrusion, even after being protected by WAF. It may be caused because of the following:

|No.|Causes|Resolution|
|---|------|----------|
|1|The ECS instance is intruded before it is connected to WAF. In this case, you must first clean up the ECS instance.|Perform a server cleanup as described in the following sections.|
|2|When the DNS resolution is not updated once WAF is configured. This makes the traffic flow directly to ECS, without letting it pass through WAF.|Make sure that DNS resolution is updated so that the website is under the protection of WAF. For more information, see [Implement Alibaba Cloud WAF](../../../../../reseller.en-US/User Guide/Implementation/Deploy Alibaba Cloud WAF.md#).|
|3|Before WAF is used, the IP address of the ECS instance is disclosed and no security group is configured. As a result, hackers directly attack the ECS instance through its IP address.|Configure a security group to prevent attacks that can bypass WAF. For more information, see [Protect your origin server](../../../../../reseller.en-US/Best Practices/Protect your origin server.md#).|
|4|Other sites that are not protected by WAF exist on the ECS instance. The ECS instance is consequently affected by attacks targeting these sites.|Make sure that all HTTP services on the ECS instance are protected by WAF.|
|5|The ECS instance encounters non-Web-attack intrusions, such as the brute crack of the ssh password.|Make sure that the ECS instance and database adopt strong passwords.|

**Note:** Before clearing Trojans and viruses, first [Create a snapshot](../../../../../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up data to avoid data loss arising from operation mistakes.

## Clear Trojans and viruses {#section_twr_clb_ygb .section}

1.  Check the network connection by using `netstat` and analyze if any suspicious requests exist. If yes, stop the ECS instance.
2.  Use antivirus software to scan and clean viruses.

Run the following command to clear Trojans in Linux.

```
chattr -i /usr/bin/.sshd 
rm -f /usr/bin/.sshd 
chattr -i /usr/bin/.swhd 
rm -f /usr/bin/.swhd 
rm -f -r /usr/bin/bsd-port 
cp /usr/bin/dpkgd/ps /bin/ps 
cp /usr/bin/dpkgd/netstat /bin/netstat 
cp /usr/bin/dpkgd/lsof /usr/sbin/lsof 
cp /usr/bin/dpkgd/ss /usr/sbin/ss
rm -r -f /root/.ssh 
rm -r -f /usr/bin/bsd-port
find /proc/ -name exe | xargs ls -l | grep -v task |grep deleted| awk '{print $11}' | awk -F/ '{print $NF}' | xargs killall -9
```

## Check and fix vulnerabilities for your ECS instance {#section_kw1_flb_ygb .section}

1.  Check if the server account is normal. If the server account is abnormal, stop the ECS and delete the abnormal account.
2.  Check if the remote logon to ECS exists. If yes, set up a strong logon password that contains more than 10 characters and consists of uppercase and lowercase alphabets, digits, and special characters.
3.  Confirm that the backend passwords of Jenkins, Tomcat, PhpMyadmin, WDCP, and Weblogic are strong passwords. You can disable the management port 8080, if the services are not in use.
4.  Check for vulnerabilities for Web applications, such as struts and ElasticSearch. Make sure that the website is protected by WAF. We recommend that you use Server Guard for Trojans and viruses clearing and patches installation.
5.  Check if the following vulnerability exists: the Jenkins administrator runs commands remotely without using a password. If yes, set a password or close the page for managing the 8080 port.
6.  Check if the following vulnerability exists: files can be written on Redis without using a password. Check if SSH logon key files created by hackers exist under `/root/`. If the files exist, delete the files. Modify Redis to make users access Redis using passwords and configure stronger passwords. If access to public networks is not required, use `bind 127.0.0.1` to only allow local access.
7.  Check MySQL, SQLServer, FTP, and Web management backend for which passwords are set and make sure you set strong passwords.

## Enable Alibaba Cloud Security services {#section_kq2_glb_ygb .section}

-   Make sure that WAF is enabled for all websites on the ECS instance.
-   Use Alibaba Cloud Security Threat Detection Service for host scanning, Trojans scanning and clearing, and fixing vulnerabilities.

## Reinitialize the cloud disk {#section_yhd_hlb_ygb .section}

If the preceding methods cannot help you fix the problem, we recommend that you reinitialize your cloud disk to restore the system disk or the data disk to the status when they were created.

For more information, see [Reinitialize a cloud disk](../../../../../reseller.en-US/Block storage/Block storage/Reinitialize a cloud disk.md#).

**Note:** Before re-initializing the cloud disk, download and back up the data on the system disk and data disk to your local storage. After initialization, perform antivirus for the data and then upload it to your cloud storage.

When the cloud disk is reinitialized, perform the preceding cleanup and enable Alibaba Cloud Security.

