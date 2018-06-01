---
layout: post
permalink: backwards-compatible-apis
title: Backwards Compatible APIs
---

While the majority of your end-users will update to the most recent update within a few weeks, there will always be a subset of users who won't. This can have multiple reasons. Often it is related to the iOS version they run, which they can't always update depending on how old the given iOS device is.

You can install and use Facebook Messenger on a first-generation iPad (2010). While newer features are not supported, the core functionality is still available thanks to API versioning.

The basic concept is that you don't update an existing API, but add a new one instead and let them run in parallel

```
https://your-api.com/1.0/drivers.json
https://your-api.com/1.1/drivers.json
```

You may eventually need to turn off or slightly change semantics of an API. Even if your company has a deep commitment to stability, sometimes matters of law force this change. This means you should encode an API endpoint that is queriable just to indicate the API status. 

```
https://your-api.com/1.0/status.json
https://your-api.com/1.1/status.json
```

The status API should include information such as

 - What's the stage of the API? (e.g. testing, beta, production)
 - Is the API is depreciated? If so, what date is it scheduled to be turned off?
 - Is the API offline? If so, will it remain so or is it a temporary outage?


 

