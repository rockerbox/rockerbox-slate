---
title: API Reference

language_tabs:
  - shell
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - api/action
  - api/funnel
  - api/onsite
  - api/udf
  - api/cache

  - errors


search: true
---

# Crusher

Crusher allows you to look at the on-site activity user and determine how the on-site activity is influenced by a users off-site browsing activity.
These are the APIs that power crusher and make it possible to analyze on-site versus off-site activity.

## Background

Crusher is a collection of analytics, machine learning and ad-buying technologies that make it possible for a user to: 

- collect information about on-site and off-site activity
- classify and understand how these behaviors influence each other
- target ads based on these different classifications 

## Important Terms

These are standard terms that are used when referring to different components within crusher. 
They allow us to use common language when thinking about how different pieces of crusher are related to on another.

### Event

```
# Example of an event
```

An event is an atomic unit of interaction on an advertisers website. Currently this is limited to page views and conversions but may expand in the future to include javascript triggered events such as expanding images, scrolling, etc. 

### Action

```
# Example of an action
```

An action is a group of events that are all related to the same functionality. For instance, an action may be used to describe all landing pages, even though the individual url for each landing page is different. 

### Funnel

```
# Example of a funnel
```

A funnel is a group of actions that occur (often sequentially) that is used to predict a goal. For instance, a user that visits a landing page, a product page and converts would represent a funnel.

# Authentication

## Authorization

Most of our APIs require authentication. We demonstrate here how to login using cookie-based authentication.

To log in, send a `POST` request to `crusher.getrockerbox.com/login` with an object containing the username and password assigned to you by Rockerbox.

> Use the `/login` endpoint, saving your cookie in a file to use for future requests

```shell
cat <<EOF > creds
{
    "username": "my_user", 
    "password": "my_pw"
}
EOF

curl -b cookie -c cookie -X POST -d @creds "crusher.getrockerbox.com/login"
```

### HTTP Request

`POST http://crusher.getrockerbox.com/login`

### Request Payload

Formatted as a json object, you must include the following values as part of your `POST`:

Key | Description
--- | -----
username | the username that was provided by Rockerbox upon receiving your account
password | the password that was provided by Rockerbox upon receiving your account


#### Cookie-based



For cookie-based login, you will need to have the cookies that we set as a result of this request included on future requests. 
If using curl, use the `-b` and `-c` options to read/write your cookie from disk.

#### Header-based

Rick doesn't like APIs that don't have this as an option, so we're going to make this a thing...at some point.

## Permissions

> Request

```shell
curl -b cookie -c cookie "crusher.getrockerbox.com/account/permissions"
```

> Response

```json
{
    "results": [
        {
            "external_advertiser_id": 987654,
            "pixel_source_name": "examle_advertiser_1",
            "advertiser_name": "Example Advertiser One",
            "selected": true
        },
        {
            "external_advertiser_id": 123456,
            "pixel_source_name": "example_advertiser_2",
            "advertiser_name": "Example Advertiser Two",
            "selected": false
        }
    ]
}
```

Once authenticated, you can use `/account/permissions` to view the advertisers you have access to.





