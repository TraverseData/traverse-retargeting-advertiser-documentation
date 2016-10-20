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

This instantiates a `TraverseRetargeting` singleton. After [initializing](#initialization) it, you can [include a user in a campaign](#inclusion). 

### Initialization

Before using the `TraverseRetargeting` singleton, it must be initialized with your advertiser ID:

```javascript
TraverseRetargeting.init({
  advertiserId: "YOUR-ADVERTISER-ID-HERE"
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
