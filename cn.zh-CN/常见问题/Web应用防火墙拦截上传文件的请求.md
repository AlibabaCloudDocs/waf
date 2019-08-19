# Web应用防火墙拦截上传文件的请求 {#concept_j4m_kfl_q2b .concept}

本文介绍了业务接入Web应用防火墙后，上传文件请求被Web应用防火墙拦截的解决方法。

## 问题描述 {#section_qpw_kfl_q2b .section}

在浏览器中调用POST方法上传文件时，会有一定的概率出现405错误，提示被Web应用防火墙拦截。

## 问题原因 {#section_rpw_kfl_q2b .section}

因为POST方法上传文件时，文件本身的内容也会被转码放到POST请求的body中一起上传，并且同样会被Web应用防火墙检测到。当转码后的文件中出现一些关键字时，就会被Web应用防火墙误认为含有恶意代码，从而拦截。

## 解决方案 {#section_spw_kfl_q2b .section}

由于是文件转码后的误命中，暂时没有主动的解决办法，建议您将该地址加入精准访问控制的放行规则里。

