---
layout: post
permalink: persistence-of-data
---

Storing data and configuration according to Apple's guideline is crucial for your app's lifecycle, in particular when it comes to iCloud sync, upgrading to a new phone and restoring a phone from a backup.

[iOS Data Storage Guidelines](https://developer.apple.com/icloud/documentation/data-storage/index.html)

- `Documents`: Use this directory for user-generated content, it will be backed up
- `Caches`: Use this directory for data that can be regenerated
- `tmp`: Use this directory for temporary files
- Make use of the `do not back up` attribute

Never store sensitive user-information (like passwords or sessions) in those directories. Use the Keychain API, which comes with various advantages:

TODO: finish