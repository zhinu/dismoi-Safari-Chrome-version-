# Steps to reproduce what I have done 

## 1. Download
First download the extension from https://github.com/dis-moi/extension/releases (here we use the Google Chrome version), unpack it using available tools.

## 2. Install Xcode 13 
Xcode needs to be version 13 (found here https://xcodereleases.com/ ), at this time it is still in Beta version. Version 12 will also work, but you won't be able to build for ios devices (Ipad & Iphone)
If Xcode is already installed make sure that the xcrun version in the terminal is at least 60. To check : 
```
xcrun --version
```
If the version is wrong then apply the following step
```
sudo xcode-select --switch /Applications/Xcode-beta.app
```

## 3. Convert the extension to Safari
Use the safari-web-extension-converter to convert the extension.

Below my log :

```
dismoi@Johns-MacBook-Air ~ % xcrun safari-web-extension-converter /Users/dismoi/Documents/bulles-v3.86.7-chromium-proding   
objc[12145]: Class AMSupportURLConnectionDelegate is implemented in both /usr/lib/libauthinstall.dylib (0x1f16f5160) and /System/Library/PrivateFrameworks/MobileDevice.framework/Versions/A/MobileDevice (0x10df342c8). One of the two will be used. Which one is undefined.
objc[12145]: Class AMSupportURLSession is implemented in both /usr/lib/libauthinstall.dylib (0x1f16f51b0) and /System/Library/PrivateFrameworks/MobileDevice.framework/Versions/A/MobileDevice (0x10df34318). One of the two will be used. Which one is undefined.
Xcode Project Location: /Users/dismoi
App Name: Dismoi - proding
App Bundle Identifier: com.yourCompany.Dismoi---proding
Platform: All
Language: Swift
Warning: The following keys in your manifest.json are not supported by your current version of Safari. If these are critical to your extension, you should review your code to see if you need to make changes to support Safari:
	exclude_matches
	exclude_globs
	persistent
	version
	browser_action
	content_security_policy
	name
	js
	matches
	externally_connectable
	icons
	description
	activeTab
	storage
	page
	manifest_version
	web_accessible_resources
	contextMenus
	run_at
```

## 4. Change the manifest to make the background not permanent (for IOS)
Although persistent background is supported for macos, it is not for ios. The stated ground for this, is to save resources (Apple recommends to change the background page to include a timer or an eventlistener). To quicly fix, this to be able to activate the extension in the simulator, change the manifest to include :
```
"background": {
    "page": "background.html",
    "persistent": false
  },
````

## 5. Enjoy 
![Simulator Screen Shot - iPhone 12 Pro Max - 2021-08-18 at 17 31 02](https://user-images.githubusercontent.com/75084558/129975395-bec661b9-abfd-4906-911a-a85a34b5fd04.png)
![Simulator Screen Shot - iPhone 12 Pro Max - 2021-08-18 at 17 33 12](https://user-images.githubusercontent.com/75084558/129975408-e14f5dd5-16e3-494a-ba24-55a1f5eef897.png)

