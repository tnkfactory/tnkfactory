---
layout: default
title: 3. Analytics Report
parent: Tnkfactory SDK Rwd
nav_order: 3
---

# Analytics Report
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}


Analytics 적용을 위해서는 Tnk 사이트에서 앱 등록 및 프로젝트 상의 SDK 관련 설정이 우선 선행되어야합니다.

[[SDK 설정하기](/sdk_rwd/sdk_setting/)]의 내용을 우선 확인해주세요.

## 기본 설정
<br>
AndroidMenifest.xml 파일 내에 Tnk 앱 등록세 발급 받은 App ID를 설정하시고 그 아래에 아래와 같이 tnkad_tracking 값을 true로 설정합니다.

이후 더 이상 tracking을 원하지 않을 경우에는 false로 설정하시기 바랍니다.

```xml
<application>
    ...
    <meta-data android:name="tnkad_app_id"  android:value="your-app-id-from-tnk-sites" />
    <meta-data android:name="tnkad_tracking" android:value="true" />
    ...
</application>
```

앱의 유입경로 파악을 위해서는 Google Install Referrer 라이브러리가 필요합니다. 아래와 같이 build.gradle (Module: app) 안에 라이브러리를 설정합니다.

\- GooglePlay에서 다운받은 앱에 대해서만 유입 경로 파악 기능이 제공됩니다.

```gradle
dependencies {
    ...
    implementation 'com.android.installreferrer:installreferrer:1.1'
    ...
}
```

SDK가 요구하는 permission들을 추가합니다.

\- 앱의 유입 경로 기능을 사용하기 위해서는 BIND_GET_INSTALL_REFERRER_SERVICE 권한은 필수입니다.

```xml
<uses-permission android:name="android.permission.INTERNET" />

<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />

<uses-permission android:name="com.google.android.finsky.permission.BIND_GET_INSTALL_REFERRER_SERVICE" />
```

전체적인 AndroidMenifest 파일의 모습은 아래와 같습니다.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.myapplication" >

    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="com.google.android.finsky.permission.BIND_GET_INSTALL_REFERRER_SERVICE" />



    <application android:icon="@drawable/ic_launcher" android:label="@string/app_name">

        ... your activities ...



        <meta-data android:name="tnkad_app_id" android:value="your-app-id-from-tnk-sites" />

        <meta-data android:name="tnkad_tracking" android:value="true" />    

    </application>

</manifest>
```

## 필수 호출
<br>
앱이 실행되는 시점에 TnkSession.applicationStarted()를 호출합니다. 필수적으로 호출해야하는 API 이며 이것만으로도 사용자 활동 분석을 제외한 대부분의 분석 데이터를 얻으실 수 있습니다.

### TnkSession.applicationStarted()
<br>
**Method**

- void TnkSession.applicationStarted(Context context)

**Description**

앱이 실행되는 시점에 호출합니다. 다른 API 보다 가장 먼저 호출되어야 합니다.

**Parameters**

| 파라메터 명칭 | 내용         |
| ------------- | ------------ |
| context       | Context 객체 |

**적용 예시**

```java
TnkSession.applicationStarted()
```

## 사용 활동 분석
<br>
사용자가 앱을 설치하고 처음 실행했을 때 어떤 행동을 취하는지 분석하고자 할 때 아래의 API를 사용합니다.

예를 들어 로그인, 아이템 구매, 친구 추천 등의 행동이 이루어 질때 해당 행동에 대한 구분자와 함께 호출해주시면 사용자가 어떤 패턴으로 앱을 이용하는지 또는 어떤 단계에서 많이 이탈하는지 등의 분석이 가능해집니다.

### TnkSession.actionCompleted()
<br>
**Method**

- void TnkSession.actionCompleted(Context context, String actionName)

**Description**

사용자의 특정 액션 발생시 호출합니다.

동일 액션에 대해서는 최초 발생시에만 데이터가 수집됩니다.

**Parameters**

| 파라메터 명칭 | 내용                                                         |
| -------------------- | ------------------------------------------------------------ |
| context       | Context 객체                                                 |
| actionName    | 사용자 액션을 구별하기 위한 문자열 (예를 들어 "user_login" 등) 사용하시는 actionName 들은 모두 Tnk 사이트의 분석보고서 화면에서 등록되어야 합니다. |

**적용예시**

```java
// 추가 데이터 다운로드 완료시
TnkSession.actionCompleted(this, "resource_loaded");

// 회원 가입 완료시
TnkSession.actionCompleted(this, "signup_completed");

// 프로필 작성 완료시
TnkSession.actionCompleted(this, "profile_entered");

// 친구 추천시
TnkSession.actionCompleted(this, "friend_invite");
```

## 구매 활동 분석
<br>
사용자가 유료 구매 등의 활동을 하는 경우 이에 대한 분석데이터를 얻고자 할 경우에는 아래의 API를 사용합니다.

구매활동 분석 API 적용시에는 유입경로별로 구매횟수와 구매 사용자 수 파악이 가능하며, 하루 사용자 중에서 몇명의 유저가 구매 활동을 하였는 지 또 사용자가 앱을 처음 실행한 후 얼마정도가 지나야 구매활동을 하는지 등의 데이터 분석이 가능합니다. 분석 보고서에서 제공하는 데이터에 각 아이템별 가격을 대입시키면 ARPU 및 ARPPU 값도 산출하실 수 있습니다.

### TnkSession.buyCompleted()
<br>
**Method**

- void TnkSession.buyCompleted(Context context, String itemName)

**Description**

사용자가 유료 구매를 완료하였을 때 호출합니다.

**Parameters**

| 파라메터 명칭 | 내용                                                        |
| ------------- | ----------------------------------------------------------- |
| context       | Context 객체                                                |
| itemName      | 구매한 item을 구별하기 위한 문자열 (예를 들어 "item_01" 등) |

**적용예시**

```java
// item_01 구매 완료시
TnkSession.buyCompleted(this, "item_01");

//item_02 구매 완료시
TnkSession.buyCompleted(this, "item_02");
```

## 사용자 정보 설정

사용자의 성별 및 나이 정보를 설정하시면 보고서에서 해당 내용이 반영되어 추가적인 데이터를 확인하실 수 있습니다.

```java
// 나이 설정
TnkSession.setUserAge(this,23);

// 성별 설정 (남)
TnkSession.setUserGender(this,TnkCode.MALE);

// 성별 설정 (여)
TnkSession.setUserGender(this,TnkCode.FEMALE);
```
