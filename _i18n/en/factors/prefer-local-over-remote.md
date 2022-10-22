In the recent years, some development teams started using approaches that require less development work, on the expense of the user's app experience by moving more logic to a remote backend and having the iOS app be a thin client showing the server results. This approach results in user frustration when the app is used in a situation with a less than perfect internet connection (like in a subway, elevator or a spotty WiFi).

**An app should do as much of the business logic and calculations on-device as possible** for a variety of reasons:

- Privacy: avoid sending data to a remote server
- Speed: Sending data to a server and waiting for a response requires time and might fail (e.g. spotty WiFi)
- Data usage: users often have monthly data limits
- Scaling: If your app goes viral, you are responsible to scale the backend services up
- Battery life: Using mobile data is costly for battery life
- Reliability: Some countries still have unreliable LTE/3G connections

Most iOS apps require some kind of backend for certain tasks, like authentication, more complex calculations or storing of content.

**Limit the number of tasks that run on the backend to a minimum to enhance the end-user's experience and to protect their privacy.**

All parts of the app that don't necessarily **need** an internet connection (e.g. login) should work without any internet connection at all:

- Your app's startup screen ([that shouldn't exist in the first place](https://developer.apple.com/design/human-interface-guidelines/patterns/launching/)) should never wait for the first successful web response, as this causes bad UX for users with a spotty internet connection.
- If your app requires an internet connection for everything (e.g. social networking app or ride sharing app), your app should still work (in read-only mode) without an internet connection to access historic data (e.g. recent rides, recent direct messages).
- Any feature of your app that needs a working internet connection should show a clear error message that the server couldn't be reached.
- As WiFi hotspots might require a login or confirmation of some sorts (e.g. hotel or airport), HTTPS requests will often get stuck and time-out after about a minute. Until Apple resolves this issue on a system level, we as developers have to make sure to properly handle those situations.
- Never assume a user has a working internet connection on the first launch of the app. The user might install your app and then doesn't open it until they're on the go without an internet connection. You are responsible for shipping your app in a state that it works out of the box with the most up to date resources during deploy time. This directly plays together with the weekly release trains described in the [deployment](/deployment) factor.
