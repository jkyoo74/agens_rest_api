# AgensGraph RESTFul API
- Author: Jungkeun Yoo

## INTRODUCTION
AgensGraph supports RESTFul APIs for accessing AgensGraph.

This document includes descriptions of there APIs.

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
The first call must be '/api/auth/connect'.
create session information through this api.
#### example1: request to connect
##### request
```
URL: http://localhost:8085/api/auth/connect
Method: GET
Parameter: NO
```
##### response
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

### /api/core/meta
This call retrieves the metadata for all objects in graph db(node, edge...)

#### example1:
##### request
```
URL: http://localhost:8085/api/core/meta
Method: GET
Parameter: no
```
##### response
```
{
    "meta": {
        "nodes": [
            {
                "data": {
                    "size": 19,
                    "name": "hw",
                    "id": "12",
                    "labels": [
                        "NODE"
                    ],
                    "props": {
                        "owner": "agens",
                        "size": 19,
                        "name": "hw",
                        "is_dirty": false,
                        "id": "12",
                        "size_not_empty": 19,
                        "desc": ""
                    }
                }
            }
        ],
        "meta": [
            {
                "owner": "",
                "size": 1,
                "neighbors": [
                ],
                "name": "EDGE",
                "is_dirty": true,
                "oid": "118a8eb2-30af-4095-8a9b-153eabf88182",
                "type": "EDGE",
                "size_not_empty": 1,
                "properties": [
                ],
                "desc": ""
            },
            {
                "owner": "",
                "size": 1,
                "neighbors": [
                ],
                "name": "NODE",
                "is_dirty": true,
                "oid": "8536fada-4185-4e2d-89c1-de913ddb78b8",
                "type": "NODE",
                "size_not_empty": 1,
                "properties": [
                ],
                "desc": ""
            }
        ],
        "edges": [
            {
                "data": {
                    "size": 22,
                    "name": "connect_to",
                    "id": "13",
                    "source": "12",
                    "labels": [
                        "EDGE"
                    ],
                    "target": "12",
                    "props": {
                        "owner": "agens",
                        "size": 22,
                        "name": "connect_to",
                        "is_dirty": false,
                        "id": "13",
                        "size_not_empty": 22,
                        "desc": ""
                    }
                }
            }
        ]
    },
    "is_dirty": false,
    "state": "SUCCESS",
    "message": "network, labels.size=2 (1/1), relations=1, isDirty=false",
    "graph": {
        "owner": "agens",
        "name": "network",
        "is_dirty": false,
        "oid": "16386",
        "jdbc_url": "jdbc:postgresql://127.0.0.1:5432/agens?ApplicationName=AgensBrowser",
        "version": 1.3,
        "desc": ""
    },
    "labels": [
        {
            "owner": "agens",
            "size": 22,
            "neighbors": [
                "hw"
            ],
            "name": "connect_to",
            "is_dirty": false,
            "oid": "13",
            "type": "EDGE",
            "size_not_empty": 22,
            "properties": [
                {
                    "size": 22,
                    "type": "STRING",
                    "key": "label"
                },
                {
                    "size": 22,
                    "type": "NUMBER",
                    "key": "no"
                },
                {
                    "size": 22,
                    "type": "STRING",
                    "key": "type"
                }
            ],
            "desc": ""
        },
        {
            "owner": "agens",
            "size": 19,
            "neighbors": [
                "hw"
            ],
            "name": "hw",
            "is_dirty": false,
            "oid": "12",
            "type": "NODE",
            "size_not_empty": 19,
            "properties": [
                {
                    "size": 19,
                    "type": "STRING",
                    "key": "name"
                },
                {
                    "size": 19,
                    "type": "STRING",
                    "key": "rack"
                },
                {
                    "size": 19,
                    "type": "STRING",
                    "key": "type"
                }
            ],
            "desc": ""
        }
    ]
}

```


### /api/core/query
This call executes the cypher to perform data handling.

#### example1: request with cypher
##### request
```
URL: http://localhost:8085/api/core/query
Method: GET
Parameter: sql, options

/api/core/query?sql=MATCH(a) return a limit 10
```
##### response
```
{
    "request": {
        "options": "",
        "txid": "core#100002",
        "type": "QUERY",
        "ssid": "dd71eb04-1464-41df-a544-f2d4a1769d03",
        "command": "",
        "sql": "MATCH (a) RETURN a limit 10;",
        "target": ""
    },
    "record": {
        "meta": [
            {
                "name": "a",
                "index": 0,
                "type": "NODE"
            }
        ],
        "rows": [
            [
                {
                    "data": {
                        "size": 1,
                        "name": "1.1",
                        "id": "1.1",
                        "labels": [
                            "ag_vertex"
                        ],
                        "props": {
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "ROUTER",
                        "id": "12.1",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-1",
                            "name": "ROUTER",
                            "type": "ROUTER"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "SW_1ST",
                        "id": "12.2",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-3",
                            "name": "SW_1ST",
                            "type": "SWITCH"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "SW_BB",
                        "id": "12.3",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-4",
                            "name": "SW_BB",
                            "type": "SWITCH"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "SW_SAN",
                        "id": "12.4",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "INT#2-3",
                            "name": "SW_SAN",
                            "type": "SWITCH"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "FW_1ST",
                        "id": "12.5",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-2",
                            "name": "FW_1ST",
                            "type": "FIREWALL"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "FW_INT",
                        "id": "12.6",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-6",
                            "name": "FW_INT",
                            "type": "FIREWALL"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "FW_DB",
                        "id": "12.7",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-5",
                            "name": "FW_DB",
                            "type": "FIREWALL"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "IPS1",
                        "id": "12.8",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-7",
                            "name": "IPS1",
                            "type": "IPS"
                        }
                    }
                }
            ],
            [
                {
                    "data": {
                        "size": 1,
                        "name": "FW_WEB",
                        "id": "12.9",
                        "labels": [
                            "hw"
                        ],
                        "props": {
                            "rack": "PUB#1-8",
                            "name": "FW_WEB",
                            "type": "WEBFIREWALL"
                        }
                    }
                }
            ]
        ]
    },
    "state": "SUCCESS",
    "message": "return 10 rows (cols=1), graph(nodes=10, edges=0)",
    "graph": {
        "nodes": [
            {
                "data": {
                    "size": 1,
                    "name": "ROUTER",
                    "id": "12.1",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-1",
                        "name": "ROUTER",
                        "type": "ROUTER"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "SW_1ST",
                    "id": "12.2",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-3",
                        "name": "SW_1ST",
                        "type": "SWITCH"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "FW_WEB",
                    "id": "12.9",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-8",
                        "name": "FW_WEB",
                        "type": "WEBFIREWALL"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "FW_DB",
                    "id": "12.7",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-5",
                        "name": "FW_DB",
                        "type": "FIREWALL"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "IPS1",
                    "id": "12.8",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-7",
                        "name": "IPS1",
                        "type": "IPS"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "FW_1ST",
                    "id": "12.5",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-2",
                        "name": "FW_1ST",
                        "type": "FIREWALL"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "FW_INT",
                    "id": "12.6",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-6",
                        "name": "FW_INT",
                        "type": "FIREWALL"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "SW_BB",
                    "id": "12.3",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "PUB#1-4",
                        "name": "SW_BB",
                        "type": "SWITCH"
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "1.1",
                    "id": "1.1",
                    "labels": [
                        "ag_vertex"
                    ],
                    "props": {
                    }
                }
            },
            {
                "data": {
                    "size": 1,
                    "name": "SW_SAN",
                    "id": "12.4",
                    "labels": [
                        "hw"
                    ],
                    "props": {
                        "rack": "INT#2-3",
                        "name": "SW_SAN",
                        "type": "SWITCH"
                    }
                }
            }
        ],
        "meta": [
            {
                "owner": "",
                "size": 0,
                "neighbors": [
                ],
                "name": "ag_vertex",
                "is_dirty": true,
                "oid": "b1cb1775-d005-4b9c-8c42-3e1b473933b4",
                "type": "NODE",
                "size_not_empty": 0,
                "properties": [
                ],
                "desc": ""
            },
            {
                "owner": "agens",
                "size": 9,
                "neighbors": [
                    "hw"
                ],
                "name": "hw",
                "is_dirty": false,
                "oid": "12",
                "type": "NODE",
                "size_not_empty": 9,
                "properties": [
                    {
                        "size": 9,
                        "type": "STRING",
                        "key": "name"
                    },
                    {
                        "size": 9,
                        "type": "STRING",
                        "key": "rack"
                    },
                    {
                        "size": 9,
                        "type": "STRING",
                        "key": "type"
                    }
                ],
                "desc": ""
            }
        ],
        "edges": [
        ]
    }
}
```
#### example2: request with sql
##### request
```
URL: http://localhost:8085/api/core/query
Method: GET
Parameter: sql, options

/api/core/query?sql=select 1
```
##### response
```
{
    "request": {
        "options": "",
        "txid": "core#100005",
        "type": "QUERY",
        "ssid": "bbbcb0da-06f7-4a45-b5d3-0e9c7e72ca7a",
        "command": "",
        "sql": "select 1;",
        "target": ""
    },
    "record": {
        "meta": [
            {
                "name": "?column?",
                "index": 0,
                "type": "NUMBER"
            }
        ],
        "rows": [
            [
                1
            ]
        ]
    },
    "state": "SUCCESS",
    "message": "return 1 rows (cols=1), no graph",
    "graph": {
        "nodes": [
        ],
        "meta": [
        ],
        "edges": [
        ]
    }
}
```

### /api/core/command
This call executes the to perform create and drop label(vertex label, edge label)

#### example1: request with parameter to create vlabel
##### request
```
URL: http://localhost:8085/api/core/command
Method: GET
Parameter: type, command, target, options
           type - CREATE, DROP
           target - vlabel, elabel
           command - name of vlabel, elabel
           
/api/core/command?command=vlabel&type=CREATE&target=label_new
```
##### response
```
{
    "request": {
        "options": "",
        "txid": "core#100004",
        "type": "CREATE",
        "ssid": "dd71eb04-1464-41df-a544-f2d4a1769d03",
        "command": "vlabel",
        "sql": "CREATE vlabel label_new;",
        "target": "label_new"
    },
    "label": {
        "owner": "agens",
        "size": 0,
        "neighbors": [
        ],
        "name": "label_new",
        "is_dirty": true,
        "oid": "14",
        "type": "NODE",
        "size_not_empty": 0,
        "properties": [
        ],
        "desc": ""
    },
    "state": "SUCCESS",
    "message": "'CREATE' affected\n Also meta storage is updated(ADD/REPLACE)"
}

```
### /api/auth/disconnect
This call removes session id.
if you want to call other api, you must call '/api/auth/connect'.

#### example1: request to disconnect
##### request
```
URL: http://localhost:8085/api/auth/disconnect
Method: GET
Parameter: NO
```
##### response
```
{
    "_link": "http://localhost:8085/api/core/connect",
    "state": "SUCCESS",
    "message": "disconnect client: ssid='dd71eb04-1464-41df-a544-f2d4a1769d03', done=true"
}
```
