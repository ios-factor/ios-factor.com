The App Store doesn't natively allow rollbacks, so this section describes how to achieve similar results, using the technology we have available.

#### Phased Releases

Using phased releases, you can slowly rollout a build to production, starting with a subset of the active users. The main benefit of this approach is the built-in way to pause a rollout, before it reaches a high amount of users, allowing you to replace the binary.

However even with phased releases, there is no way to completely revoke a build: Once a build is installed on a user's device, the only way to change that build is to distribute a new one with an updated version/build number.

#### [Recommended]: Version bump & Release

Just like with phased releases, App Store and TestFlight builds can only be updated by doing the following:

1. Go back in your version control system to a state you want to rollback to
1. Increment the version and/or build number of your project
1. Build and codesign your application
1. Distribute your app through a beta testing service or App Store
1. User has to update the app on their phone

The above steps can be done manually, however it is recommended to fully automate the process to be able to react fast.

#### [Alternative]: Resign an old build

An alternative approach that some teams might want to pick up

1. Access an old build (`.ipa` file) before the regression was introduced
1. Update the version/build number in the `Info.plist` file
1. Resign the build
1. Distribute it as a new build

However, resigning iOS apps often introduces more problems, especially since the Xcode command line tools offer no good way to do so. The iOS community ended up building and maintaining various open source shell scripts that aim to resign iOS binaries, one example can be found in the [fastlane resign feature source code](https://github.com/fastlane/fastlane/blob/master/sigh/lib/assets/resign.sh). The file grew within the last 7 years to a total of over 800 LOC, mostly due growing complexities of binaries, like multiple targets and new entitlements.


