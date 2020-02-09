---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Accounts

All `POST` requests are expected as `application/json` 

## Register

> Successful registration returns the following JSON

```javascript
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


## Authenticate

> Successful authentication returns the following JSON

```javascript
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