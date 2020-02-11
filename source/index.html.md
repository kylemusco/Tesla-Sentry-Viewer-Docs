---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript
  - python

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Accounts

All `POST` requests are expected as `application/json` 

## Authenticate

> Successful authentication returns the following JSON

```json
{
  "apiKey": "User's API Key"
}
```

### HTTP Request

`POST https://teslasentryviewer.herokuapp.com/authenticate`

Parameter | Description
--------- | -----------
email | User's email address
password | User's password

## Register

> Successful registration returns the following JSON

```json
{
  "apiKey": "User's API Key"
}
```

### HTTP Request

`POST https://teslasentryviewer.herokuapp.com/register`

Parameter | Description
--------- | -----------
email | Needs to be valid email
password | Needs to be at least 8 characters long


# Videos

## Get User's Videos

```javascript
// Example request to get user's videos in NodeJS
const rp = require('request-promise');
rp({
  url: "https://teslasentryviewer.herokuapp.com/videos",
  headers: {
    "apiKey": "User's API key"
  }
})
.then( response => {
  // response will contain JSON object with an array of user's videos or error message
});
```
```python
# Eample request to get user's videos in Python
import requests

url = "https://teslasentryviewer.herokuapp.com/videos"

payload = {}
headers = {
  'apiKey': 'API Key'
}

response = requests.request("GET", url, headers=headers, data=payload)
```

> Successful request returns the following JSON

```json
{
  "videos": [
    {
      "url": "https://teslasentryviewer.s3.amazonaws.com/eee00a971a984930cb1e7babb1d04bff.mp4?AWSAccessKeyId=AKIAI3FAKMJFM54SABTQ&Expires=1581280948&Signature=mplV0zNG2b9EfGir4HqOjdMDD4I%3D",
      "date": 1581279896241
    },
    {
      "url": "https://teslasentryviewer.s3.amazonaws.com/e3ac30af41749097b1c85c90caae3304.mp4?AWSAccessKeyId=AKIAI3FAKMJFM54SABTQ&Expires=1581280948&Signature=ADXFXdbATP%2B1uA9iI7H9H9Rpptc%3D",
      "date": 1581279954841
    }
  ]
}
```

Returns a JSON object containing an array of user's videos

### HTTP Request

`GET https://teslasentryviewer.herokuapp.com/videos`

<aside class="notice">
This endpoint requires an API key
</aside>

## Upload Video

```javascript
// Example request to upload a video in NodeJS
const rp = require('request-promise');
const fs = require('fs');
const options = {
  "method": "POST",
  "url": "https://teslasentryviewer.herokuapp.com/upload",
  "headers": {
    "Content-Type": "application/x-www-form-urlencoded",
    "apiKey": "API key"
  },
  formData: {
    "video": {
      "value": fs.createReadStream("Full path to video"),
      "options": {
        "filename": "Name of file with extension"
      }
    },
    "location": "Joe's apartment",
    "latitude": 39.882531,
    "longitude": -76.798357
  }
};

rp(options)
.then( response => {
  // response will be HTTP 200 if successful or object containing error message
});
```
```python
# Example request to upload a video in python
import requests

url = "https://teslasentryviewer.herokuapp.com/upload"

payload = {}
files = [
  ('video', open('Full path to video file','rb'))
]
headers = {
  'Content-Type': 'application/x-www-form-urlencoded',
  'apiKey': 'API Key'
}

response = requests.request("POST", url, headers=headers, data=payload, files=files)
```

> Successful request returns HTTP 200

Endpoint for uploading new sentry videos 

### Form Parameters
Parameter | Description
--------- | ----------- 
video | Sentry video file
location | User specified location name 
latitude | lat as double
longitude | lon as double

### HTTP Request

`POST https://teslasentryviewer.herokuapp.com/upload`

<aside class="notice">
This endpoint requires an API key
</aside>