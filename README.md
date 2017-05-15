# Traverse Email Retargeting Advertiser Documentation

## Contents

  1. [Overview](#overview)
  2. [Getting started](#getting-started)
  3. [Creating a campaign](#creating-a-campaign)
  4. [Campaign Inclusion](#campaign-inclusion)
     1. [Deploying our tag](#deploying-our-tag)
     2. [Calling our pixel](#calling-our-pixel)

## Overview

Traverse Email Retargeting allows you to send email advertisements to anonymous website visitors.

## Getting started

To get started with Traverse Email Retargeting:

 1. [Create a campaign](#creating-a-campaign).
 2. [Deploy our tag](#deploying-our-tag) or [call our pixel](#calling-our-pixel).

## Creating a campaign

*Creating campaigns programmatically is not yet supported.*

In the meantime, please <a href="mailto:Traverse Operations <operations@traversedlp.com&gt">contact us</a> and we will provide you a campaign ID.

## Campaign Inclusion

Include anonymous users in a campaign by [deploying our tag](#deploying-our-tag) or [calling our pixel](#calling-our-pixel).

| Parameter    | Description | Required |
| ------------ |------------ | -------- |
| `advertiserId` | Your provided 36-character client ID (includes hyphens). | Yes |
| `campaignId` | Your provided 36-character campaign ID (includes hyphens). | Yes |
| `advertiserProperties` | A JSON object of additional properties | No |

### Deploying our tag

Our tag is the preferred integration method. If for some reason, you can't use this, integrate by [calling our pixel](#calling-our-pixel).

Load our tag from the following URL:
```
https://static.traversedlp.com/v1/retargeting.js
```

For example:
```html
<script src="https://static.traversedlp.com/v1/retargeting.js" type="text/javascript"></script>
```

This instantiates a `TraverseRetargeting` singleton. After [initializing](#initialization) it, you can [include a user in a campaign](#inclusion). 

#### Initialization

Before using the `TraverseRetargeting` singleton, it must be initialized with your advertiser ID:

```javascript
TraverseRetargeting.init({
  advertiserId: "YOUR-ADVERTISER-ID-HERE"
});
```

#### Inclusion

To include a user in a campaign, use the `include` method:

```javascript
TraverseRetargeting.include({
  campaignId: "YOUR-CAMPAIGN-ID-HERE"
});
```

Advanced users may use the `advertiserProperties` property to pass additional data:

```javascript
TraverseRetargeting.include({
  campaignId: "YOUR-CAMPAIGN-ID-HERE",
  advertiserProperties: {
    impressionId: "5d2f8eb0-4757-48e7-9ea7-525850c22344",
    foo: "bar"
  }
});
```

### Calling our pixel

To include a user in a campaign using our pixel, load the following pixel in the user's browser, with the parameters replaced:

```
<img border="0" width="1" height="1" src="https://api.traversedlp.com/retargeting/v1/include.gif?advertiserId={{advertiserId}}&campaignId={{campaignId}}"/\>
```

Advanced users may use the `advertiserProperties` property to pass additional data. It should be a URL-encoded, serialized JSON object or have each property set like `advertiserProperties.foo`. If your advertiserProperties are `{foo: 'bar'}`, passing it in the URL would look like one of these:

Using serialized, URL-encoded JSON:
```
<img border="0" width="1" height="1" src="https://api.traversedlp.com/retargeting/v1/include.gif?advertiserId={{advertiserId}}&campaignId={{campaignId}}&advertiserProperties=%7B%22foo%22%3A%22bar%22%7D"/\>
```

Using advertiserProperties.propertyName:
```
<img border="0" width="1" height="1" src="https://api.traversedlp.com/retargeting/v1/include.gif?advertiserId={{advertiserId}}&campaignId={{campaignId}}&advertiserProperties.foo=bar"/\>
```
