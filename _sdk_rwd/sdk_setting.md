---
layout: default
title: 1. SDK 설정하기
parent: Tnkfactory SDK Rwd
nav_order: 1
---

# SDK설정하기
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### 라이브러리 등록

TNK SDK는 Maven Central에 배포되어 있습니다.

최상위 Level(Project) 의 build.gradle 에 maven repository를 추가해주세요.

```gradle
repositories {
    mavenCentral()
}
```

아래의 코드를 App Module의 build.gradle 파일에 추가해주세요.

```gradle
dependencies {
    implementation 'com.tnkfactory:rwd:7.25.1'
}
```

### Manifest 설정하기

#### Application ID 설정하기

Tnk 사이트에서 앱 등록하면 상단에 App ID 가 나타납니다. 이를 AndroidMenifest.xml 파일의 <application> tag 안에 아래와 같이 설정합니다.

(*your-application-id-from-tnk-site* 부분을 실제 App ID 값으로 변경하세요.)

```xml
<application>

     ...

    <meta-data android:name="tnkad_app_id" android:value="your-application-id-from-tnk-site" />

</application>
```

#### 권한 설정

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

동영상 광고 적용 시 **ACCESS_WIFI_STATE** 권한은 필수 설정 권한입니다.

```xml
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

#### Activity tag 추가하기

광고 목록을 띄우기 위한 Activity 2개를 <activity>로 아래와 같이 설정합니다. 매체앱인 경우에만 설정하시면 됩니다. 광고만 진행하실 경우에는 설정하실 필요가 없습니다.

```xml
<activity android:name="com.tnkfactory.ad.AdWallActivity" />
<activity android:name="com.tnkfactory.ad.AdMediaActivity" android:screenOrientation="landscape"/>

<!-- 또는 아래와 같이 설정-->
<activity android:name="com.tnkfactory.ad.AdMediaActivity" android:screenOrientation="sensorLandscape"/>

<!-- 동영상 세로 화면으로 설정하려면 아래와 같이 설정 -->
<activity android:name="com.tnkfactory.ad.AdMediaActivity" android:screenOrientation="portrait"/
```

### Proguard 사용

Proguard를 사용하실 경우 Proguard 설정내에 아래 내용을 반드시 넣어주세요.

```
-keep class com.tnkfactory.** { *;}
```

### COPPA 설정

COPPA는 [미국 어린이 온라인 개인정보 보호법](https://www.ftc.gov/tips-advice/business-center/privacy-and-security/children's-privacy) 및 관련 법규입니다. 구글 에서는 앱이 13세 미만의 아동을 대상으로 서비스한다면 관련 법률을 준수하도록 하고 있습니다. 연령에 맞는 광고가 보일 수 있도록 아래의 옵션을 설정하시기 바랍니다.

```java
TnkSession.setCOPPA(MainActivity.this, true); // ON - 13세 미만 아동을 대상으로 한 서비스 일경우 사용
TnkSession.setCOPPA(MainActivity.this, false); // OFF
```
