# Response format

## Fields
Response is currently always in JSON (but we might support XML and JSONP if there will be someone who might use it). Response always has these fields:

| Field   | Purpose                                  | example content      |
|---------|------------------------------------------|----------------------|
| code    | Contains the HTTP code                   | `200`                |
| message | A string containing sample message.      | `Success, see type.` |
| type    | A string with the type of returned data  | `ping_response`      |

Response may have additional fields, such as `url` or `data`. These depends on the type.

## Types

Types that start with `e_` are *always* errors. The following type can be retrieved:


### `e_invalid_key` | Key-only endpoints
 The key given is invalid and cannot be used.

### `e_missing_query` | *
 Request lacks GET query string, which is required by the endpoint.

### `e_invalid_query` | *
 Request has invalid fields/missing fields/invalid values. See `message` in the response for more information.

### `e_empty_response` | *
 Request succeeded, but the response provided by the endpoint was empty.

### `e_cannot_get` | *
 Request failed while trying to fetch external data.

### `e_generic` | *
 Unknown error.

### `e_ester_error`  | Ester
 An error occured inside Ester API. See `data` field (contains response from Ester API).

### `e_bakalari_missing_school` | Bakalari
 Error occured during fetching data from the given domain, which usually means the schoold doesn't exists or has private API (currently no known school has private API).

### `e_bakalari_missing_user` | Bakalari
 Request to school succeeded, but the user doesn't exists.

### `e_missing_subreddit` | Reddit
 Couldn't fetch subreddit. Subreddit may be NSFW (which are currently unsupported) or private or just simply doesn't exists.

### `e_reddit_failed` | Reddit
 Reddit returned invalid response and/or error response.

### `e_neko_type` | Nekos
 Unknown neko type.
 
-----

 > Example response:

 ```json
 {
     "code": 200,
     "message": "Success, nothing to do",
     "type": "generic"
 }
 ```

### `generic` | *

 A response containing only the default 3 fields.
 
<br>
<br>
<br>
<br>

 > Example response:

 ```json
 {
     "code": 200,
     "message": "Success, see types",
     "type": "neko_list",
     "types": [ "..." ]
 }
 ```

### `neko_list` | Nekos

 List of available `neko` endpoints.

<br>
<br>
<br>
<br>
<br>

 > Example response:

 ```json
 {
     "code": 404,
     "message": "ICe API in development, see later",
     "type": "ice_response",
     "data": {}
 }
 ```

### `ice_response` | Ice

 A generic bot response.

<br>
<br>
<br>
<br>
<br>

 > Example response:

 ```json
{
    "code": 200,
"type": "ice_http_code_response",
"http": {
    "standart": true,
    "title": "OK",
    "description": "Standard response for successful HTTP requests. The actual response will depend on the request method used.  In a GET request, the response will contain an entity corresponding to the requested resource. In a POST request, the response will contain an entity describing or containing the result of the action.",
    "choices": []
},
"source": "Wikipedia"
}
 ```

### `ice_http_code_response` | Http

 A response containing information about given http code.

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


 > Example response:

 ```json
{
  "code": 400,
  "message": "Missing parameter code. Use it as /http/:code",
  "type": "e_ice_http_missing_code"
}
 ```

### `ice_http_code_list` | Ice

 A *planned* response to list all available HTTP codes.

<br>
<br>
<br>
<br>

### `pushr_response` | Pushr
 A response from Pushr API (danbulant.eu API acts as pass-through for this).

 > Example response:

 ```json
{
  "code": 200,
  "message": "Success, see reddit",
  "type": "reddit_response",
  "reddit": {
    "title": "I really ininterested",
    "image": "https://imgur.com/tLBzS1h.jpg",
    "author": "nickjayr",
    "authorIcon": "https://www.redditstatic.com/avatars/avatar_default_17_0DD3BB.png",
    "link": "https://reddit.com/r/memes/comments/ey2hkb/i_really_ininterested/"
  }
}
```

### `redddit_response` | Reddit

 Response from reddit API containing `reddit` object.

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

 > Example response:

 ```json
{
  "code": 200,
  "message": "Success, see response",
  "path": "/",
  "type": "ester_response",
  "data": {
    "code": 200,
    "message": "Čau!",
    "user": {
      "name": "Daniel",
      "id": "1"
    },
    "text": "Čau!"
  }
}
```

### `ester_response` | Ester

 A generic response from Ester API.

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

> Example response:

```json
{
  "code": 200,
  "message": "Success",
  "type": "bakalari_response",
  "data": {
    "verze": "17/18.20191219",
    "jmeno": "[NAME HIDDEN]",
    "typ": "R",
    "strtyp": "rodič",
    "skola": "[SCHOOL REDACTED]",
    "typskoly": "",
    "trida": "0.A",
    "rocnik": -1,
    "moduly": "*znamky*predvidac*rozvrh*predmety*vyuka*ukoly*akce*suplovani*absence*pololetni*prijate*odeslane*nastenka*setread*setok*komsend*komenslisty*komdel*",
    "params": {
      "newmarkdays": 1
    },
    "result": 1
  }
}
```

### `bakalari_response` | Bakalari

 Response from the `bakalari` API. Format depends on the bakalari response (e.g., try the desired info in browser to see, as danbulant.eu only converts xml to json).

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

> Example response:

```json
{
  "code": 200,
  "message": "Success, see url",
  "type": "image",
  "url": "https://i.imgur.com/wVUpmao.jpg"
}
```

### `image` | *

 Generic image response. The actual image is on adress inside the provided `url` field.

<br>
<br>
<br>
<br>
<br>
