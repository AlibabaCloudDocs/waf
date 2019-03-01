# File upload requests blocked by Alibaba Cloud WAF {#concept_j4m_kfl_q2b .concept}

## Symptoms {#section_qpw_kfl_q2b .section}

When a client uses the POST method to upload files from a browser, they may receive the 405 error telling that the request was blocked by Alibaba Cloud WAF.

## Causes {#section_rpw_kfl_q2b .section}

When a client uses the POST method to upload a file, the file content will be transcoded and added to the POST body. Therefore, Alibaba Cloud WAF also inspects the file content. In case the file content contains sensitive keywords, Alibaba Cloud WAF regards the request as malicious code and intercepts the request.

## Resolution {#section_spw_kfl_q2b .section}

Currently, no active measure is available to avoid such false positives caused by transcoded files. We recommend that you create an HTTP ACL rule to allow the client request.

