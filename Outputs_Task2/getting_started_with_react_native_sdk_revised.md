---
title: Getting Started with the MoEngage React Native SDK
---

# Getting Started with the MoEngage React Native SDK

# Overview

The MoEngage React Native SDK lets you add MoEngage features to your iOS and Android apps built with React Native.  It supports push notifications, in-app messages, cards, user attributes, events, and more.  See sample code in the [GitHub repository](https://github.com/moengage/React-Native-Sample-App). This guide explains how to implement MoEngage features in your React Native app.

# SDK Installation and Initialization

**Step 1: Installation**

To add the MoEngage React Native SDK, see the [Installation Methods](https://developers.moengage.com/hc/en-us/articles/4404205340564).

**Step 2: Android Native Setup**

Complete the Android native setup as described in this [article](https://developers.moengage.com/hc/en-us/articles/7778283953300-Android). iOS requires no additional steps. Proceed to initialization (Step 3).

**Step 3: Framework Initialization**

Initialize the MoEngage plugin using the method described in this [article](https://developers.moengage.com/hc/en-us/articles/4404205878676-Framework-Initialization#h_01H95NNGA8R8D6K6Y5QRDXEPQ6).

**Step 4: Platform Initialization**

Initialize the SDK and configure the data center using these platform-specific guides:

* [Android](https://developers.moengage.com/hc/en-us/articles/7778321669908-Android)
* [iOS](https://developers.moengage.com/hc/en-us/articles/7778302956308-iOS)

# Data Tracking

Track user behavior to improve engagement.  This includes actions like login, logout, and events.  Follow these steps to avoid data corruption:

* **Install/Update Differentiation:** Track new installs and updates separately. See this [article](https://developers.moengage.com/hc/en-us/articles/7778340663316-Install-Update).

* **Tracking Login, Logout, and Unique ID:**  Use a unique ID for each user (passed using `setUserUniqueID()`). This ensures accurate user identification across installs and platforms.  Call `logout()` when a user logs out to prevent data errors. Follow these guides:
    * [Tracking Login and Setting User ID](https://developers.moengage.com/hc/en-us/articles/4404254395924-Tracking-User-Attributes#01GP38JWB7FBZR6Y2AY5HDVMGD)
    * [Tracking Logout](https://developers.moengage.com/hc/en-us/articles/4404254395924-Tracking-User-Attributes#01GP38JWB7S4F48SWD063BJJMJ)
    * [Updating User Attribute Unique ID](https://developers.moengage.com/hc/en-us/articles/4404254395924-Tracking-User-Attributes#01GP38JWB7H48XRJA0RYNWAZT8)

* **Tracking User Attributes:** Set custom attributes in user profiles. See this [article](https://developers.moengage.com/hc/en-us/articles/4404254395924-Tracking-User-Attributes#01GP38JWB74TBR6QBQAMBGZ9M1).

* **Tracking Events:** Record user actions and their properties. See this [article](https://developers.moengage.com/hc/en-us/articles/4404254869780-Tracking-Events).

* **Enable Advertising Identifier Tracking (Android only):**  Enable tracking of the Advertising ID (AAID) after obtaining user consent. This improves push notification delivery and reinstall tracking. See this [article](https://developers.moengage.com/hc/en-us/articles/7782519973012-Enable-Advertising-Identifier-Tracking).


# Push Notifications

Send push notifications to your users. Follow the platform-specific steps below.

## Basic Setup - Android

* **FCM Setup on MoEngage Dashboard:** Authenticate MoEngage with Firebase to send push notifications. Use the methods in this [article](https://developers.moengage.com/hc/en-us/articles/16909296490644-FCM-Authentication).

* **Adding Push Notification Metadata:** Configure icons and other options. See this [article](https://developers.moengage.com/hc/en-us/articles/20128522113556-Push-Configuration-For-Hybrid-Applications#01GRNPZWD99YXM7KBVC0458YFM).

* **Android Notification Runtime Permissions:** Request notification permissions on Android 13. See this [article](https://developers.moengage.com/hc/en-us/articles/13065189737748-Android-Notification-Runtime-Permissions).

* **Push Registration and Receiving:** Configure Firebase and choose whether to handle push notifications using the MoEngage SDK (recommended) or your app.


## Basic Setup - iOS

* **APNS Setup on MoEngage Dashboard:** Configure APNS using either an authentication key (recommended) or a certificate/PEM file.
    * [APNS Authentication Key (recommended)](https://developers.moengage.com/hc/en-us/articles/8484447635348-APNS-Authentication-Key)
    * [APNS Certificate/PEM file](https://developers.moengage.com/hc/en-us/articles/4403944011028-APNS-Certificate-PEM-file)

* **App Target Implementation:** Enable notifications in your app target. See this [article](https://developers.moengage.com/hc/en-us/articles/4403930540820#h_01H92ZQDWGGWZ787NMPM1AR76A).

* **Provide the App Group ID to SDK:** Pass the App Group ID. See this [article](https://developers.moengage.com/hc/en-us/articles/4403930540820#h_01H92ZQDWGDK7956MD1QYAXR7E).

* **Push Registration and Receiving:**

    * **Disable Badge Reset:** Prevent the app from clearing notifications on launch. See this [section](https://developers.moengage.com/hc/en-us/articles/4403930540820#h_01H92ZQDWHNYPKKBJYGJVZBV8G).

    * **Custom Sound for Notification:** Set a custom notification sound. See this [section](https://developers.moengage.com/hc/en-us/articles/4403930540820#h_01H92ZQDWHKNAW4VMZ7419V44Z).

    * **Notification Service Extension Target Implementation:** Customize notification content. See this [article](https://developers.moengage.com/hc/en-us/articles/4403930540820-Push-Notification-Implementation#h_01H92ZQDWH8BSRH5WC0T4KTY2A).

    * **Notification Actions:** Add custom action buttons to notifications. See this [article](https://developers.moengage.com/hc/en-us/articles/4403961980308-Actionable-Notifications#h_01H9MM3BEEPZYF8KC4ZSKHHC3J).


## Push Templates

Create visually appealing notifications using templates.  See this guide for creating campaigns in the dashboard: [this article](https://help.moengage.com/hc/en-us/articles/4415622460948-Push-Templates).  Enable push templates using these platform-specific guides:

* [Android](https://developers.moengage.com/hc/en-us/articles/4403408116884-Push-Templates#01H8KSGSRA13MVGJA6MWC7TWBF)
* [iOS](https://developers.moengage.com/hc/en-us/articles/4403956104084-Push-templates#h_01H9MKXXAX6C1FP3544XX0AJ6J)


## Push Amp+ (Android only, optional)

Improve notification delivery rates by integrating Push Amplification+.  See the documentation for each OEM-specific SDK.

### Supported Integrations

* [HMS Push Kit](https://developers.moengage.com/hc/en-us/articles/4403466195732)


## Push Amplification (Android only, optional)

Use Push Amplification as a fallback if FCM fails.  See this guide: [Push Amplification](https://developers.moengage.com/hc/en-us/articles/4650416409876-Push-Amplification#01H8KQW3RYC8PBKM5BCS8AR2FD).


## Notification Center

Implement a notification center to show push notification history.  See this guide: [Notification Center](https://developers.moengage.com/hc/en-us/articles/4407468722452-Notification-Center).


## Location-Triggered Notifications (optional)

Send location-based notifications. See this guide: [Location-Triggered](https://developers.moengage.com/hc/en-us/articles/9613758028564-Location-Triggered).


## Device-Triggered Notifications (optional)

Send notifications triggered by device activity, including offline delivery.

* [Android](https://developers.moengage.com/hc/en-us/articles/4649815712532-Device-Triggered)
* [iOS](https://developers.moengage.com/hc/en-us/articles/4404012829204-Real-Time-Triggers)


## Advanced Use Cases in Android

* **Non-MoEngage Payload:** Handle push payloads from other servers. See this guide: [here](https://developers.moengage.com/hc/en-us/articles/5339876445972-Configuring-FCM#01H8KNNGF169M3A7TRJ6GZKRDC).

* **Callbacks and Customizations:** Customize notification display and behavior.  See this guide: [here](https://developers.moengage.com/hc/en-us/articles/4403449633428-Callbacks-and-Customisation).  This includes:
    * Controlling notification visibility
    * Notification received, clicked, and cleared callbacks
    * Custom action button click handling

* **Push Display Handled by Application (Android):** Handle push display and tracking on the client side. See this [article](https://developers.moengage.com/hc/en-us/articles/4403442558228-Push-Display-Handled-by-Application).


# In-App Messages

Send in-app messages to users within your app.

**Basic Setup:**

* [Android](https://developers.moengage.com/hc/en-us/articles/4404257042452-InApp-NATIV#h_01H9677QPM7GGHPNQZ0292PYSZ)
* iOS (no installation needed)


## Displaying In-App Messages

Use MoEngage's built-in UI or handle it yourself.

* **Show In-app:** Use the `showInApp()` method (see [here](https://developers.moengage.com/hc/en-us/articles/4404257042452-InApp-NATIV#h_01H9677QPM7GGHPNQZ0292PYSZ)).

* **Handling Orientation Change:**  Notify the SDK of orientation changes. See this [article](https://developers.moengage.com/hc/en-us/articles/4404257042452-InApp-NATIV#h_01H9677QPMJHDF9TBX410DHWRJ).

* **Self-handled In-apps:**  Build your own UI using the SDK's payload.
    * [Getting self-handled campaigns](https://developers.moengage.com/hc/en-us/articles/4404257042452-InApp-NATIV#h_01H9677QPMAQ9Z37KBTAXVQJ82)
    * [Tracking Statistics for Self-Handled In-Apps](https://developers.moengage.com/hc/en-us/articles/4404257042452-InApp-NATIV#h_01H9677QPM8A606G1KRCBMD23M)


## InApp Callbacks

Register for callbacks for in-app shown, clicked, dismissed, and self-handled events. See this [article](https://developers.moengage.com/hc/en-us/articles/4404257042452-InApp-NATIV#h_01H9677QPM37XA96NWBFN69FDT).


# Cards

Implement self-handled cards to display persistent messages. See this guide: [Self-Handled Cards](https://developers.moengage.com/hc/en-us/articles/18392458870676-Self-Handled-Cards).

# Glossary of Terms

* **AAID:** Advertising Identifier
* **APNS:** Apple Push Notification service
* **FCM:** Firebase Cloud Messaging
* **OEM:** Original Equipment Manufacturer
* **SDK:** Software Development Kit
