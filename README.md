# Traverse Email Retargeting Advertiser Documentation

## Contents

  1. [Overview](#overview)
  2. [Getting started](#getting-started)
  3. [Creating a campaign](#creating-a-campaign)
  4. [Deploying our tag](#deploying-our-tag)
    1. [Initialization](#initialization)
    2. [Inclusion](#inclusion)

## Overview

Traverse Email Retargeting allows you to send email advertisements to anonymous website visitors.

## Getting started

To get started with Traverse Email Retargeting:

 1. [Create a campaign](#creating-a-campaign).
 2. [Deploy our tag](#deploying-our-tag).

## Creating a campaign

*Creating campaigns programmatically is not yet supported.*

In the meantime, please <a href="mailto:Traverse Operations <operations@traversedlp.com&gt">contact us</a> and we will provide you a campaign ID.

## Deploying our tag

Load our tag from the following URL:
```
https://static.traversedlp.com/v1/retargeting.js
```

For example:
```html
<script src="https://static.traversedlp.com/v1/retargeting.js" type="text/javascript"></script>
```

This instantiates a `TraverseRetargeting` singleton. After [initializing](#initialization), you can [include a user in a campaign](#inclusion). 

### Initialization

Before using the `TraverseRetargeting` singleton, it must be initialized with your client ID:

```javascript
TraverseRetargeting.init({
  clientId: "YOUR-CLIENT-ID-HERE"
});
```

### Inclusion

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

### Exclusion

To exclude a user from campaigns, pass the `exclude` method an object with the following properties:

| Property | Description | Required |
| -------- | ----------- | -------- |
| `campaignId` | Campaign ID | Yes |
| `email` | Email address (*N.B.* we will hash before submitting) | No |
| `emailMd5Lower` | MD5 hash of trimmed, lowercased email address | No |
| `emailSha1Lower` | SHA-1 hash of trimmed, lowercased email address | No |

Notes:

 1. (Hashed) email addresses are optional, but enable more-accurate exclusion.
 2. Users who convert should typically be excluded.

For example:

```javascript
TraverseRetargeting.exclude({
  campaignId: "YOUR-CAMPAIGN-ID-HERE",
  emailMd5Lower: "ba9d46a037766855efca2730031bfc5db095c654"
});
```
