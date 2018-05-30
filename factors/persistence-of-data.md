---
layout: post
permalink: persistence-of-data
---

Storing data and configuration according to Apple's guideline is crucial for your app's lifecycle, in particular when it comes to iCloud sync, upgrading to a new phone and restoring a phone from a backup.

Make sure to follow Apple's official [iOS Data Storage Guidelines](https://developer.apple.com/icloud/documentation/data-storage/index.html):

- `Documents`: Use this directory for user-generated content, it will be backed up
- `Caches`: Use this directory for data that can be regenerated
- `tmp`: Use this directory for temporary files
- Make use of the `do not back up` attribute for files

Never store sensitive user-information (like passwords or sessions) in those directories. Instead use the Keychain API.

The Keychain API gives you control of how data is being stored on device. Make sure you have a good understanding of how the [various attributes](https://developer.apple.com/documentation/security/keychain_services/keychain_items/item_attribute_keys_and_values) affect the lifecycle of your app.

One often overlooked question you should ask yourself: When the user upgrades to a new iOS device, should the data (e.g. login session) be migrated as well?

If you use [`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly) the data won't be included in the iCloud or iTunes backup, meaning the user will lose the data when they upgrade their device.
