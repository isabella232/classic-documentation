---
template: page-sidebar
title: "Token based"
---

# Classic Token based authentication

<div class="attention attention--warning push--bottom">
  The tokens described below only work for the v1 API. Use
  <a href="/x/authentication/personal-token">Personal Tokens</a>
  for the v2 API.
</div>

<div class="attention attention--warning push--bottom">
  Visit <a target="_blank" href="https://app.optimizely.com/tokens" name"_">app.optimizely.com/tokens</a>
  to generate an API token.
</div>

To authenticate, use a token generated from the link above in the request header, as shown in the example below. All API request examples in this documentation use the same header.

```bash
curl \
  -H "Token: abcdefghijklmnopqrstuvwxyz:123456" \
  "https://www.optimizelyapis.com/experiment/v1/projects/"
```

You can also write applications that authenticate with the REST API via OAuth 2.0. For more details on connecting applications via OAuth 2.0, refer to our [OAuth 2.0 documentation](/oauth).

Using the wrong token, or including the token in the request body rather than the header, will fail with error `Authentication Failed`.
