# Long connection timeout {#concept_ak4_dyl_q2b .concept}

## Symptoms {#section_hkx_dyl_q2b .section}

In some service scenarios, when a client submits a request, the server returns a response after more than 60s for processing. The server does not exchange any data with the client during the processing.

For example, you upload an Excel file on the Web page, requiring the server to process data in the file \(the processing time is about 3 minutes\). Within 120s after the file is submitted, no data \(HTTP or TCP packet\) is exchanged between the client and the server. In this case, WAF returns a 504 timeout response to the client and disconnects the connection.

This is because WAF does not maintain a long connection that lasts more than 120s \(without any data exchange\) and this Layer 7 timeout interval \(120s\) cannot be modified.

## Resolution {#section_ikx_dyl_q2b .section}

We recommend that you modify the exchange mode of the request so that some data \(such as Ack packet, heartbeat packet, and keep-alive packet that can maintain the session\) can be exchanged for long connections within 60s.

Considering the diversity of user scenarios, code-level modification suggestions are not provided. You must make adjustments according to your service features.

