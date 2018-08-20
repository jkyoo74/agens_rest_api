# AgensGraph RESTFul API
- Author: Jungkeun Yoo
## INTRODUCTION
AgensGraph already has RESTFul APIs. 
User can use these APIs to access AgensGraph.  

This contains descriptions of there APIs.

## REQUIREMENT
* AgensGraph as a Graph Database Server
* AgensBrowser as a RESTFul API Server
* Tools for calling these APIs(Restlet Client as Chrome plugin)

## SETUP
You can download below link
- DOWNLOAD [agens graph](https://bitnine.net/downloads/agensgraph-v-1-3-linux/)
- DOWNLOAD [agens browser](https://bitnine.net/downloads/agensbrowser-v-1-0/)

you can also refer to documentation in [bitnine site](https://bitnine.net/documentation/) for installation.

## FLOW

![flow_of_call](flow_of_call.png)

### /api/auth/connect
1st call must be '/api/auth/connect'

#### request
```
URL: http://localhost:8085/api/auth/connect
Method: GET
Parameter: NO
```
#### response
```
{
"valid": true,
"user_ip": "0:0:0:0:0:0:0:1",
"user_name": "agens",
"state": "SUCCESS",
"message": "AgensBrowser web v1.0 (since 2018-02-01)",
"ssid": "df3f72e5-33f3-46b0-9cb6-c72be56f89e3",
"timestamp": "2018-08-20 04:42:27"
}
```
the important thing is to remember the ssid value in the response.
At the next request, this value will be set request header 'Authorization'.
