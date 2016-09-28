# Traverse Email Retargeting Advertiser Documentation

## Contents

  1. [Overview](#overview)
  2. [Getting started](#getting-started)
  3. [Creating a campaign](#creating-a-campaign)
  4. [Deploying our tag](#deploying-our-tag)
    1. [Initialization](#initialization)
    2. [Inclusion](#inclusion)
    3. [Exclusion](#exclusion)

## Overview

Traverse Email Retargeting allows you to send email advertisements to anonymous website visitors.

## Getting started

To get started with Traverse Email Retargeting:

 1. [Create an exclusion list](#creating-a-campaign).
 2. [Create a campaign](#creating-a-campaign).
 3. [Deploy our tag](#deploying-our-tag).

## Creating an exclusion list

Exclusion lists are used to exclude users from campaigns.

*Creating exclusion lists programmatically is not yet supported.*

In the meantime, please <a href="mailto:Traverse Operations <operations@traversedlp.com&gt">contact us</a> and we will provide you an exclusion-list ID.

## Creating a campaign

*Managing campaigns programmatically is not yet supported.*

In the meantime, please <a href="mailto:Traverse Operations <operations@traversedlp.com&gt">contact us</a> and we will provide you a campaign ID.

## Deploying our tag

Load our tag from the following URL:
```
https://static.traversedlp.com/v1/retargeting.js
```

For example:
```html
<script src="https://static.traversedlp.com/v1/container/traverse-retargeting.js" type="text/javascript"></script>
```

This instantiates a `TraverseRetargeting` singleton. You can use it to:

  1. [Include a user in a campaign](#inclusion).
  2. [Exclude a user from campaigns](#exclusion).

### Initialization

Before using the `TraverseRetargeting` singleton, it must be initialized with your client ID.

For example:

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

### Exclusion

To exclude a user from campaigns, add them to an exclusion list:

```javascript
TraverseRetargeting.exclude({
  exclusionListId: "YOUR-EXCLUSION-LIST-ID-HERE"
});
```
