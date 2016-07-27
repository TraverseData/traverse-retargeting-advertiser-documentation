# Traverse Email Retargeting Advertiser API

## Contents

  1. [Overview](#overview)
  2. [Getting started](#getting-started)
  3. [Exclusion lists](#exclusion-lists)
    1. [Creating an exclusion list](#creating-an-exclusion-list)
    2. [Exclusion-list representation](#exclusion-list-representation)
    3. [Updating an exclusion list](#updating-an-exclusion-list)
    4. [Listing your exclusion lists](#listing-your-exclusion-lists)
    5. [Excluding individual users](#excluding-individual-users)
  4. [Creating a campaign](#creating-a-campaign).
  5. [Deploying our tag](#deploying-our-tag).
  6. [Best practices](#best-practices)

## Overview

Traverse Email Retargeting allows you to send email advertisements to your anonymous website visitors.

## Getting started

To get started with Traverse Email Retargeting:

 1. [Set up your exclusion list(s)](#exclusion-lists), if any.
 2. [Create your campaign(s)](#creating-a-campaign).
 3. [Deploy our tag](#deploying-our-tag).

## Exclusion lists

In order to use an exclusion list:

 1. [Get credentials](#authentication).
 2. [Review the error-handling guidance](#error-handling).
 3. [Create a list](#creating-an-exclusion-list).
 4. [Upload its contents](#updating-an-exclusion-list).

Optionally, advanced users may also:

 * Create multiple exclusion lists (*e.g.* for different campaigns).
 * [List your exclusion lists](#listing-your-exclusion-lists).
 * *Update an exclusion list*, by repeating step 4, monthly.
 * [Add individual users to an exclusion list](#excluding-individual-users), in real time.

### Authentication

**Important!** *All API calls are authenticated via <a href="https://en.wikipedia.org/wiki/Basic_access_authentication">basic auth</a>.*

Please <a href="mailto:Traverse Operations <operations@traversedlp.com&gt">contact Traverse</a> for credentials.

### Error handling

While we make every attempt to maintain the availability of our system, unexpected errors may occur:

 1. Always check whether the HTTP status code  is *<a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#2xx_Success">2xx</a>* (success) before proceeding, and abort if not.
 2. If the status code is *<a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error">4xx</a>* (client error), your request is likely invalid. Review the documentation before retrying.
 3. If the status code is *<a href="https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_Error">5xx</a>* (server error), there is likely a problem on our end. Please retry after 60 seconds.
 4. Otherwise, treat any unexpected response, status code, timeout or exception as a *5xx*.
 5. Log your requests and replies, and monitor for and review any failures.

### Creating an exclusion list

To create an exclusion list, upload a [representation](#exclusion-list-representation), without an `id`, to:
```
POST https://retargeting.traversedlp.com/v1/blacklist
```

The response will contain an updated [representation](#exclusion-list-representation), with an `id`.

Notes:

 1. Do not include the `id`. The system will assign one for you.
 2. This just creates an empty list. You still need to [upload its contents](#updating-an-exclusion-list).
 3. Make note of the returned `id` so that you can update the list.

### Exclusion-list representation

Exclusion lists are represented by a JSON object with the following fields::

| Name          | Value                                | Required |
| ------------- |--------------------------------------|----------|
| `id`          | Traverse-generated unique identifier | No       |
| `name`        | Client-supplied name                 | No       |
| `description` | Client-supplied description          | No       |

For example:

```javascript
{
  id: "401b1f0c-0307-4efa-aab0-49f57f930572",
  name: "Acme website purchasers",
  description: "Users who have purchased from acme.com"
}
```

### Updating an exclusion list

To update an exclusion list's users, upload a CSV:
```
PUT https://retargeting.traversedlp.com/v1/blacklists/{id}/hashes
```

Format:

 1. Commas, quotes and line terminators per <a href="https://tools.ietf.org/html/rfc4180">RFC 4180</a>.
 2. A  header row, consisting of the column names, is required.
 3. <a id="f1">At least one of the `emailMdLower` or `emailSha1Lower` columns is required.</a>
 4. Additional columns should not be included, and will be ignored.

Columns:

| Name             | Value                                           | Required                |
|------------------|-------------------------------------------------|-------------------------|
| `emailMd5Lower`  | MD5 hash of trimmed, lowercased email address   | No<sup id="a1">[3](#f1) |
| `emailSha1Lower` | SHA-1 hash of trimmed, lowercased email address | No<sup id="a1">[3](#f1) |

For example:
```
emailMd5Lower,emailSha1Lower
ba9d46a037766855efca2730031bfc5db095c654,1105677c8d9decfa1e36a73ff5fb5531
52245908b2816145e7b101c4304982c6f33df9e4,380236b305e0e37b2bfae587966c34e2
```

A successful response will have a 2xx status code.

### Listing your exclusion lists

To list your exclusion lists:
```
GET https://retargeting.traversedlp.com/v1/blacklists
```

The response will include a JSON array of [representations](#exclusion-list-representation).

## Excluding individual users

In order to add an individual user to an exclusion list, upload their representation to:
```
POST https://retargeting.traversedlp.com/v1/blacklist/{id}/hash
```

Individual users on an exclusion list are represented by a JSON object with <a id="f1">(*) one or more of the following fields</a>:

| Name             | Value                                           | Required                |
|------------------|-------------------------------------------------|-------------------------|
| `email`          | Email address (see note, below)                 | No<sup id="a1">[*](#f2) |
| `emailMd5Lower`  | MD5 hash of trimmed, lowercased email address   | No<sup id="a1">[*](#f2) |
| `emailSha1Lower` | SHA-1 hash of trimmed, lowercased email address | No<sup id="a1">[*](#f2) |

*Note*: If you provide us an email address, we will compute its hashes for you, and only store the hashes.

For example:

```javascript
{
  emailMd5Lower: "ba9d46a037766855efca2730031bfc5db095c654",
  emailSha1Lower: "1105677c8d9decfa1e36a73ff5fb5531"
}
```

## Creating a campaign

To set up a campaign, please:

  1. Email us the creative.
  2. Let us know which suppression lists to use, if any.

## Deploying our tag

Load our tag from the following URL:
```
http(s)://static.traversedlp.com/v1/retargeting.js?clientId={clientId}
```

For example:

```javascript
<script src="https://static.traversedlp.com/v1/retargeting.js?clientId=YOUR-CLIENT-ID-HERE" type="text/javascript"></script>
<script type="text/javascript">
TraverseRetargeting.
});
</script>

### Inclusion
