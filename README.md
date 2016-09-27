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

 1. [Create an exclusion list](#creating-a-campaign).
 2. [Create a campaign](#creating-a-campaign).
 3. [Deploy our tag](#deploying-our-tag).

## Creating an exclusion list

Exclusion lists are used to specify users to exclude from campaigns.

Clients cannot currently create exclusion lists programmatically.

In the meantime, please reach out and we will provide you an exclusion-list ID.

## Creating a campaign

Clients cannot currently manage campaigns programmatically.

In the meantime, please reach out and we will provide you a campaign ID.

## Deploying our tag

You can load our tag from the following URL:
```
https://static.traversedlp.com/v1/retargeting.js
```

This instantiates a `TraverseRetargeting` singleton. Call it when:

  1. You want to [include someone in a campaign](#inclusion).
  2. You want to [exclude someone from a campaign](#exclusion).
  3. Someone [converts](#conversion).

For example:
```html
<script src="https://static.traversedlp.com/v1/container/traverse-container.js" type="text/javascript"></script>
```

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

### Conversion

Users who convert will automatically be excluded from the campaign.

To report a conversion, pass the `conversion` method an object with the following properties:

| Property | Description | Required |
| -------- | ----------- | -------- |
| `campaignId` | Campaign ID | Yes |
| `email` | Email address (*N.B.* we will hash before submitting) | No |
| `emailMd5Lower` | MD5 hash of trimmed, lowercased email address | No |
| `emailSha1Lower` | SHA-1 hash of trimmed, lowercased email address | No |
| `goal` | Conversion goal (*e.g.* `"register"`, `"subscribe"`, `"purchase"`, *etc.*) | No |

*Note:* Conversion goals and (hashed) email addresses are optional, but enable more-detailed reporting.

For example:

```javascript
TraverseRetargeting.conversion({
  campaignId: "YOUR-CAMPAIGN-ID-HERE",
  emailMd5Lower: "ba9d46a037766855efca2730031bfc5db095c654",
  goal: "purchase"
});
```
