---
title: Apple Privacy Manifest 
description: Learn what changes you need to apply to your project to support the latest Apple privacy policy.
type: troubleshooting
page_title: Apple's Privacy Manifest Policy Requirements
slug: adding-apple-privacy-manifest-file-dotnet-maui-application
tags: apple, privacy, manifest, apple store, requirements, .NET MAUI
res_type: kb
---

Apple is introducing a new privacy policy for including privacy manifest files in your apps that target the iOS, iPadOS, tvOS, visionOS, and watchOS platforms on the App Store. 
For more details on this policy, please review the <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files" target="_blank">Privacy Manifest Files</a> in the Apple documentation.

> As of May 1, 2024, the Apple privacy policy manifest file must be included in your apps.

## What Must Be Included in the PrivacyInfo.xcprivacy File

The `PrivacyInfo.xcprivacy` file lists:

* The <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests" target="_blank">types of data</a> collected by your .NET MAUI application or any third-party SDKs.
* The reasons for using certain <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_use_of_required_reason_api" target="_blank">Required Reason APIs</a>. 

## Add PrivacyInfo.xcprivacy to Your Application

Create a `PrivacyInfo.xcprivacy` file inside the `Platforms/iOS` folder.

For reference, you can use the `PrivacyInfo.xcprivacy` file already added to the [Telerik UI for .NET MAUI Controls Samples]({% slug controls-samples-app %}) and [Telerik UI for .NET MAUI Crypto Tracker]({% slug maui-crypto-app %}) applications:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>NSPrivacyAccessedAPITypes</key>
    <array>
        <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategoryFileTimestamp</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>C617.1</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategorySystemBootTime</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>35F9.1</string>
            </array>
        </dict>
        <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategoryDiskSpace</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>E174.1</string>
            </array>
        </dict>     
	    <dict>
            <key>NSPrivacyAccessedAPIType</key>
            <string>NSPrivacyAccessedAPICategoryUserDefaults</string>
            <key>NSPrivacyAccessedAPITypeReasons</key>
            <array>
                <string>CA92.1</string>
            </array>
        </dict>
    </array>
</dict>
</plist>
```

## See Also

* <a href="https://devblogs.microsoft.com/dotnet/apple-privacy-manifest-support/" target="_blank">Microsoft Blogs - Adding Apple Privacy Manifest Support to .NET iOS & .NET MAUI Apps</a>
* <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files" target="_blank">Apple Documentation - Privacy Manifest Files</a>
* <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/adding_a_privacy_manifest_to_your_app_or_third-party_sdk" target="_blank">Apple Documentation - Adding a Privacy Manifest File</a>
* <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests" target="_blank">Apple Documentation - Describing Data Use in Privacy Manifests</a>
* <a href="https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_use_of_required_reason_api" target="_blank">Apple Documentation - Describing Use of Required Reason API</a>