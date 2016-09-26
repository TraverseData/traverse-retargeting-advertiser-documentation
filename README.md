# Traverse Email Retargeting Advertiser API

## Contents

  1. [Overview](#overview)
  2. [Getting started](#getting-started)
  3. [Creating a campaign](#creating-a-campaign)
  4. [Deploying our tag](#deploying-our-tag)
    1. [Inclusion](#inclusion)
    2. [Exclusion](#exclusion)
    3. [Conversion](#conversion)

## Overview

Traverse Email Retargeting allows you to send email advertisements to anonymous website visitors.

## Getting started

To get started with Traverse Email Retargeting:

 1. [Create a campaign](#creating-a-campaign).
 2. [Deploy our tag](#deploying-our-tag).

## Creating a campaign

To set up a campaign, please send us:

  1. Your creative.
  2. Your exclusion list of (hashed) email addresses, if any.

We will then provide you:

  1. A campaign ID.
  2. An exclusion-list ID.

*Note:* We will release a UI and our internal API after MVP.

## Deploying our tag

You can load our tag from the following URL:
```
http(s)://static.traversedlp.com/v1/retargeting.js?clientId={clientId}
```

This instantiates a `TraverseRetargeting` object. Call it when:

  1. You want to [include someone in a campaign](#inclusion).
  2. You want to [exclude someone from a campaign](#exclusion).
  3. Someone [converts](#conversion).

For example:
```html
<script src="https://static.traversedlp.com/v1/container/traverse-container.js?clientId=YOUR-CLIENT-ID-HERE" type="text/javascript"></script>
<script type="text/javascript">
TraverseRetargeting.include({
  campaignId: "YOUR-CAMPAIGN-ID-HERE"
});
</script>
```

### Inclusion

To include a user in a campaign, use the `include` method:

```javascript
TraverseRetargeting.include({
  campaignId: "YOUR-CAMPAIGN-ID-HERE"
});
```

### Exclusion

To exclude a user from your campaigns, use the `exclude` method:
```javascript
TraverseRetargeting.exclude({
  blacklistId: "YOUR-EXCLUSION-LIST-ID-HERE"
});
```

### Conversion

To report a conversion, use the `conversion` method:
```javascript
TraverseRetargeting.conversion({
  campaignId: "YOUR-CAMPAIGN-ID-HERE",
});
```
