# Design Principles

Traditionally, end-to-end tests on mobile are riddled with inherent issues, making the testing process difficult and lowering ROI for developers. We believe that the only way to solve these issues at the core is by changing some of the basic principles of our approach.

* **Detox does not rely on WebDriver**—Detox is built from the ground up to integrate with native layers of your mobile app directly. We try to avoid generic cross-platform interfaces that are often the lowest common denominator. We want to optimize per platform.

* **Detox does gray box, not black box** — Theoretically, it sounds better to test exactly what you ship as a black box. In practice, switching to gray box allows the test framework to monitor the app from the inside and delivers critical wins like fighting flakiness at the core.

* **Detox relies on EarlGrey and Espresso** — The leading native gray box drivers are developed by Google - EarlGrey for iOS and Espresso for Android. Detox relies on them using a JSON-based reflection mechanism which allows a common JavaScript implementation to invoke their native methods directly.

* **Detox synchronizes with your app's activity** — By being aware of what your app is doing and synchronizing it, Detox times its actions to run only when your app is idle, meaning it has determined that your app has finished work, such as React Native load, animations, network requests, etc. You can further read on this [here](https://github.com/wix/Detox/blob/master/docs/Troubleshooting.Synchronization.md).

* **Friendly Protractor-like API for tests** — Tests in Detox are implemented in human-readable JavaScript and can even be shared between platforms. This easy to use API completely abstracts the complex native driver invocations taking place under the hood.

* **Detox controls devices through low-level APIs** — Let's take iOS simulators for example, which are difficult to control efficiently since multiple concurrent instances aren't supported. Detox uses [AppleSimulatorUtils](https://github.com/wix/AppleSimulatorUtils) (another opensource library by Wix) to work around these issues and support test sharding.

* **Built from the ground up for mobile and React Native** — Detox is inspired by web testing methodologies but is not a direct translation of a solution designed for a different platform. Detox is built from the ground up for native mobile and has deep first-class support for React Native apps.

* **Detox relies on websockets for communication** — Communication between the test script running on Node.js and the tested app running on device uses websockets. This provides true bi-directional communication and is much faster and resilient than REST-like protocols.

* **Both tester and testee are websocket clients** — The test script running on Node.js and the tested app running on device are both clients. This allows one side to disconnect without affecting the other. A separate proxy websocket server is used to connect them.

* **Expectations run on the testee, not the tester** — Traditionally, test frameworks evalutate expectations in the test script running on Node.js. Detox evaluates expectations natively directly in the tested app running on device. This enables operations that were impossible before due to performance reasons.
