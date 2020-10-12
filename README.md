
# The Amazon Kinesis Video WebRTC Sample
[![Build Status](https://travis-ci.org/awslabs/amazon-kinesis-video-streams-webrtc-sdk-ios.svg?branch=master)](https://travis-ci.org/awslabs/amazon-kinesis-video-streams-webrtc-sdk-ios)
[![Coverage Status](https://codecov.io/gh/awslabs/amazon-kinesis-video-streams-webrtc-sdk-ios/branch/master/graph/badge.svg)](https://codecov.io/gh/awslabs/amazon-kinesis-video-streams-webrtc-sdk-ios)

This sample demonstrates the Amazon KinesisVideoStreams and KinesisVideoSignaling framework found in the AWS Mobile SDK for iOS.

## Requirements

* Xcode 10 and later
* iOS 11 and later

#### Download the WebRTC SDK in iOS
To download the WebRTC SDK in iOS, run the following command:

    git clone https://github.com/awslabs/amazon-kinesis-video-streams-webrtc-sdk-ios.git
  

#### Using XCode to build the project

1. The AWS Mobile SDK for iOS is available through [CocoaPods](http://cocoapods.org). If you have not installed CocoaPods, install CocoaPods: (Requires Ruby installed) 

        sudo gem install cocoapods
        pod setup

2. To install the AWS Mobile SDK for iOS run the following command in the directory containing this sample:

        pod install

3. Create an Amazon Cognito User Pool. Follow the 4 steps under **Creating your Cognito Identity user pool** in this [blog post](http://mobile.awsblog.com/post/TxGNH1AUKDRZDH/Announcing-Your-User-Pools-in-Amazon-Cognito).

4. Open `KinesisVideoWebRTCDemoApp.xcworkspace` (File location: KVSiOS/Swift/AWSKinesisVideoWebRTCDemoApp.xcworkspace).

5. Open **Constants.swift**. Set **CognitoIdentityUserPoolRegion**, **CognitoIdentityUserPoolId**, **CognitoIdentityUserPoolAppClientId** and **CognitoIdentityUserPoolAppClientSecret** to the values obtained when you created your user pool.
```swift
        let CognitoIdentityUserPoolRegion: AWSRegionType = .Unknown
        let CognitoIdentityUserPoolId = "YOUR_USER_POOL_ID"
        let CognitoIdentityUserPoolAppClientId = "YOUR_APP_CLIENT_ID"
        let CognitoIdentityUserPoolAppClientSecret = "YOUR_APP_CLIENT_SECRET"
```
Replace the “REPLACEME” places in each of these files with the appropriate AWS Credentials:
  *  _awsconfiguration.json_ (path: KVSiOS/Swift/KVSiOSApp/awsconfiguration.json)
  *     _Constants.swift_ (path: KVSiOS/Swift/KVSiOSApp/Constants.swift)

6. To build and run, click the play button on the XCode menu. 
The following step-by-step instructions describe how to download, build, and run the Kinesis Video Streams WebRTC SDK in iOS.

The following cocoa pod dependencies are included in the Podfile and need to pod installed:

 * Starscream
 * Common Crytpo
 * WebRTC.framework: this is the GoogleWebRTC module framework package (bit code disabled).
 * AWSMobileClient
 * AWSCognito
 * AWSKinesisVideo
 * AWSKinesisVideoSignaling
 


#### Run the iOS Sample Application
Building the iOS sample application installs the AWSKinesisVideoWebRTCDemoApp on your iOS device. Using this app, you can verify live audio/video streaming between mobile, web and IoT device clients (camera). The procedure below describes some of these scenarios. 

Complete the following steps:

1.    On your iOS device, open AWSKinesisVideoWebRTCDemoApp and login using the AWS user credentials from Set Up an AWS Account and Create an Administrator. (Note: Cognito settings can be tuned through your Cognito User Pool in the AWS management Console)
2.    On successful sign-in, the channel configuration view is displayed where the **channel-name, client-id (optional) and region-name** have to be configured. 

#### Run the Integration Tests  
1.   To run the integration tests, the test user has to be created with the appropiate test password as in the TestConstants.swift file located at amazon-kinesis-video-streams-webrtc-sdk-ios/Swift/AWSKinesisVideoWebRTCDemoAppUITests/TestConstants.swift


##### Note
*    Ensure that in all the cases described below, both the client applications use the same signaling channel name, region, viewer-id/client-id and the AWS account id.
*    Please note that a Primary Connection should be started first before the viewer connects to it.

#####    Peer to Peer Streaming between multiple iOS devices: One Primary Connection and Mutliple Viewer Connections:
*    Start one iOS device in primary mode for starting a new session using a channel name (e.g. demo). Remote peer will be joining as viewer to this primary connection.
*    Currently, there can be only one primary connection for a channel at any given time.
*    Use other iOS devices, with the application installed, to connect to the same channel name (started up in the above step set up as a primary) in viewer mode. This will connect to an existing session (channel) where a primary connection was setup. 

#####    Peer to Peer Streaming between [Embedded SDK](https://github.com/awslabs/amazon-kinesis-video-streams-webrtc-sdk-c) Primary and iOS device:
  *    Run KVS WebRTC embedded SDK (in C) in primary mode on a camera device.
  *    Start the iOS device in viewer mode – you should be able to see the local video preview in the lower right side of the screen and also the larger part of the screen should stream the remote video view.

#####    Peer to Peer Streaming between iOS device as Primary and Web browser as viewer:
 *    Start one iOS device in primary mode for starting a new session using a channel name (e.g. demo)
 *    Start the Web Browser using the Javascript SDK (JS with audio selected) and start it as viewer.
 *    Verify media showing up from the iOS device and also from the browser.

##### Note

* _This sample application with multiple viewers has been tested in iPhone8(iOS 14.0.1) & iPhone XS(iOS 14.0.1) and between JS SDK. 
* _This sample does not have the audio support from Viewers to Primary Connection.
* _In scenario (i.e) When primary connection has been established, and 2 viewers V1 & V2 have joined in
    _Video : V1 will show up on the Primary's application and V2 will not will not visible on the Primary's screen. The Sample currently has UI only to show only 1 viewer connection and other view connections video to the Primary will be ignored. 
    _Audio: V1 audio track on the Primary application will be available & V2's audio track will be ignored on the primary to avoid audio mixing, however we will have the Primary's audio on all the viewers. 

## License
This library is licensed under the [Apache 2.0 License](https://github.com/awslabs/amazon-kinesis-video-streams-webrtc-sdk-ios/blob/master/LICENSE).
