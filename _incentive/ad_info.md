---
layout: default
title: APP ID
permalink: incentive/APP ID
nav_order: 2
---

# APP ID와 APP KEY
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

## 광고 매체 등록하기
보상형 광고를 탑재하기 위해서는 다음과 같은 단계를

![appid_placementid](/assets/incentive/incentive_1.png)

![appid_placementid](/assets/incentive/incentive_3.png)

![appid_placementid](/assets/incentive/incentive_3.png)

![appid_placementid](/assets/incentive/incentive_4.png)

- 플랫폼 : 사용 할 플랫폼을 설정합니다. (android iOS 각각 등록하셔야 합니다.)
- 앱 이름 : 관리 페이지에서 사용 할 앱의 이름입니다.
- 아이콘 : 앱의 아이콘을 등록합니다. 300x300미만 png파일로 등록 해 주세요
- 패키지명 : 안드로이드의 경우 앱의 패키지명, iOS의 경우 appscheme를 입력합니다.
- 카테고리 : 적용 할 매체의 관련 카테고리를 선택합니다.(미 지정시 기본 값 사용, But 광고 수익 향상을 위해 선택 권장)
- 등급, 주 사용자 : 해당 매체에 나갈 광고의 연령 등급과 주 사용자 성별 필터입니다.
- time zone : 앱이 주로 사용되는 지역의 타임존 값을 선택합니다.
- 개발사명 : 해당 플랫폼을 개발하는 개발사명입니다.


## APP ID

![appid_placementid](/assets/incentive/incentive_7.png)

등록 후 좌측 메뉴의 '매체관리'에서 앱을 선택 후  
기본설정 메뉴에서 상단의 AppID값을 저장해 두시기 바랍니다.

광고 매체(Android App, iOS App, Web 등)의 id입니다.

<p>앱 개발 시 AndroidManifest.xml 파일 등에 설정합니다.</p>

[Android APP ID id설정](/sdk_rwd/sdk_setting/#manifest-설정하기){:target="_blank"}

[iOS APP ID id설정](https://github.com/tnkfactory/ios-sdk-rwd/blob/master/iOS_Guide.md#tnk-%EA%B0%9D%EC%B2%B4-%EC%B4%88%EA%B8%B0%ED%99%94){:target="_blank"}
