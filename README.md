# BlendVision Player Android SDK

This repository contains sample apps using the BlendVision Player Android SDK.  
This guide details how to integrate the BlendVision Player SDK into your application.  
Our player provides convenient APIs for DRM, media controllers, and a generic UI that can be customized as needed.

## Requirements

- **IDE**: Android Studio 3.0 or later
- **minSdkVersion**: 21
- **targetSdkVersion**: 34
- **Kotlin Version**: 1.9.x or later
- **Android Gradle Plugin**: 8.2.0 or lower

## Integration

### In your settings.gradle file, `dependencyResolutionManagement` sections:
[Gets username and password](https://github.com/BlendVision/Android-Player-SDK/wiki/Android%E2%80%90Player%E2%80%90SDK-pull-credentials)
```groovy
dependencyResolutionManagement {
  repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
  repositories {
    google()
    mavenCentral()
    //add below
    maven {
      url = uri("https://maven.pkg.github.com/blendvision/Android-Player-SDK")
      credentials {
        username = //TODO
        password = //TODO
      }
    }

  }
}
```

### Add the dependencies for the Messaging SDK to your module's app-level Gradle file, normally app/build.gradle:

```groovy
dependencies {
    implementation 'com.blendvision.player:playback:5.0.0'
    implementation 'com.blendvision.player:download:5.0.0'
    implementation 'com.blendvision.player:analytics:5.0.0'
    implementation 'com.blendvision.player:common:5.0.0'
}
```

> **Note**: After making changes, don't forget to sync your Gradle files to ensure that the project
> compiles successfully.

## Sample App Setup Instructions

### Player license
BlendVision Player license key is obtained by logging into BlendVision CMS (https://app.one.blendvision.com/en/dashboard) and navigating to `VOD -> select one of content -> share icon -> Player SDK -> License Key` to find the license.

#### The license key can be add by following two ways:
1. Dynamically coding (license lifecycle scope only for current player instance)
    ```kotlin
    private var player: UniPlayer? = null
    
    player = UniPlayer.Builder(
        requireContext(),
        PlayerConfig(
            license = "{YOUR_PLAYER_LICENSE}"
        )
    ).build()
    
    binding.kksPlayerServiceView.setUnifiedPlayer(player)
    ```
2. Application manifest (license lifecycle scope for all players in your application)
    ```xml
    <meta-data 
        android:name="UNI_PLAYER_LICENSE_KEY" 
        android:value="{YOUR_PLAYER_LICENSE}"
    />
    ```

> **Note**:
>   1. The order player adopts is first check PlayerConfig and then check meta-data.
>   2. If the license key is not correctly set, you will encounter a 20403 error.

