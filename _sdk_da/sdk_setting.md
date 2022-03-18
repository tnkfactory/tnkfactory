---
layout: default
title: 1. SDK 설정하기
parent: Tnkfactory SDK DA
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
    implementation 'com.tnkfactory:pub:7.17.2'
}
```

AndroidManifest.xml 파일에 아래의 권한을 추가해주세요.

```xml
// 광고 정보를 수신하기 위해 인터넷 사용 권한 추가
<uses-permission android:name="android.permission.INTERNET" />
// 동영상 광고를 사용 할 경우 WIFI상태 체크 권한 추가
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```



Proguard 를 사용하시는 경우 Proguard 설정 파일에 아래의 내용을 반드시 넣어주세요.

```proguard
 -keep class com.tnkfactory.** { *;}
```

### Test Flight

아래의 코드를 사용하어 간단하게 테스트 광고를 띄워보세요.
> SDK import

```java
import com.tnkfactory.ad.*;
```

> 전면 광고 (Interstitial Ad)

```java
InterstitialAdItem adItem = new InterstitialAdItem(this,"TEST_INTERSTITIAL_V", new AdListener() {
        @Override
        public void onLoad(AdItem adItem) {
            adItem.show();
        }
    });

adItem.load();
```
> 배너 광고 (Banner Ad)

```xml
<com.tnkfactory.ad.BannerAdView
    android:id="@+id/banner_ad_view"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_alignParentBottom="true"
    android:background="#ffffffff"
    app:placement_id="TEST_BANNER_100"/>
```

```java
BannerAdView bannerAdView = findViewById(R.id.banner_ad_view);
bannerAdView.load();
```
> Test Flight 용 Placement 들

아래와 같이 광고 유형별로 Test Flight 용 Placement 들을 제공하고 있습니다. 아래의 Placement ID 를 사용하시면 별도로 계정이나 앱을 등록하지 않아도 간단하게 테스트 광고를 띄워보실 수 있습니다.

- TEST_BANNER_100 : 배너 광고 (640x100)
- TEST_BANNER_200 : 배너 광고 (640x200)
- TEST_INTERSTITIAL_H : 전면 광고 가로
- TEST_INTERSTITIAL_V : 전면 광고 세로
- TEST_INTERSTITIAL_V_FINISH : 전면 광고 세로 (종료시 2-Button 형)
- TEST_FEED : 피드형 광고
- TEST_NATIVE : 네이티브 광고
- TEST_REWARD_V : 리워드 동영상 광고

### Publisher ID 등록하기
<br>
Test Flight 에서는 별도로 계정등록을 하지않아도 간단히 테스트를 할 수 있습니다.<br>
**(Test Flight의 PLACEMENT_ID를 사용하여 테스트를 진행하기 위해서는 Publisher ID를 등록하지 않고 진행 하셔야합니다.)**<br><br>
실제 광고를 받기 위해서는 우선 [Tnk Publish Site](https://pub.tnkad.net/pub/pub.inventory.user){:target="_blank"}에서 Inventory를 등록하여 발급받은 [Application id](/display_ad/ad_info){:target="_blank"}를 AndroidManifest.xml 파일에 추가하셔야합니다.
아래의 샘플을 참고하시어 실제 [Application id](/display_ad/ad_info){:target="_blank"}를 등록하세요.<br>
회원 가입 및 매체 설정을 하지 않으셨다면 다음 단계를 먼저 진행 하시기 바랍니다.<br>
- [회원가입](/docs/join){:target="_blank"}
- [매체관리](/display_ad/inventory){:target="_blank"}
<p> </p>
```xml
<application
   ...
   >
      ...

        <meta-data android:name="tnk_pub_id" android:value="YOUR-INVENTORY-ID-HERE" />

      ...
</application>
```

실제 ID를 등록하면 위 Test Flight 코드에서는 더 이상 광고가 나타나지 않습니다. Tnk Publish Site 에서 광고 유형에 맞추어 Placement 를 등록하시고 등록한 Placement의 이름을 사용하셔야 실제 광고가 표시됩니다.



### COPPA 설정

COPPA는 [미국 어린이 온라인 개인정보 보호법](https://www.ftc.gov/tips-advice/business-center/privacy-and-security/children's-privacy) 및 관련 법규입니다. 구글 에서는 앱이 13세 미만의 아동을 대상으로 서비스한다면 관련 법률을 준수하도록 하고 있습니다. 연령에 맞는 광고가 보일 수 있도록 아래의 옵션을 설정하시기 바랍니다.

```java
AdConfiguration.setCOPPA(this, true); // ON - 13세 미안 아동을 대상으로 한 서비스 일경우 사용
AdConfiguration.setCOPPA(this, false); // OFF - 기본값
```
