# Migration Guide: Upgrading from Version 4.5.x to 5.0.0

Upgrading from version 4.5.x to 5.0.0 introduces several breaking changes. This guide provides detailed instructions to help you migrate your project to the latest version smoothly. The major breaking changes include:

1. Maven implementation from GitHub.
2. Changes to the `MediaConfig` interface.
3. Changes in import paths.

## 1. Maven Implementation from GitHub

### Previous version (4.5.x)
In version 4.5.x, you might import the player SDK as below which under project libs folder. In addition, implemetation other library because of player needed.  

Example:
```groovy
implementation fileTree(dir: '../libs', include: ['*.jar', "*.aar"])

// player dependency, for example:

//Glide
implementation Libs.glide

//gson
implementation Libs.gson

//coroutines
implementation Libs.coroutines

//retrofit2
implementation Libs.retrofit2
implementation Libs.converterGson

//okhttp_logging_interceptor
implementation Libs.okhttp_logging_interceptor

//koin
implementation Libs.koin

// ... and so on
```

### New version (5.0.0)
Start from version 5.0.0, the dependency management has been streamlined, and the project artifacts are now hosted on Github package repository.

Example:
```groovy
// only add these library
implementation 'com.blendvision.player:playback:5.0.0'
implementation 'com.blendvision.player:download:5.0.0'
implementation 'com.blendvision.player:analytics:5.0.0'
implementation 'com.blendvision.player:common:5.0.0'
```

***Note***: please check README for setting maven repository, than you can implementation above library.

#### Steps to Migrate:
1. Add maven repository
    - Please check the `In your settings.gradle file` section in README.
3. Implementation player SDK
4. Remove redundent library

## 2. MediaConfig Interface Changed

### Previous Interface (4.5.x)
```kotlin
data class MediaConfig {
    source = listOf(
        MediaConfig.Source(
            ...
        )
    ),
}
```

### New Interface (5.0.0)
In version 5.0.0, the `MediaConfig` object is more straightforward to present as a single streaming source.

```java
data class MediaConfig {
    source = MediaConfig.Source(
        ...
    ),
}
```

#### Steps to Migrate:
1. Remove the list struture

## 3. Import Path Changed

### Previous Import Paths (4.5.x)
In version 4.5.x, the player classes might have been imported from a exist package structure.

Example:
```kotlin
import com.blendvision.player.playback.player.common.PlayerConfig
import com.blendvision.player.playback.player.common.UniPlayer
import com.blendvision.player.playback.player.common.callback.PlayLogger
```

### New Import Paths (5.0.0)
In version 5.0.0, the package structure has been reorganized to improve modularity, clarity and better documentation.

Example:
```kotlin
import com.blendvision.player.playback.presentation.entity.PlayerConfig
import com.blendvision.player.playback.presentation.UniPlayer
import com.blendvision.player.playback.presentation.logger.PlayLogger
```

#### Steps to Migrate:
1. Add missing classes with Android Studio's helping
    - hotkey: option + enter
2. Remove previous imported classes with Android Studio
    - hotkey: option + command + o

## Summary

Upgrading from version 4.5.x to 5.0.0 involves updating your Maven dependencies, implementing new methods in the `MediaConfig` interface, and updating import paths throughout your codebase. Following this guide will help ensure a smooth transition to the latest version. Always remember to thoroughly test your application after making these changes to verify that everything works as expected.