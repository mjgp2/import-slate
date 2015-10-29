---
title: API Documentation 1.0

search: true
---

# API Documentation 1.0
> ### Produces
> `application/json`

### Authorization: api_key
Type | Name | In | Description
--- | --- | --- | ---
apiKey | _apikey | query | 



## Disown connector

```http
POST /store/connector/{id}/_disown HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "status": "OK"
}	
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

Make myself no longer the owner of a connector, removing it from My Data.

Connectors cannot be deleted.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the object

### Responses
Http code | Type | Description
--- | --- | ---
200 | [StatusResponse](#statusresponse) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Get connectorversion schema

```http
GET /store/connectorversion/{id}/schema HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "inputProperties": [
        {
            "defaultValue": "http:\/\/site.com\/page.html",
            "type": "URL",
            "name": "webpage\/url"
        }
    ],
    "guid": "68b858b3-e6b3-bd24-5a5e-36b0e4f13d0d",
    "outputProperties": [
        {
            "type": "DOUBLE",
            "name": "no_number"
        },
        {
            "type": "STRING",
            "name": "competition_value"
        },
        {
            "type": "DOUBLE",
            "name": "competition_value_numbers"
        },
        {
            "type": "STRING",
            "name": "john_value"
        },
        {
            "type": "STRING",
            "name": "adam_value"
        },
        {
            "type": "STRING",
            "name": "robert_value"
        },
        {
            "type": "STRING",
            "name": "paul_value"
        },
        {
            "type": "IMAGE",
            "name": "piccy_image"
        },
        {
            "type": "CURRENCY",
            "name": "cost_price"
        }
    ],
    "_meta": {
        "timestamp": 1427729022748,
        "creatorGuid": "84920b9e-9578-3948-0174-5f15b344d094",
        "creationTimestamp": 1427729022748,
        "lastEditorGuid": "84920b9e-9578-3948-0174-5f15b344d094",
        "ownerGuid": "9e7f165e-a8c2-481e-9f02-6bbe05ec68af"
    }
}	
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the ConnectorVersion

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Schema](#schema) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Count connectors

```http
GET /store/connector/_count HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "count": "608800\\"
}	
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
q | query | string | Optional. An elasticsearch [query string](http://www.elastic.co/guide/en/elasticsearch/reference/1.x/query-dsl-query-string-query.html#query-string-syntax)
_exists | query | array[string] | Optional. Required fields (multi-valued)
_missing | query | array[string] | Optional. Fields that must be null (multi-valued)
_field | query | string | Optional. Field to operate on
_type | query | string | Optional. The type of search
_default_operator | query | string | Optional. Operator a space character represents.
_mine | query | boolean | Optional. Restrict to just the objects you own

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Count](#count) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Magically get data

```http
GET /store/connector/_magic HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "tables": {
        "connectorVersionGuid": "string",
        "pagination": {
            "pattern": "string",
            "next": "string",
            "currentPageNum": "integer",
            "previous": "string"
        },
        "connectorGuid": "string",
        "totalResults": "integer",
        "errorType": "string",
        "outputProperties": [
            {
                "type": "string",
                "name": "string"
            }
        ],
        "cookies": [
            "string"
        ],
        "results": [
            "object"
        ],
        "pageUrl": "string",
        "error": "string",
        "data": "object"
    }
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

This is the simplest way to convert a URL into data using the import.io platform.

This will magically generate up to 3 different `ConnectorVersion` configurations, and return a `Page` object for each representing lists or tables on the page at that URL.

Javascript and infinite scroll support in beta.

You can select the region to process using a keyword contained within it.

If you wish to repeatedly extract the same table from many URLs, you can use the `connectorVersionGuid` returned in the table in the Magic versioned method below, or the standard query methods (although these do not support js/infinite scroll currently).




### Parameters
Name | In | Type | Description
--- | --- | --- | ---
url<b title="required">&nbsp;*&nbsp;</b> | query | string | URL you wish to process
format | query | string | Optional. The output response format. JSON_HASH will add an additional field &#039;_hash&#039; to the result that is a hash of the result fields.
js | query | boolean | Optional. Whether to process with javascript on (slower)
infiniteScrollPages | query | integer | Optional. How many times to load infinite scroll - requires js=true
regionText | query | string | Optional. Process the area that contains this phrase

### Responses
Http code | Type | Description
--- | --- | ---
200 | [MagicTables](#magictables) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Get test results

```http
GET /store/connector/{id}/_attachment/testResults/{testResults} HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "status": "string",
    "results": [
        {
            "test": {
                "proxyPort": "integer",
                "expectedPages": "integer",
                "name": "string",
                "proxyPassword": "string",
                "proxyHost": "string",
                "expectedFields": "integer",
                "expectedTotalResults": "integer",
                "proxyUsername": "string",
                "pageExamples": [
                    {
                        "connectorVersionGuid": "string",
                        "pagination": {
                            "pattern": "string",
                            "next": "string",
                            "currentPageNum": "integer",
                            "previous": "string"
                        },
                        "connectorGuid": "string",
                        "totalResults": "integer",
                        "errorType": "string",
                        "outputProperties": [
                            {
                                "type": "string",
                                "name": "string"
                            }
                        ],
                        "cookies": [
                            "string"
                        ],
                        "results": [
                            "object"
                        ],
                        "pageUrl": "string",
                        "error": "string",
                        "data": "object"
                    }
                ],
                "guid": "string",
                "expectedResults": "integer"
            },
            "result": {
                "renderedHTML": "string",
                "status": "string",
                "expectedPages": "integer",
                "runAt": "integer",
                "actualFields": "integer",
                "actualTotalResults": "integer",
                "actualResults": "integer",
                "expectedTotalResults": "integer",
                "expectedResults": "integer",
                "cpuMilliseconds": "integer",
                "name": "string",
                "expectedFields": "integer",
                "testFailureException": {
                    "message": "string",
                    "exceptionType": "string"
                },
                "responseMilliseconds": "integer",
                "actualPages": "integer",
                "input": "object"
            }
        }
    ],
    "thrownException": {
        "message": "string",
        "exceptionType": "string"
    }
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Object
testResults<b title="required">&nbsp;*&nbsp;</b> | path | string | Value of the `testResults` field in the `Connector`

### Responses
Http code | Type | Description
--- | --- | ---
200 | [CheckResults](#checkresults) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Attachment version history

```http
GET /store/connector/{id}/_attachment/{field}/_history HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "hits": {
        "hits": [
            {
                "_score": 1,
                "_type": "Attachment",
                "_id": "fe465046e-6af8-40ce-90ce-7b34b26ba66c",
                "fields": {
                    "field": "settings",
                    "bucketGuid": "edf21d7e-cb36-4e82-10dd-d3dfaeca6fbf",
                    "objectGuid": "2300189f-b35a-4139-a10c-4cc21e238019",
                    "_meta": {
                        "timestamp": 1408116739909,
                        "creatorGuid": "1396ebdb-e59d-4db1-b3a0-32db31a3e634",
                        "creationTimestamp": 1408116739909,
                        "lastEditorGuid": "1396ebdb-e59d-4db1-b3a0-32db31a3e634",
                        "ownerGuid": "1396ebdb-e59d-4db1-b3a0-32db31a3e634"
                    },
                    "size": 48
                }
            }
        ],
        "total": 1,
        "max_score": 1
    },
    "took": 483,
    "timed_out": false
}	
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Object
_page | query | integer | Optional. The page to return
field<b title="required">&nbsp;*&nbsp;</b> | path | string | The field name of the attachment in the object

### Responses
Http code | Type | Description
--- | --- | ---
200 | [AttachmentSearch](#attachmentsearch) | Successful response


## Search connectors

```http
GET /store/connector/_search HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "hits": {
        "hits": [
            {
                "_score": 1,
                "_type": "Connector",
                "_id": "b409c071-5e09-4346-be9c-1f00097e419b",
                "fields": {
                    "status": "WORKING",
                    "lastCheckedAt": 1428050602915,
                    "_meta": {
                        "timestamp": 1428050603218,
                        "creatorGuid": "f7841145-ab7f-4461-8ffe-ff160535d56a",
                        "creationTimestamp": 1428050602319,
                        "lastEditorGuid": "84920b9e-9578-3948-0174-5f15b344d094",
                        "ownerGuid": "f7841145-ab7f-4461-8ffe-ff160535d56a"
                    },
                    "name": "Test Connector - 79dwdl3504",
                    "source": "http:\/\/site.com",
                    "headline": "Headline",
                    "latestVersionGuid": "1ef446f1-5669-4769-ae80-5407a8b01753",
                    "lastModifiedAt": 1428050602626,
                    "publishRequestGuid": "5522a505-4169-4a2f-9917-020ab93ad8f1",
                    "publishRequest": "5522a505-4169-4a2f-9917-020ab93ad8f1",
                    "lastPublishRequestGuid": "5522a505-4169-4a2f-9917-020ab93ad8f1",
                    "latestVersion": 1428050602915,
                    "guid": "017b4da8-ce99-4bfa-b882-a4a107e47293",
                    "type": "API",
                    "testResults": "6bf627a2-ad31-4c70-ad1e-b13dd205de63"
                }
            }
        ],
        "total": 1,
        "max_score": 1
    },
    "took": 145,
    "timed_out": false
}	
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

Search your connectors - or all Connectors if you are an administrator of an organization.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
q | query | string | Optional. An elasticsearch [query string](http://www.elastic.co/guide/en/elasticsearch/reference/1.x/query-dsl-query-string-query.html#query-string-syntax)
_page | query | integer | Optional. The page to return
_perpage | query | integer | Optional. Up to 100
_sort | query | string | Optional. The field to sort upon, e.g. _meta.creationTimestamp
_sortDirection | query | string | Optional. Direction of sort; ASC or DESC
_exists | query | array[string] | Optional. Required fields (multi-valued)
_missing | query | array[string] | Optional. Fields that must be null (multi-valued)
_facet | query | array[string] | Optional. Fields that should have facets produced (multi-valued)
_field | query | string | Optional. Field to operate on
_type | query | string | Optional. The type of search
_default_operator | query | string | Optional. Operator a space character represents.
_mine | query | boolean | Optional. Restrict to just the objects you own

### Responses
Http code | Type | Description
--- | --- | ---
200 | [ConnectorSearch](#connectorsearch) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Advanced query

```http
POST /store/connector/{id}/_query HTTP/1.1
Content-Type: application/json

{
    "query": {
        "proxyPort": "integer",
        "connectorVersionGuid": "string",
        "cookies": [
            "string"
        ],
        "format": "string",
        "returnPaginationSuggestions": "boolean",
        "proxyPassword": "string",
        "proxyHost": "string",
        "proxyUsername": "string",
        "input": "object",
        "userAgent": "string",
        "page": "integer"
    }
}
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "connectorVersionGuid": "string",
    "pagination": {
        "pattern": "string",
        "next": "string",
        "currentPageNum": "integer",
        "previous": "string"
    },
    "connectorGuid": "string",
    "totalResults": "integer",
    "errorType": "string",
    "outputProperties": [
        {
            "type": "string",
            "name": "string"
        }
    ],
    "cookies": [
        "string"
    ],
    "results": [
        "object"
    ],
    "pageUrl": "string",
    "error": "string",
    "data": "object"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

You can pass up cookies to use for a query in the input object optionally. This is shown in the example.

This feature is required if you are using authenticated APIs and maintaining a session between calls.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Connector you are querying.
query<b title="required">&nbsp;*&nbsp;</b> | body | [Query](#query) | The query to execute.

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Page](#page) | Successful response
default | [ErrorModel](#errormodel) | error payload

## Simple query

```http
GET /store/connector/{id}/_query HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "connectorVersionGuid": "string",
    "pagination": {
        "pattern": "string",
        "next": "string",
        "currentPageNum": "integer",
        "previous": "string"
    },
    "connectorGuid": "string",
    "totalResults": "integer",
    "errorType": "string",
    "outputProperties": [
        {
            "type": "string",
            "name": "string"
        }
    ],
    "cookies": [
        "string"
    ],
    "results": [
        "object"
    ],
    "pageUrl": "string",
    "error": "string",
    "data": "object"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

This is the simplest way to make a query onto the import.io platform.

Specify your inputs as `input={name}:{value}` named query string parameters, for example:

```html
/store/connector/d50aff7b-ad19-4f64-ab1a-1e8f9a1bb249/_query?
    input=webpage/url:http%3A%2F%2Fcdn.import.io%2Ftest%2Fpages%2Fbasic%2Findex.html
```

There can be default values for inputs, e.g. the URL you extracted data from for `webpage/url`. You can see the defaults in the `Schema` of the `ConnectorVersion`.




### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Connector you are querying.
format | query | string | Optional. The output response format. The _HASH variants will add an additional field &#039;_hash&#039; to the result that is a hash of the result fields.
page | query | integer | Optional. The page you require (if supported by the Connector)
version | query | string | Optional. The specific ConnectorVersion you want to query if not the latest
input | query | array[string] | Optional. The inputs in the format {name}:{value} (multiple unique keys and their input values as query parameters accepted)

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Page](#page) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Get extra settings

```http
GET /store/connector/{id}/_attachment/settings/{settings} HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
```

Returns crawl - or other - additional settings.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Object
settings<b title="required">&nbsp;*&nbsp;</b> | path | string | Value of the `settings` field in the `Connector`

### Responses
Http code | Type | Description
--- | --- | ---
200 | no content | OK


## New api key

```http
POST /auth/apikeyadmin HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "apiKey": "string"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
password | query | string | Optional. Optional and not required for regular users.

### Responses
Http code | Type | Description
--- | --- | ---
200 | [ApiKey](#apikey) | Successful response
default | [ErrorModel](#errormodel) | error payload

## Get api key

```http
GET /auth/apikeyadmin HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "apiKey": "string"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
password | query | string | Optional. Optional and not required for regular users.

### Responses
Http code | Type | Description
--- | --- | ---
200 | [ApiKey](#apikey) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Get data snapshot

```http
GET /store/connector/{id}/_attachment/snapshot/{snapshot} HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "tiles": [
        {
            "name": "string",
            "unlocked": "boolean",
            "settings": "object",
            "type": "string",
            "results": [
                {
                    "query": {
                        "proxyPort": "integer",
                        "connectorVersionGuid": "string",
                        "cookies": [
                            "string"
                        ],
                        "format": "string",
                        "returnPaginationSuggestions": "boolean",
                        "proxyPassword": "string",
                        "proxyHost": "string",
                        "proxyUsername": "string",
                        "input": "object",
                        "userAgent": "string",
                        "page": "integer"
                    },
                    "enabled": "boolean",
                    "pages": [
                        {
                            "connectorVersionGuid": "string",
                            "pagination": {
                                "pattern": "string",
                                "next": "string",
                                "currentPageNum": "integer",
                                "previous": "string"
                            },
                            "connectorGuid": "string",
                            "totalResults": "integer",
                            "errorType": "string",
                            "outputProperties": [
                                {
                                    "type": "string",
                                    "name": "string"
                                }
                            ],
                            "cookies": [
                                "string"
                            ],
                            "results": [
                                "object"
                            ],
                            "pageUrl": "string",
                            "error": "string",
                            "data": "object"
                        }
                    ],
                    "name": "string"
                }
            ],
            "schemas": "object"
        }
    ]
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

Returns uploaded snapshots: crawls or data set data


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Object
snapshot<b title="required">&nbsp;*&nbsp;</b> | path | string | Value of the `snapshot` field in the `Connector`

### Responses
Http code | Type | Description
--- | --- | ---
200 | [DataView](#dataview) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Get session user

```http
GET /auth/currentuser HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "username": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "roles": [
        "string"
    ],
    "orgGuid": "string",
    "guid": "string",
    "email": "string"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Responses
Http code | Type | Description
--- | --- | ---
200 | [User](#user) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Update connector

```http
PATCH /store/connector/{id} HTTP/1.1
Content-Type: application/json

{
    "connector": {
        "status": "string",
        "lastCheckedAt": "integer",
        "forkedFromGuid": "string",
        "tags": [
            "string"
        ],
        "latestVersionGuid": "string",
        "testResults": "string",
        "pagePattern": "string",
        "publishRequestGuid": "string",
        "latestVersion": "integer",
        "pendingPublishRequestGuid": "string",
        "reversedDomain": "string",
        "authenticated": "boolean",
        "name": "string",
        "extension": "string",
        "settings": "string",
        "headline": "string",
        "_meta": {
            "lastEditorGuid": "string",
            "timestamp": "integer",
            "orgGuid": "string",
            "objectGuid": "string",
            "creationTimestamp": "integer",
            "creatorGuid": "string",
            "patchTimestamp": "integer",
            "ownerGuid": "string"
        },
        "lastModifiedAt": "integer",
        "source": "string",
        "publishRequest": "string",
        "snapshot": "string",
        "parentGuid": "string",
        "publishSnapshot": "string",
        "type": "string",
        "lastPublishRequestGuid": "string"
    }
}
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "guid": "017b4da8-ce99-4bfa-b882-a4a107e47293",
    "_meta": {
        "timestamp": 1428100396593,
        "patchTimestamp": 1428050603218,
        "lastEditorGuid": "58e092b4-4f13-4674-9258-6f1b1d34234c"
    },
    "tags": [
        "TAG"
    ]
}	
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

Overwrites supplied fields. Declared fields with `null` values will be nullified in the store.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | GUID of the Data Source
timestamp | query | string | Optional. Required timestamp of the object
connector<b title="required">&nbsp;*&nbsp;</b> | body | [Connector](#connector) | Class of the object

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Connector](#connector) | Successful response
default | [ErrorModel](#errormodel) | error payload

## Get connector

```http
GET /store/connector/{id} HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "status": "WORKING",
    "lastCheckedAt": 1428050602915,
    "_meta": {
        "timestamp": 1428050603218,
        "creatorGuid": "f7841145-ab7f-4461-8ffe-ff160535d56a",
        "creationTimestamp": 1428050602319,
        "lastEditorGuid": "84920b9e-9578-3948-0174-5f15b344d094",
        "ownerGuid": "f7841145-ab7f-4461-8ffe-ff160535d56a"
    },
    "name": "Test Connector - 79dwdl3504",
    "source": "http:\/\/site.com",
    "headline": "Headline",
    "latestVersionGuid": "1ef446f1-5669-4769-ae80-5407a8b01753",
    "lastModifiedAt": 1428050602626,
    "publishRequestGuid": "5522a505-4169-4a2f-9917-020ab93ad8f1",
    "publishRequest": "5522a505-4169-4a2f-9917-020ab93ad8f1",
    "lastPublishRequestGuid": "5522a505-4169-4a2f-9917-020ab93ad8f1",
    "latestVersion": 1428050602915,
    "guid": "017b4da8-ce99-4bfa-b882-a4a107e47293",
    "type": "API",
    "testResults": "6bf627a2-ad31-4c70-ad1e-b13dd205de63"
}	
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the object

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Connector](#connector) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Get publish snapshot

```http
GET /store/connector/{id}/_attachment/publishSnapshot/{publishSnapshot} HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "tiles": [
        {
            "name": "string",
            "unlocked": "boolean",
            "settings": "object",
            "type": "string",
            "results": [
                {
                    "query": {
                        "proxyPort": "integer",
                        "connectorVersionGuid": "string",
                        "cookies": [
                            "string"
                        ],
                        "format": "string",
                        "returnPaginationSuggestions": "boolean",
                        "proxyPassword": "string",
                        "proxyHost": "string",
                        "proxyUsername": "string",
                        "input": "object",
                        "userAgent": "string",
                        "page": "integer"
                    },
                    "enabled": "boolean",
                    "pages": [
                        {
                            "connectorVersionGuid": "string",
                            "pagination": {
                                "pattern": "string",
                                "next": "string",
                                "currentPageNum": "integer",
                                "previous": "string"
                            },
                            "connectorGuid": "string",
                            "totalResults": "integer",
                            "errorType": "string",
                            "outputProperties": [
                                {
                                    "type": "string",
                                    "name": "string"
                                }
                            ],
                            "cookies": [
                                "string"
                            ],
                            "results": [
                                "object"
                            ],
                            "pageUrl": "string",
                            "error": "string",
                            "data": "object"
                        }
                    ],
                    "name": "string"
                }
            ],
            "schemas": "object"
        }
    ]
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

Returns the static data from training a Connector.


### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | ID of the Object
publishSnapshot<b title="required">&nbsp;*&nbsp;</b> | path | string | Value of the `publishSnapshot` field in the `Connector`

### Responses
Http code | Type | Description
--- | --- | ---
200 | [DataView](#dataview) | Successful response
default | [ErrorModel](#errormodel) | error payload


## Query login

```http
POST /store/connector/{id}/_login HTTP/1.1
Content-Type: application/json

{
    "input": {
        "username": "string",
        "password": "string"
    }
}
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "connectorVersionGuid": "string",
    "pagination": {
        "pattern": "string",
        "next": "string",
        "currentPageNum": "integer",
        "previous": "string"
    },
    "connectorGuid": "string",
    "totalResults": "integer",
    "errorType": "string",
    "outputProperties": [
        {
            "type": "string",
            "name": "string"
        }
    ],
    "cookies": [
        "string"
    ],
    "results": [
        "object"
    ],
    "pageUrl": "string",
    "error": "string",
    "data": "object"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

This API logs into the target site for an authenticated API. Pass the cookies back through a POST query to use the authenticated session.




### Parameters
Name | In | Type | Description
--- | --- | --- | ---
id<b title="required">&nbsp;*&nbsp;</b> | path | string | id of the Connector you are querying.
input<b title="required">&nbsp;*&nbsp;</b> | body | [QueryLoginInput](#querylogininput) | Login input

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Page](#page) | Successful response (will have no results)
default | [ErrorModel](#errormodel) | error payload


## Re-run table

```http
GET /store/connector/_magic/{connectorVersionGuid} HTTP/1.1
```
	
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "connectorVersionGuid": "string",
    "pagination": {
        "pattern": "string",
        "next": "string",
        "currentPageNum": "integer",
        "previous": "string"
    },
    "connectorGuid": "string",
    "totalResults": "integer",
    "errorType": "string",
    "outputProperties": [
        {
            "type": "string",
            "name": "string"
        }
    ],
    "cookies": [
        "string"
    ],
    "results": [
        "object"
    ],
    "pageUrl": "string",
    "error": "string",
    "data": "object"
}
```
```http
HTTP/1.1 [default] 
Content-Type: application/json

{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

This will re-run a specific `ConnectorVersion` that generated a table via the regular magic call.

Use this if you want to use the same table extraction for many URLs.




### Parameters
Name | In | Type | Description
--- | --- | --- | ---
connectorVersionGuid<b title="required">&nbsp;*&nbsp;</b> | path | string | The id of the ConnectorVersion for that table you want
url<b title="required">&nbsp;*&nbsp;</b> | query | string | URL you wish to process
format | query | string | Optional. The output response format. The _HASH variants will add an additional field &#039;_hash&#039; to the result that is a hash of the result fields.
js | query | boolean | Optional. Whether to process with javascript on (slower)
infiniteScrollPages | query | integer | Optional. How many times to load infinite scroll - requires js=true

### Responses
Http code | Type | Description
--- | --- | ---
200 | [Page](#page) | Successful response
default | [ErrorModel](#errormodel) | error payload



# Models
## DataView
```json
{
    "tiles": [
        {
            "name": "string",
            "unlocked": "boolean",
            "settings": "object",
            "type": "string",
            "results": [
                {
                    "query": {
                        "proxyPort": "integer",
                        "connectorVersionGuid": "string",
                        "cookies": [
                            "string"
                        ],
                        "format": "string",
                        "returnPaginationSuggestions": "boolean",
                        "proxyPassword": "string",
                        "proxyHost": "string",
                        "proxyUsername": "string",
                        "input": "object",
                        "userAgent": "string",
                        "page": "integer"
                    },
                    "enabled": "boolean",
                    "pages": [
                        {
                            "connectorVersionGuid": "string",
                            "pagination": {
                                "pattern": "string",
                                "next": "string",
                                "currentPageNum": "integer",
                                "previous": "string"
                            },
                            "connectorGuid": "string",
                            "totalResults": "integer",
                            "errorType": "string",
                            "outputProperties": [
                                {
                                    "type": "string",
                                    "name": "string"
                                }
                            ],
                            "cookies": [
                                "string"
                            ],
                            "results": [
                                "object"
                            ],
                            "pageUrl": "string",
                            "error": "string",
                            "data": "object"
                        }
                    ],
                    "name": "string"
                }
            ],
            "schemas": "object"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
tiles | array[[DataTile](#datatile)] | 

	
## QueryResult
```json
{
    "query": {
        "proxyPort": "integer",
        "connectorVersionGuid": "string",
        "cookies": [
            "string"
        ],
        "format": "string",
        "returnPaginationSuggestions": "boolean",
        "proxyPassword": "string",
        "proxyHost": "string",
        "proxyUsername": "string",
        "input": "object",
        "userAgent": "string",
        "page": "integer"
    },
    "enabled": "boolean",
    "pages": [
        {
            "connectorVersionGuid": "string",
            "pagination": {
                "pattern": "string",
                "next": "string",
                "currentPageNum": "integer",
                "previous": "string"
            },
            "connectorGuid": "string",
            "totalResults": "integer",
            "errorType": "string",
            "outputProperties": [
                {
                    "type": "string",
                    "name": "string"
                }
            ],
            "cookies": [
                "string"
            ],
            "results": [
                "object"
            ],
            "pageUrl": "string",
            "error": "string",
            "data": "object"
        }
    ],
    "name": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
query | [Query](#query) | 
enabled | boolean | 
pages | array[[Page](#page)] | 
name | string | 

	
## DataSource
```json
{
    "status": "string",
    "tags": [
        "string"
    ],
    "producerGuid": "string",
    "firstReadyAt": "integer",
    "name": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "working": "boolean",
    "testerGuid": "string",
    "deprecated": "boolean",
    "lastSuccessfulRunGuid": "string",
    "statusAsOf": "integer",
    "note": "string",
    "url": "string",
    "reviewerGuid": "string",
    "lastRunSuccessAt": "integer",
    "instructions": "string",
    "type": "string",
    "schema": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status<b title="required">&nbsp;*&nbsp;</b> | string | 
tags | array[string] | 
producerGuid | string | 
firstReadyAt | integer | 
name<b title="required">&nbsp;*&nbsp;</b> | string | 
_meta | [Meta](#meta) | 
working | boolean | 
testerGuid | string | 
deprecated | boolean | 
lastSuccessfulRunGuid | string | 
statusAsOf | integer | 
note | string | 
url<b title="required">&nbsp;*&nbsp;</b> | string | 
reviewerGuid | string | 
lastRunSuccessAt | integer | 
instructions | string | 
type | string | 
schema | string | 

	
## DataSourceRun
```json
{
    "status": "string",
    "runIndex": "string",
    "dataSourceGuid": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "startedAt": "integer",
    "completedAt": "integer",
    "sampleData": "string",
    "note": "string",
    "previousSuccessfulRunGuid": "string",
    "diff": "string",
    "progress": {
        "convert": "integer",
        "rows": "integer",
        "robots": "integer",
        "queue": "integer",
        "failedConvert": "integer",
        "error": "integer",
        "failedFetch": "integer",
        "fetch": "integer"
    },
    "data": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status | string | 
runIndex | string | 
dataSourceGuid | string | 
_meta | [Meta](#meta) | 
startedAt | integer | 
completedAt | integer | 
sampleData | string | 
note | string | 
previousSuccessfulRunGuid | string | 
diff | string | 
progress | object | 
data | string | 

	
## DataPackageSnapshotResponse
```json
{
    "snapshotAt": "integer",
    "previousSnapshotAt": "integer",
    "guid": "string",
    "snapshotBuildCompletedAt": "integer",
    "snapshotBuildStartedAt": "integer",
    "includedSourceIds": [
        "string"
    ],
    "packageId": "string",
    "excludedSources": [
        {
            "sourceId": "string",
            "reason": "string"
        }
    ],
    "totalObjects": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
snapshotAt | integer | 
previousSnapshotAt | integer | 
guid | string | 
snapshotBuildCompletedAt | integer | 
snapshotBuildStartedAt | integer | 
includedSourceIds | array[string] | 
packageId | string | 
excludedSources | array[[DataPackageSnapshotExcludedSource](#datapackagesnapshotexcludedsource)] | 
totalObjects | integer | 

	
## Connector
```json
{
    "status": "string",
    "lastCheckedAt": "integer",
    "forkedFromGuid": "string",
    "tags": [
        "string"
    ],
    "latestVersionGuid": "string",
    "testResults": "string",
    "pagePattern": "string",
    "publishRequestGuid": "string",
    "latestVersion": "integer",
    "pendingPublishRequestGuid": "string",
    "reversedDomain": "string",
    "authenticated": "boolean",
    "name": "string",
    "extension": "string",
    "settings": "string",
    "headline": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "lastModifiedAt": "integer",
    "source": "string",
    "publishRequest": "string",
    "snapshot": "string",
    "parentGuid": "string",
    "publishSnapshot": "string",
    "type": "string",
    "lastPublishRequestGuid": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status | string | The current status of this connector
lastCheckedAt | integer | The last date this connector was checked at
forkedFromGuid | string | What connector this was forked from
tags | array[string] | The tags for this connector, a maximum of 10
latestVersionGuid | string | The id of the latest version of the connector
testResults | string | Test results
pagePattern | string | The URL pattern that this connector can process
publishRequestGuid | string | The GUID of the publish request that has been successful
latestVersion | integer | The date of the latest version of the connector
pendingPublishRequestGuid | string | The GUID of the currently pending publish request
reversedDomain | string | The reversed domain, e.g. com.importio.api
authenticated | boolean | Is this an authenticated connector?
name<b title="required">&nbsp;*&nbsp;</b> | string | The connector&#039;s name
extension | string | This field is a code to indicate the application to be used when editing this connector
settings | string | Secondary settings JSON
headline | string | A short description of the connector
_meta | [Meta](#meta) | 
lastModifiedAt | integer | The date of the last snapshot upload or publish
source | string | The source of the data from the connector
publishRequest | string | The JSON for the last publish (save)
snapshot | string | The snapshot JSON
parentGuid | string | What connector this is linked to
publishSnapshot | string | The snapshot JSON for the last publish (save)
type | string | The connector type.
lastPublishRequestGuid | string | The GUID of the publish request that last completed

	
## CheckTestResult
```json
{
    "test": {
        "proxyPort": "integer",
        "expectedPages": "integer",
        "name": "string",
        "proxyPassword": "string",
        "proxyHost": "string",
        "expectedFields": "integer",
        "expectedTotalResults": "integer",
        "proxyUsername": "string",
        "pageExamples": [
            {
                "connectorVersionGuid": "string",
                "pagination": {
                    "pattern": "string",
                    "next": "string",
                    "currentPageNum": "integer",
                    "previous": "string"
                },
                "connectorGuid": "string",
                "totalResults": "integer",
                "errorType": "string",
                "outputProperties": [
                    {
                        "type": "string",
                        "name": "string"
                    }
                ],
                "cookies": [
                    "string"
                ],
                "results": [
                    "object"
                ],
                "pageUrl": "string",
                "error": "string",
                "data": "object"
            }
        ],
        "guid": "string",
        "expectedResults": "integer"
    },
    "result": {
        "renderedHTML": "string",
        "status": "string",
        "expectedPages": "integer",
        "runAt": "integer",
        "actualFields": "integer",
        "actualTotalResults": "integer",
        "actualResults": "integer",
        "expectedTotalResults": "integer",
        "expectedResults": "integer",
        "cpuMilliseconds": "integer",
        "name": "string",
        "expectedFields": "integer",
        "testFailureException": {
            "message": "string",
            "exceptionType": "string"
        },
        "responseMilliseconds": "integer",
        "actualPages": "integer",
        "input": "object"
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
test | [TestQuery](#testquery) | 
result | [ConnectorTestResult](#connectortestresult) | 

	
## PublishRequest
```json
{
    "forkedFromConnectorGuid": "string",
    "basedOnPublishRequestGuid": "string",
    "guid": "string",
    "connectorVersion": {
        "publishRequestGuid": "string",
        "tests": {
            "guid": "string",
            "testQueries": [
                {
                    "proxyPort": "integer",
                    "expectedPages": "integer",
                    "name": "string",
                    "proxyPassword": "string",
                    "proxyHost": "string",
                    "expectedFields": "integer",
                    "expectedTotalResults": "integer",
                    "proxyUsername": "string",
                    "pageExamples": [
                        {
                            "connectorVersionGuid": "string",
                            "pagination": {
                                "pattern": "string",
                                "next": "string",
                                "currentPageNum": "integer",
                                "previous": "string"
                            },
                            "connectorGuid": "string",
                            "totalResults": "integer",
                            "errorType": "string",
                            "outputProperties": [
                                {
                                    "type": "string",
                                    "name": "string"
                                }
                            ],
                            "cookies": [
                                "string"
                            ],
                            "results": [
                                "object"
                            ],
                            "pageUrl": "string",
                            "error": "string",
                            "data": "object"
                        }
                    ],
                    "guid": "string",
                    "expectedResults": "integer"
                }
            ]
        },
        "guid": "string",
        "runtimeConfiguration": {
            "guid": "string",
            "configuration": {
                "extraction": {
                    "resultRegexp": "string",
                    "resultPipeline": [
                        {
                            "type": "object"
                        }
                    ],
                    "errorXPaths": [
                        "string"
                    ],
                    "resultXPaths": [
                        "string"
                    ],
                    "noResultsRegExp": "string",
                    "ignoreFirst": "integer",
                    "singleResultPipeline": [
                        {
                            "type": "object"
                        }
                    ],
                    "namespaces": "object",
                    "noResultsXPaths": [
                        "string"
                    ],
                    "errorRegexp": "string",
                    "totalResultsRegExp": "string",
                    "totalResultsXPaths": [
                        "string"
                    ]
                },
                "version": "integer",
                "urlProperties": [
                    "string"
                ],
                "http404TheSameAsNoResults": "boolean",
                "playback": {
                    "javascriptDisabled": "boolean",
                    "contentType": "string",
                    "prerequests": [
                        "string"
                    ],
                    "javascriptDisabledForLogin": "boolean",
                    "loginBrowserActions": [
                        {
                            "domain": "string",
                            "format": "string",
                            "input": "string",
                            "type": "string",
                            "inputType": "string",
                            "value": "object",
                            "element": {
                                "xpaths": [
                                    "string"
                                ],
                                "formId": "string",
                                "id": "string",
                                "name": "string",
                                "formName": "string"
                            }
                        }
                    ],
                    "fixHtml": "boolean",
                    "javascriptDisabledForLastAction": "boolean",
                    "maxPages": "integer",
                    "javascriptWhitelist": "string",
                    "infiniteScrollPages": "integer",
                    "prerendered": "boolean",
                    "http10": "boolean",
                    "url": "string",
                    "browserActions": [
                        {
                            "domain": "string",
                            "format": "string",
                            "input": "string",
                            "type": "string",
                            "inputType": "string",
                            "value": "object",
                            "element": {
                                "xpaths": [
                                    "string"
                                ],
                                "formId": "string",
                                "id": "string",
                                "name": "string",
                                "formName": "string"
                            }
                        }
                    ],
                    "paginationRequests": [
                        "string"
                    ],
                    "paginationXPaths": [
                        "string"
                    ],
                    "type": "object",
                    "privileged": "boolean",
                    "crawler": "boolean"
                },
                "queryType": "object"
            }
        },
        "schema": {
            "inputProperties": [
                {
                    "defaultValue": "object",
                    "type": "string",
                    "domain": "string",
                    "name": "string"
                }
            ],
            "guid": "string",
            "outputProperties": [
                {
                    "defaultValue": "object",
                    "type": "string",
                    "domain": "string",
                    "name": "string"
                }
            ]
        }
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
forkedFromConnectorGuid | string | 
basedOnPublishRequestGuid | string | 
guid | string | 
connectorVersion | [ConnectorVersion](#connectorversion) | 

	
## Playback
```json
{
    "javascriptDisabled": "boolean",
    "contentType": "string",
    "prerequests": [
        "string"
    ],
    "javascriptDisabledForLogin": "boolean",
    "loginBrowserActions": [
        {
            "domain": "string",
            "format": "string",
            "input": "string",
            "type": "string",
            "inputType": "string",
            "value": "object",
            "element": {
                "xpaths": [
                    "string"
                ],
                "formId": "string",
                "id": "string",
                "name": "string",
                "formName": "string"
            }
        }
    ],
    "fixHtml": "boolean",
    "javascriptDisabledForLastAction": "boolean",
    "maxPages": "integer",
    "javascriptWhitelist": "string",
    "infiniteScrollPages": "integer",
    "prerendered": "boolean",
    "http10": "boolean",
    "url": "string",
    "browserActions": [
        {
            "domain": "string",
            "format": "string",
            "input": "string",
            "type": "string",
            "inputType": "string",
            "value": "object",
            "element": {
                "xpaths": [
                    "string"
                ],
                "formId": "string",
                "id": "string",
                "name": "string",
                "formName": "string"
            }
        }
    ],
    "paginationRequests": [
        "string"
    ],
    "paginationXPaths": [
        "string"
    ],
    "type": "object",
    "privileged": "boolean",
    "crawler": "boolean"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
javascriptDisabled | boolean | 
contentType | string | 
prerequests | array[string] | 
javascriptDisabledForLogin | boolean | 
loginBrowserActions | array[[BrowserAction](#browseraction)] | 
fixHtml | boolean | 
javascriptDisabledForLastAction | boolean | 
maxPages | integer | 
javascriptWhitelist | string | 
infiniteScrollPages | integer | 
prerendered | boolean | 
http10 | boolean | 
url | string | 
browserActions | array[[BrowserAction](#browseraction)] | 
paginationRequests | array[string] | 
paginationXPaths | array[string] | 
type | [QueryType](#querytype) | 
privileged | boolean | 
crawler | boolean | 

	
## Attachment
```json
{
    "field": "string",
    "bucketGuid": "string",
    "objectGuid": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "size": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
field<b title="required">&nbsp;*&nbsp;</b> | string | Owning object field
bucketGuid<b title="required">&nbsp;*&nbsp;</b> | string | Internal type identifier
objectGuid<b title="required">&nbsp;*&nbsp;</b> | string | Owning object id
_meta | [Meta](#meta) | 
size<b title="required">&nbsp;*&nbsp;</b> | integer | Size in bytes

	
## AttachmentSearch
```json
{
    "hits": {
        "hits": [
            {
                "_score": "number",
                "_id": "string",
                "fields": {
                    "field": "string",
                    "bucketGuid": "string",
                    "objectGuid": "string",
                    "_meta": {
                        "lastEditorGuid": "string",
                        "timestamp": "integer",
                        "orgGuid": "string",
                        "objectGuid": "string",
                        "creationTimestamp": "integer",
                        "creatorGuid": "string",
                        "patchTimestamp": "integer",
                        "ownerGuid": "string"
                    },
                    "size": "integer"
                }
            }
        ],
        "total": "integer",
        "max_score": "number"
    },
    "took": "integer",
    "timed_out": "boolean"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
hits<b title="required">&nbsp;*&nbsp;</b> | object | 
took<b title="required">&nbsp;*&nbsp;</b> | integer | 
timed_out<b title="required">&nbsp;*&nbsp;</b> | boolean | 

	
## Type
```json
"string"
```
	
### Fields
Name | Type | Description
--- | --- | ---

	
## MagicTables
```json
{
    "tables": {
        "connectorVersionGuid": "string",
        "pagination": {
            "pattern": "string",
            "next": "string",
            "currentPageNum": "integer",
            "previous": "string"
        },
        "connectorGuid": "string",
        "totalResults": "integer",
        "errorType": "string",
        "outputProperties": [
            {
                "type": "string",
                "name": "string"
            }
        ],
        "cookies": [
            "string"
        ],
        "results": [
            "object"
        ],
        "pageUrl": "string",
        "error": "string",
        "data": "object"
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
tables | [Page](#page) | Data tables or lists found on the page

	
## Schema
```json
{
    "inputProperties": [
        {
            "defaultValue": "object",
            "type": "string",
            "domain": "string",
            "name": "string"
        }
    ],
    "guid": "string",
    "outputProperties": [
        {
            "defaultValue": "object",
            "type": "string",
            "domain": "string",
            "name": "string"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
inputProperties | array[[IO](#io)] | 
guid | string | 
outputProperties | array[[IO](#io)] | 

	
## Status
```json
"string"
```
	
### Fields
Name | Type | Description
--- | --- | ---

	
## ConnectorTestResult
```json
{
    "renderedHTML": "string",
    "status": "string",
    "expectedPages": "integer",
    "runAt": "integer",
    "actualFields": "integer",
    "actualTotalResults": "integer",
    "actualResults": "integer",
    "expectedTotalResults": "integer",
    "expectedResults": "integer",
    "cpuMilliseconds": "integer",
    "name": "string",
    "expectedFields": "integer",
    "testFailureException": {
        "message": "string",
        "exceptionType": "string"
    },
    "responseMilliseconds": "integer",
    "actualPages": "integer",
    "input": "object"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
renderedHTML | string | 
status | [Status](#status) | 
expectedPages | integer | 
runAt | integer | 
actualFields | integer | 
actualTotalResults | integer | 
actualResults | integer | 
expectedTotalResults | integer | 
expectedResults | integer | 
cpuMilliseconds | integer | 
name | string | 
expectedFields | integer | 
testFailureException | [ConnectorTestError](#connectortesterror) | 
responseMilliseconds | integer | 
actualPages | integer | 
input | object | 

	
## ApiKey
```json
{
    "apiKey": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
apiKey | string | 

	
## Run
```json
{
    "configurationGuid": "string",
    "totalNrUrls": "integer",
    "successNrUrls": "integer",
    "completedAt": "integer",
    "apiGuid": "string",
    "errorType": "string",
    "state": "string",
    "result": {
        "field": "string",
        "bucketGuid": "string",
        "objectGuid": "string",
        "_meta": {
            "lastEditorGuid": "string",
            "timestamp": "integer",
            "orgGuid": "string",
            "objectGuid": "string",
            "creationTimestamp": "integer",
            "creatorGuid": "string",
            "patchTimestamp": "integer",
            "ownerGuid": "string"
        },
        "size": "integer"
    },
    "error": "string",
    "startedAt": "integer",
    "message": "string",
    "guid": "string",
    "userGuid": "string",
    "failedNrUrls": "integer"
}
```

Encapsulates and asynchronous run.

	
### Fields
Name | Type | Description
--- | --- | ---
configurationGuid<b title="required">&nbsp;*&nbsp;</b> | string | 
totalNrUrls | integer | The total number of URLs in the run.
successNrUrls | integer | Number of urls with successful queries
completedAt | integer | 
apiGuid<b title="required">&nbsp;*&nbsp;</b> | string | 
errorType | string | 
state<b title="required">&nbsp;*&nbsp;</b> | string | 
result | [Attachment](#attachment) | New line separated JSON concatenation of results.
error | string | Message related to the error.
startedAt | integer | 
message | string | Any messages regarding the run
guid<b title="required">&nbsp;*&nbsp;</b> | string | 
userGuid | string | 
failedNrUrls | integer | Number of urls with successful queries

	
## ConnectorTestError
```json
{
    "message": "string",
    "exceptionType": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
message | string | 
exceptionType | string | 

	
## DataPackageSubscriptions
```json
{
    "subscriptions": [
        {
            "status": "string",
            "packageSchemaName": "string",
            "packageName": "string",
            "expires": "integer",
            "scheduleEffectiveOn": "integer",
            "scheduleDaysOfWeek": "string",
            "packageGuid": "string",
            "scheduleTimesOfDay": "string"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
subscriptions | array[[DataPackageSubscription](#datapackagesubscription)] | 

	
## BrowserAction
```json
{
    "domain": "string",
    "format": "string",
    "input": "string",
    "type": "string",
    "inputType": "string",
    "value": "object",
    "element": {
        "xpaths": [
            "string"
        ],
        "formId": "string",
        "id": "string",
        "name": "string",
        "formName": "string"
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
domain | string | 
format | string | 
input | string | 
type | [Type](#type) | 
inputType | [Type](#type) | 
value | object | 
element | [Element](#element) | 

	
## DataPackageRequestResponse
```json
{
    "results": [
        {
            "url": "string",
            "message": "string",
            "guid": "string",
            "result": "string"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
results | array[[DataPackageRequestResponseUrl](#datapackagerequestresponseurl)] | 

	
## CheckResults
```json
{
    "status": "string",
    "results": [
        {
            "test": {
                "proxyPort": "integer",
                "expectedPages": "integer",
                "name": "string",
                "proxyPassword": "string",
                "proxyHost": "string",
                "expectedFields": "integer",
                "expectedTotalResults": "integer",
                "proxyUsername": "string",
                "pageExamples": [
                    {
                        "connectorVersionGuid": "string",
                        "pagination": {
                            "pattern": "string",
                            "next": "string",
                            "currentPageNum": "integer",
                            "previous": "string"
                        },
                        "connectorGuid": "string",
                        "totalResults": "integer",
                        "errorType": "string",
                        "outputProperties": [
                            {
                                "type": "string",
                                "name": "string"
                            }
                        ],
                        "cookies": [
                            "string"
                        ],
                        "results": [
                            "object"
                        ],
                        "pageUrl": "string",
                        "error": "string",
                        "data": "object"
                    }
                ],
                "guid": "string",
                "expectedResults": "integer"
            },
            "result": {
                "renderedHTML": "string",
                "status": "string",
                "expectedPages": "integer",
                "runAt": "integer",
                "actualFields": "integer",
                "actualTotalResults": "integer",
                "actualResults": "integer",
                "expectedTotalResults": "integer",
                "expectedResults": "integer",
                "cpuMilliseconds": "integer",
                "name": "string",
                "expectedFields": "integer",
                "testFailureException": {
                    "message": "string",
                    "exceptionType": "string"
                },
                "responseMilliseconds": "integer",
                "actualPages": "integer",
                "input": "object"
            }
        }
    ],
    "thrownException": {
        "message": "string",
        "exceptionType": "string"
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status | [Status](#status) | 
results | array[[CheckTestResult](#checktestresult)] | 
thrownException | [PublishingError](#publishingerror) | 

	
## WebQueryConfiguration
```json
{
    "extraction": {
        "resultRegexp": "string",
        "resultPipeline": [
            {
                "type": "object"
            }
        ],
        "errorXPaths": [
            "string"
        ],
        "resultXPaths": [
            "string"
        ],
        "noResultsRegExp": "string",
        "ignoreFirst": "integer",
        "singleResultPipeline": [
            {
                "type": "object"
            }
        ],
        "namespaces": "object",
        "noResultsXPaths": [
            "string"
        ],
        "errorRegexp": "string",
        "totalResultsRegExp": "string",
        "totalResultsXPaths": [
            "string"
        ]
    },
    "version": "integer",
    "urlProperties": [
        "string"
    ],
    "http404TheSameAsNoResults": "boolean",
    "playback": {
        "javascriptDisabled": "boolean",
        "contentType": "string",
        "prerequests": [
            "string"
        ],
        "javascriptDisabledForLogin": "boolean",
        "loginBrowserActions": [
            {
                "domain": "string",
                "format": "string",
                "input": "string",
                "type": "string",
                "inputType": "string",
                "value": "object",
                "element": {
                    "xpaths": [
                        "string"
                    ],
                    "formId": "string",
                    "id": "string",
                    "name": "string",
                    "formName": "string"
                }
            }
        ],
        "fixHtml": "boolean",
        "javascriptDisabledForLastAction": "boolean",
        "maxPages": "integer",
        "javascriptWhitelist": "string",
        "infiniteScrollPages": "integer",
        "prerendered": "boolean",
        "http10": "boolean",
        "url": "string",
        "browserActions": [
            {
                "domain": "string",
                "format": "string",
                "input": "string",
                "type": "string",
                "inputType": "string",
                "value": "object",
                "element": {
                    "xpaths": [
                        "string"
                    ],
                    "formId": "string",
                    "id": "string",
                    "name": "string",
                    "formName": "string"
                }
            }
        ],
        "paginationRequests": [
            "string"
        ],
        "paginationXPaths": [
            "string"
        ],
        "type": "object",
        "privileged": "boolean",
        "crawler": "boolean"
    },
    "queryType": "object"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
extraction | [Scraper](#scraper) | 
version | integer | 
urlProperties | array[string] | 
http404TheSameAsNoResults | boolean | 
playback | [Playback](#playback) | 
queryType | [QueryType](#querytype) | 

	
## ConnectorVersionTests
```json
{
    "guid": "string",
    "testQueries": [
        {
            "proxyPort": "integer",
            "expectedPages": "integer",
            "name": "string",
            "proxyPassword": "string",
            "proxyHost": "string",
            "expectedFields": "integer",
            "expectedTotalResults": "integer",
            "proxyUsername": "string",
            "pageExamples": [
                {
                    "connectorVersionGuid": "string",
                    "pagination": {
                        "pattern": "string",
                        "next": "string",
                        "currentPageNum": "integer",
                        "previous": "string"
                    },
                    "connectorGuid": "string",
                    "totalResults": "integer",
                    "errorType": "string",
                    "outputProperties": [
                        {
                            "type": "string",
                            "name": "string"
                        }
                    ],
                    "cookies": [
                        "string"
                    ],
                    "results": [
                        "object"
                    ],
                    "pageUrl": "string",
                    "error": "string",
                    "data": "object"
                }
            ],
            "guid": "string",
            "expectedResults": "integer"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
guid | string | 
testQueries | array[[TestQuery](#testquery)] | 

	
## DataPackageRequestResponseUrl
```json
{
    "url": "string",
    "message": "string",
    "guid": "string",
    "result": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
url | string | 
message | string | 
guid | string | 
result | string | 

	
## DataSourceConfig
```json
{
    "nextRunAt": "integer",
    "periodMinutes": "integer",
    "strategyConfiguration": "object",
    "guidUniqueFields": [
        "string"
    ],
    "strategy": "string",
    "lastRunGuid": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
nextRunAt | integer | 
periodMinutes | integer | 
strategyConfiguration | object | 
guidUniqueFields | array[string] | 
strategy | string | 
lastRunGuid | string | 

	
## DataSourceSearch
```json
{
    "hits": {
        "hits": [
            {
                "_score": "number",
                "_id": "string",
                "fields": {
                    "status": "string",
                    "tags": [
                        "string"
                    ],
                    "producerGuid": "string",
                    "firstReadyAt": "integer",
                    "name": "string",
                    "_meta": {
                        "lastEditorGuid": "string",
                        "timestamp": "integer",
                        "orgGuid": "string",
                        "objectGuid": "string",
                        "creationTimestamp": "integer",
                        "creatorGuid": "string",
                        "patchTimestamp": "integer",
                        "ownerGuid": "string"
                    },
                    "working": "boolean",
                    "testerGuid": "string",
                    "deprecated": "boolean",
                    "lastSuccessfulRunGuid": "string",
                    "statusAsOf": "integer",
                    "note": "string",
                    "url": "string",
                    "reviewerGuid": "string",
                    "lastRunSuccessAt": "integer",
                    "instructions": "string",
                    "type": "string",
                    "schema": "string"
                }
            }
        ],
        "total": "integer",
        "max_score": "number"
    },
    "took": "integer",
    "timed_out": "boolean"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
hits<b title="required">&nbsp;*&nbsp;</b> | object | 
took<b title="required">&nbsp;*&nbsp;</b> | integer | 
timed_out<b title="required">&nbsp;*&nbsp;</b> | boolean | 

	
## PublishingError
```json
{
    "message": "string",
    "exceptionType": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
message | string | 
exceptionType | string | 

	
## DataSourceRunSearch
```json
{
    "hits": {
        "hits": [
            {
                "_score": "number",
                "_id": "string",
                "fields": {
                    "status": "string",
                    "runIndex": "string",
                    "dataSourceGuid": "string",
                    "_meta": {
                        "lastEditorGuid": "string",
                        "timestamp": "integer",
                        "orgGuid": "string",
                        "objectGuid": "string",
                        "creationTimestamp": "integer",
                        "creatorGuid": "string",
                        "patchTimestamp": "integer",
                        "ownerGuid": "string"
                    },
                    "startedAt": "integer",
                    "completedAt": "integer",
                    "sampleData": "string",
                    "note": "string",
                    "previousSuccessfulRunGuid": "string",
                    "diff": "string",
                    "progress": {
                        "convert": "integer",
                        "rows": "integer",
                        "robots": "integer",
                        "queue": "integer",
                        "failedConvert": "integer",
                        "error": "integer",
                        "failedFetch": "integer",
                        "fetch": "integer"
                    },
                    "data": "string"
                }
            }
        ],
        "total": "integer",
        "max_score": "number"
    },
    "took": "integer",
    "timed_out": "boolean"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
hits<b title="required">&nbsp;*&nbsp;</b> | object | 
took<b title="required">&nbsp;*&nbsp;</b> | integer | 
timed_out<b title="required">&nbsp;*&nbsp;</b> | boolean | 

	
## StageType
```json
"object"
```
	
### Fields
Name | Type | Description
--- | --- | ---

	
## Count
```json
{
    "count": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
count | integer | 

	
## Pagination
```json
{
    "pattern": "string",
    "next": "string",
    "currentPageNum": "integer",
    "previous": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
pattern<b title="required">&nbsp;*&nbsp;</b> | string | The URL pattern for pagination
next | string | URL of the next page
currentPageNum<b title="required">&nbsp;*&nbsp;</b> | integer | The page number for this Page
previous | string | URL of the previous page

	
## PublishResult
```json
{
    "status": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "responseTime": "integer",
    "connectorGuid": "string",
    "guid": "string",
    "cpuTime": "integer",
    "result": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status | string | 
_meta | [Meta](#meta) | 
responseTime | integer | 
connectorGuid | string | 
guid | string | 
cpuTime | integer | 
result | string | 

	
## ConnectorVersionRuntimeConfiguration
```json
{
    "guid": "string",
    "configuration": {
        "extraction": {
            "resultRegexp": "string",
            "resultPipeline": [
                {
                    "type": "object"
                }
            ],
            "errorXPaths": [
                "string"
            ],
            "resultXPaths": [
                "string"
            ],
            "noResultsRegExp": "string",
            "ignoreFirst": "integer",
            "singleResultPipeline": [
                {
                    "type": "object"
                }
            ],
            "namespaces": "object",
            "noResultsXPaths": [
                "string"
            ],
            "errorRegexp": "string",
            "totalResultsRegExp": "string",
            "totalResultsXPaths": [
                "string"
            ]
        },
        "version": "integer",
        "urlProperties": [
            "string"
        ],
        "http404TheSameAsNoResults": "boolean",
        "playback": {
            "javascriptDisabled": "boolean",
            "contentType": "string",
            "prerequests": [
                "string"
            ],
            "javascriptDisabledForLogin": "boolean",
            "loginBrowserActions": [
                {
                    "domain": "string",
                    "format": "string",
                    "input": "string",
                    "type": "string",
                    "inputType": "string",
                    "value": "object",
                    "element": {
                        "xpaths": [
                            "string"
                        ],
                        "formId": "string",
                        "id": "string",
                        "name": "string",
                        "formName": "string"
                    }
                }
            ],
            "fixHtml": "boolean",
            "javascriptDisabledForLastAction": "boolean",
            "maxPages": "integer",
            "javascriptWhitelist": "string",
            "infiniteScrollPages": "integer",
            "prerendered": "boolean",
            "http10": "boolean",
            "url": "string",
            "browserActions": [
                {
                    "domain": "string",
                    "format": "string",
                    "input": "string",
                    "type": "string",
                    "inputType": "string",
                    "value": "object",
                    "element": {
                        "xpaths": [
                            "string"
                        ],
                        "formId": "string",
                        "id": "string",
                        "name": "string",
                        "formName": "string"
                    }
                }
            ],
            "paginationRequests": [
                "string"
            ],
            "paginationXPaths": [
                "string"
            ],
            "type": "object",
            "privileged": "boolean",
            "crawler": "boolean"
        },
        "queryType": "object"
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
guid | string | 
configuration | [WebQueryConfiguration](#webqueryconfiguration) | 

	
## PipelineStageConfig
```json
{
    "type": "object"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
type | [StageType](#stagetype) | 

	
## TestQuery
```json
{
    "proxyPort": "integer",
    "expectedPages": "integer",
    "name": "string",
    "proxyPassword": "string",
    "proxyHost": "string",
    "expectedFields": "integer",
    "expectedTotalResults": "integer",
    "proxyUsername": "string",
    "pageExamples": [
        {
            "connectorVersionGuid": "string",
            "pagination": {
                "pattern": "string",
                "next": "string",
                "currentPageNum": "integer",
                "previous": "string"
            },
            "connectorGuid": "string",
            "totalResults": "integer",
            "errorType": "string",
            "outputProperties": [
                {
                    "type": "string",
                    "name": "string"
                }
            ],
            "cookies": [
                "string"
            ],
            "results": [
                "object"
            ],
            "pageUrl": "string",
            "error": "string",
            "data": "object"
        }
    ],
    "guid": "string",
    "expectedResults": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
proxyPort | integer | 
expectedPages | integer | 
name | string | 
proxyPassword | string | 
proxyHost | string | 
expectedFields | integer | 
expectedTotalResults | integer | 
proxyUsername | string | 
pageExamples | array[[Page](#page)] | 
guid | string | 
expectedResults | integer | 

	
## ConnectorSearch
```json
{
    "hits": {
        "hits": [
            {
                "_score": "number",
                "_id": "string",
                "fields": {
                    "status": "string",
                    "lastCheckedAt": "integer",
                    "forkedFromGuid": "string",
                    "tags": [
                        "string"
                    ],
                    "latestVersionGuid": "string",
                    "testResults": "string",
                    "pagePattern": "string",
                    "publishRequestGuid": "string",
                    "latestVersion": "integer",
                    "pendingPublishRequestGuid": "string",
                    "reversedDomain": "string",
                    "authenticated": "boolean",
                    "name": "string",
                    "extension": "string",
                    "settings": "string",
                    "headline": "string",
                    "_meta": {
                        "lastEditorGuid": "string",
                        "timestamp": "integer",
                        "orgGuid": "string",
                        "objectGuid": "string",
                        "creationTimestamp": "integer",
                        "creatorGuid": "string",
                        "patchTimestamp": "integer",
                        "ownerGuid": "string"
                    },
                    "lastModifiedAt": "integer",
                    "source": "string",
                    "publishRequest": "string",
                    "snapshot": "string",
                    "parentGuid": "string",
                    "publishSnapshot": "string",
                    "type": "string",
                    "lastPublishRequestGuid": "string"
                }
            }
        ],
        "total": "integer",
        "max_score": "number"
    },
    "took": "integer",
    "timed_out": "boolean"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
hits<b title="required">&nbsp;*&nbsp;</b> | object | 
took<b title="required">&nbsp;*&nbsp;</b> | integer | 
timed_out<b title="required">&nbsp;*&nbsp;</b> | boolean | 

	
## Element
```json
{
    "xpaths": [
        "string"
    ],
    "formId": "string",
    "id": "string",
    "name": "string",
    "formName": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
xpaths | array[string] | 
formId | string | 
id | string | 
name | string | 
formName | string | 

	
## PackageUrlRequest
```json
{
    "url": "string",
    "note": "string",
    "guid": "string",
    "status": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
url | string | 
note | string | 
guid | string | 
status | string | 

	
## IO
```json
{
    "defaultValue": "object",
    "type": "string",
    "domain": "string",
    "name": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
defaultValue | object | 
type | [Type](#type) | 
domain | string | 
name | string | 

	
## DataPackageSnapshotExcludedSource
```json
{
    "sourceId": "string",
    "reason": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
sourceId | string | 
reason | string | 

	
## StatusResponse
```json
{
    "status": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status | string | 

	
## Property
```json
{
    "type": "string",
    "name": "string"
}
```

A data property (or field) definition

	
### Fields
Name | Type | Description
--- | --- | ---
type<b title="required">&nbsp;*&nbsp;</b> | [Type](#type) | 
name<b title="required">&nbsp;*&nbsp;</b> | string | 

	
## DataTile
```json
{
    "name": "string",
    "unlocked": "boolean",
    "settings": "object",
    "type": "string",
    "results": [
        {
            "query": {
                "proxyPort": "integer",
                "connectorVersionGuid": "string",
                "cookies": [
                    "string"
                ],
                "format": "string",
                "returnPaginationSuggestions": "boolean",
                "proxyPassword": "string",
                "proxyHost": "string",
                "proxyUsername": "string",
                "input": "object",
                "userAgent": "string",
                "page": "integer"
            },
            "enabled": "boolean",
            "pages": [
                {
                    "connectorVersionGuid": "string",
                    "pagination": {
                        "pattern": "string",
                        "next": "string",
                        "currentPageNum": "integer",
                        "previous": "string"
                    },
                    "connectorGuid": "string",
                    "totalResults": "integer",
                    "errorType": "string",
                    "outputProperties": [
                        {
                            "type": "string",
                            "name": "string"
                        }
                    ],
                    "cookies": [
                        "string"
                    ],
                    "results": [
                        "object"
                    ],
                    "pageUrl": "string",
                    "error": "string",
                    "data": "object"
                }
            ],
            "name": "string"
        }
    ],
    "schemas": "object"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
name | string | 
unlocked | boolean | 
settings | object | 
type | string | 
results | array[[QueryResult](#queryresult)] | 
schemas | object | 

	
## Page
```json
{
    "connectorVersionGuid": "string",
    "pagination": {
        "pattern": "string",
        "next": "string",
        "currentPageNum": "integer",
        "previous": "string"
    },
    "connectorGuid": "string",
    "totalResults": "integer",
    "errorType": "string",
    "outputProperties": [
        {
            "type": "string",
            "name": "string"
        }
    ],
    "cookies": [
        "string"
    ],
    "results": [
        "object"
    ],
    "pageUrl": "string",
    "error": "string",
    "data": "object"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
connectorVersionGuid<b title="required">&nbsp;*&nbsp;</b> | string | The id of the ConnectorVersion that created this Page
pagination | [Pagination](#pagination) | Pagination information if requested
connectorGuid<b title="required">&nbsp;*&nbsp;</b> | string | The id of the Connector that owns the ConnectorVersion that created this Page
totalResults | integer | The total results in the result set
errorType | string | The type of error (if there is an error)
outputProperties<b title="required">&nbsp;*&nbsp;</b> | array[[Property](#property)] | The declared schema for the results
cookies<b title="required">&nbsp;*&nbsp;</b> | array[string] | Contents of the cookie jar
results | array[[Result](#result)] | An object whose keys are determined by the output schema for this Connector
pageUrl<b title="required">&nbsp;*&nbsp;</b> | string | The URL that represents the source of the data
error | string | Error description
data | object | Global data or meta-data

	
## QueryType
```json
"object"
```
	
### Fields
Name | Type | Description
--- | --- | ---

	
## ErrorModel
```json
{
    "code": "string",
    "data": "object",
    "error": "string"
}
```

Encapsulates a non-2xx response

	
### Fields
Name | Type | Description
--- | --- | ---
code<b title="required">&nbsp;*&nbsp;</b> | string | An error code representing the type of error
data | object | Supplementary data about the error
error | string | Human-readable description of the error

	
## DataSourceConfigCrawlerStrategy
```json
{
    "inRunExtractionConfig": [
        {
            "apiGuid": "string",
            "type": "string",
            "urlPattern": "string"
        }
    ],
    "preCrawlExtractionConfig": [
        {
            "query": {
                "proxyPort": "integer",
                "connectorGuids": [
                    "string"
                ],
                "proxyPassword": "string",
                "proxyHost": "string",
                "startPage": "integer",
                "proxyUsername": "string",
                "input": "object",
                "loginOnly": "boolean",
                "maxPages": "integer",
                "requestId": "string"
            }
        }
    ],
    "crawlerConfig": {
        "cookiesEnabled": "boolean",
        "pause": "integer",
        "connectorGuid": "string",
        "destination": "string",
        "crawlTemplate": [
            "string"
        ],
        "advancedMode": "boolean",
        "connections": "integer",
        "maxDepth": "integer",
        "dataTemplate": [
            "string"
        ],
        "local": "boolean",
        "startUrls": [
            "string"
        ]
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
inRunExtractionConfig | array[object] | 
preCrawlExtractionConfig | array[object] | 
crawlerConfig | object | 

	
## ConnectorVersion
```json
{
    "publishRequestGuid": "string",
    "tests": {
        "guid": "string",
        "testQueries": [
            {
                "proxyPort": "integer",
                "expectedPages": "integer",
                "name": "string",
                "proxyPassword": "string",
                "proxyHost": "string",
                "expectedFields": "integer",
                "expectedTotalResults": "integer",
                "proxyUsername": "string",
                "pageExamples": [
                    {
                        "connectorVersionGuid": "string",
                        "pagination": {
                            "pattern": "string",
                            "next": "string",
                            "currentPageNum": "integer",
                            "previous": "string"
                        },
                        "connectorGuid": "string",
                        "totalResults": "integer",
                        "errorType": "string",
                        "outputProperties": [
                            {
                                "type": "string",
                                "name": "string"
                            }
                        ],
                        "cookies": [
                            "string"
                        ],
                        "results": [
                            "object"
                        ],
                        "pageUrl": "string",
                        "error": "string",
                        "data": "object"
                    }
                ],
                "guid": "string",
                "expectedResults": "integer"
            }
        ]
    },
    "guid": "string",
    "runtimeConfiguration": {
        "guid": "string",
        "configuration": {
            "extraction": {
                "resultRegexp": "string",
                "resultPipeline": [
                    {
                        "type": "object"
                    }
                ],
                "errorXPaths": [
                    "string"
                ],
                "resultXPaths": [
                    "string"
                ],
                "noResultsRegExp": "string",
                "ignoreFirst": "integer",
                "singleResultPipeline": [
                    {
                        "type": "object"
                    }
                ],
                "namespaces": "object",
                "noResultsXPaths": [
                    "string"
                ],
                "errorRegexp": "string",
                "totalResultsRegExp": "string",
                "totalResultsXPaths": [
                    "string"
                ]
            },
            "version": "integer",
            "urlProperties": [
                "string"
            ],
            "http404TheSameAsNoResults": "boolean",
            "playback": {
                "javascriptDisabled": "boolean",
                "contentType": "string",
                "prerequests": [
                    "string"
                ],
                "javascriptDisabledForLogin": "boolean",
                "loginBrowserActions": [
                    {
                        "domain": "string",
                        "format": "string",
                        "input": "string",
                        "type": "string",
                        "inputType": "string",
                        "value": "object",
                        "element": {
                            "xpaths": [
                                "string"
                            ],
                            "formId": "string",
                            "id": "string",
                            "name": "string",
                            "formName": "string"
                        }
                    }
                ],
                "fixHtml": "boolean",
                "javascriptDisabledForLastAction": "boolean",
                "maxPages": "integer",
                "javascriptWhitelist": "string",
                "infiniteScrollPages": "integer",
                "prerendered": "boolean",
                "http10": "boolean",
                "url": "string",
                "browserActions": [
                    {
                        "domain": "string",
                        "format": "string",
                        "input": "string",
                        "type": "string",
                        "inputType": "string",
                        "value": "object",
                        "element": {
                            "xpaths": [
                                "string"
                            ],
                            "formId": "string",
                            "id": "string",
                            "name": "string",
                            "formName": "string"
                        }
                    }
                ],
                "paginationRequests": [
                    "string"
                ],
                "paginationXPaths": [
                    "string"
                ],
                "type": "object",
                "privileged": "boolean",
                "crawler": "boolean"
            },
            "queryType": "object"
        }
    },
    "schema": {
        "inputProperties": [
            {
                "defaultValue": "object",
                "type": "string",
                "domain": "string",
                "name": "string"
            }
        ],
        "guid": "string",
        "outputProperties": [
            {
                "defaultValue": "object",
                "type": "string",
                "domain": "string",
                "name": "string"
            }
        ]
    }
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
publishRequestGuid | string | 
tests | [ConnectorVersionTests](#connectorversiontests) | 
guid | string | 
runtimeConfiguration | [ConnectorVersionRuntimeConfiguration](#connectorversionruntimeconfiguration) | 
schema | [Schema](#schema) | 

	
## DataPackageSubscription
```json
{
    "status": "string",
    "packageSchemaName": "string",
    "packageName": "string",
    "expires": "integer",
    "scheduleEffectiveOn": "integer",
    "scheduleDaysOfWeek": "string",
    "packageGuid": "string",
    "scheduleTimesOfDay": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
status | string | 
packageSchemaName | string | 
packageName | string | 
expires | integer | 
scheduleEffectiveOn | integer | 
scheduleDaysOfWeek | string | 
packageGuid | string | 
scheduleTimesOfDay | string | 

	
## Labels
```json
[
    {
        "guid": "string",
        "label": "string"
    }
]
```
	
### Fields
Name | Type | Description
--- | --- | ---

	
## Scraper
```json
{
    "resultRegexp": "string",
    "resultPipeline": [
        {
            "type": "object"
        }
    ],
    "errorXPaths": [
        "string"
    ],
    "resultXPaths": [
        "string"
    ],
    "noResultsRegExp": "string",
    "ignoreFirst": "integer",
    "singleResultPipeline": [
        {
            "type": "object"
        }
    ],
    "namespaces": "object",
    "noResultsXPaths": [
        "string"
    ],
    "errorRegexp": "string",
    "totalResultsRegExp": "string",
    "totalResultsXPaths": [
        "string"
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
resultRegexp | string | 
resultPipeline | array[[PipelineStageConfig](#pipelinestageconfig)] | 
errorXPaths | array[string] | 
resultXPaths | array[string] | 
noResultsRegExp | string | 
ignoreFirst | integer | 
singleResultPipeline | array[[PipelineStageConfig](#pipelinestageconfig)] | 
namespaces | object | XPath prefix =&gt; XML namespaces
noResultsXPaths | array[string] | 
errorRegexp | string | 
totalResultsRegExp | string | 
totalResultsXPaths | array[string] | 

	
## Snapshots
```json
{
    "snapshots": [
        {
            "snapshotAt": "integer",
            "previousSnapshotAt": "integer",
            "guid": "string",
            "snapshotBuildCompletedAt": "integer",
            "snapshotBuildStartedAt": "integer",
            "includedSourceIds": [
                "string"
            ],
            "packageId": "string",
            "excludedSources": [
                {
                    "sourceId": "string",
                    "reason": "string"
                }
            ],
            "totalObjects": "integer"
        }
    ]
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
snapshots | array[[DataPackageSnapshotResponse](#datapackagesnapshotresponse)] | 

	
## DataSourceConfigDelegatedExtractionStrategy
```json
{
    "configuration": "object",
    "systemId": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
configuration | object | 
systemId | string | 

	
## Meta
```json
{
    "lastEditorGuid": "string",
    "timestamp": "integer",
    "orgGuid": "string",
    "objectGuid": "string",
    "creationTimestamp": "integer",
    "creatorGuid": "string",
    "patchTimestamp": "integer",
    "ownerGuid": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
lastEditorGuid | string | 
timestamp | integer | 
orgGuid | string | 
objectGuid | string | 
creationTimestamp | integer | 
creatorGuid | string | 
patchTimestamp | integer | 
ownerGuid | string | 

	
## Result
```json
"object"
```
	
### Fields
Name | Type | Description
--- | --- | ---

	
## User
```json
{
    "username": "string",
    "_meta": {
        "lastEditorGuid": "string",
        "timestamp": "integer",
        "orgGuid": "string",
        "objectGuid": "string",
        "creationTimestamp": "integer",
        "creatorGuid": "string",
        "patchTimestamp": "integer",
        "ownerGuid": "string"
    },
    "roles": [
        "string"
    ],
    "orgGuid": "string",
    "guid": "string",
    "email": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
username<b title="required">&nbsp;*&nbsp;</b> | string | 
_meta | [Meta](#meta) | 
roles<b title="required">&nbsp;*&nbsp;</b> | array[string] | 
orgGuid<b title="required">&nbsp;*&nbsp;</b> | string | 
guid<b title="required">&nbsp;*&nbsp;</b> | string | 
email<b title="required">&nbsp;*&nbsp;</b> | string | 

	
## Query
```json
{
    "proxyPort": "integer",
    "connectorVersionGuid": "string",
    "cookies": [
        "string"
    ],
    "format": "string",
    "returnPaginationSuggestions": "boolean",
    "proxyPassword": "string",
    "proxyHost": "string",
    "proxyUsername": "string",
    "input": "object",
    "userAgent": "string",
    "page": "integer"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
proxyPort | integer | 
connectorVersionGuid | string | 
cookies | array[string] | 
format | string | 
returnPaginationSuggestions | boolean | 
proxyPassword | string | 
proxyHost | string | 
proxyUsername | string | 
input<b title="required">&nbsp;*&nbsp;</b> | object | The query input
userAgent | string | 
page | integer | 

	
## QueryLoginInput
```json
{
    "username": "string",
    "password": "string"
}
```
	
### Fields
Name | Type | Description
--- | --- | ---
username<b title="required">&nbsp;*&nbsp;</b> | string | 
password<b title="required">&nbsp;*&nbsp;</b> | string | 

	
