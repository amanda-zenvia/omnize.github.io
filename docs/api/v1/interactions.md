## ClientApi V1
To get access token and set webhook url to receive, access:
```
https://zchat-admin.zenvia.com
```
Go to:
```
Menu > Settings > Integrations > ClientSDK
```
Click on 'Generate Token' to obtain a new one, after that set the 'Webhook URL' to receive the triggers events.

#### Get Departments
Make **GET** HTTP request:
```
https://zchat.zenvia.io/api/external/departments?token={yourClientSdkToken}
```
Parameter  | Required |
------------  | ------------- |
token | **true** |

#### Start interaction
Make **POST** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions
```
Body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |
department_id | integer | **true** | any active department_id from your account |
media_type | string | false | TEXT, SMS, WHATSAPP  **(null will be saved as TEXT)** |
extra | object | false | any parameters **(will be returned on webhook)** |
customer | object | false | { "phone", "cpf", "name", "email" } |
external_history | string | false | valid url that GET a JSON |

Example:
```
{
  "token": "y0urC1ientSdkT0ken",
  "media_type": "TEXT",
  "department_id": 1,
  "customer": {
    "name": "Name Surname",
    "email": "nameo@example.com",
    "phone": "11991417777",
    "cpf": "12345678900"
  },
  "extra" : {
    "clientId": "any",
    "botId": "parameter"
  },
  "external_history": "https://test.com"
}
```
Valid Response:
```
{
  "message": "Interaction created successfully",
  "data": {
    "interaction_hash": "0000a-000b-0c00-0d0e-f00d00f11111"
  }
}
```

Error Response:
```
{
    "message": "Error description here",
    "status": 422
}
```

#### External History
Endpoint that **GET** a JSON:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
messages | array of objects | **true** | objects with "time", "direction" and "content"|

Messages Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
time | datetime | **true** | any datetime |
direction | string | **true** | CLIENT, AGENT |
content | string | **true** | any string |

Example:
```
{
  "messages":[
    {
      "time":"2019-03-14 00:00:01",
      "direction":"CLIENT",
      "content":"client message here"
    },
    {
      "time":"2019-03-14 00:00:10",
      "direction":"AGENT",
      "content":"agent answer here"
    }
  ]
}
```

#### Update interaction
Make **PUT** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interaction_hash}
```
Body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token
mood | string | false | "POSITIVE", "NEGATIVE"
tag_ids | array | false | your tag_ids
customer_key | string | false | your existing customer
note | string | false | any string

Example:
```
{
  "token": "y0UrCl1EntSdk",
  "mood": "POSITIVE",
  "tag_ids": ["1", "999"],
  "customer_key": "0010-abcd-efgh-ijkd-1c422e49fdff",
  "note": "any note here"
}
```

Valid Response:
```
{
    "message": "Interaction updated successfully",
    "status": 200
}
```
Error Response:
```
{
    "message": "Error description here",
    "status": 422
}
```

#### Send message
Make **POST** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interaction_hash}/messages
```
body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |
content | string | **true** | any string |
type | string | false | text, image, video, audio, file **(null will be saved as text)** |

Example:
```
{
  "token": "yourC1ientSdkT0ken",
  "content": "your message",
  "type": "image",
  "url": "https://omz-logos.s3.amazonaws.com/logo_omz.png"
}
```
Valid Response:
```
{
    "data": {
        "interaction_hash": "interaction_hash"
    },
    "message": "Message created successfully",
    "status": 200
}
```
Error Response:
```
{
    "message": "Error description here",
    "status": 422
}
```

#### Notify when client typing
Make **PUT** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interaction_hash}/typing
```
body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |

#### Notify when client stop typing
Make **PUT** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interaction_hash}/cleared
```
body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |


#### Finish interaction
Make **PUT** HTTP request:
```
https://zchat.zenvia.io/core/api/v1/interactions/{interaction_hash}/finish
```
body:

Parameter | Type | Required | Valid Attributes |
------------ | ------------- | ------------- | ------------- |
token | string | **true** | your clientSdk token |


## Triggers

#### Interaction added to queue

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "queued",
      "position": 1,
      "extra": {}
    }

#### Agent accepts interaction

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "accepted",
      "extra": {}
    }

#### In case of unavailable agents:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "unavailable",
      "extra": {}
    }

####  Agent finish interaction:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "finished",
      "extra": {}
    }

####  Agent typing:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "typing",
      "extra": {}
    }

####  Agent stop typing:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "state": "cleared",
      "extra": {}
    }

#### Agent new message:

    {
      "interaction_hash": "322e458c-540c-4c11-ab5c-d38d39f57213",
      "message": {
        "hash": "3110a5da-87c7-4f6d-a4ab-2b1ed5edfd46",
        "content": "Message",
        "type": "text",
        "url": "http://..."
      },
      "agent": {
        "id": 111,
        "name": "Atendente"
      },
      "extra": {}
    }
