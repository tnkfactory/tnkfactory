---
layout: default
title: 그 밖의 기능들
parent: 2. Publisher API
grand_parent: Tnkfactory SDK Rwd
permalink: /docs/sdk_rwd/publisher_api/etc/
nav_order: 3
---

## 그밖의 기능들
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
#### TnkSession.queryPublishState()

Tnk 사이트의 [게시정보]에서 광고 게시 중지를 하게 되면 이후에는 사용자가 광고 목록 창을 띄워도 광고들이 나타나지 않습니다.
그러므로 향후 광고 게시를 중지할 경우를 대비하여 화면에 충전소 버튼 자체를 보이지 않게 하는 기능을 갖추는 것이 바람직합니다.
이를 위하여 현재 게시앱의 광고게시 상태를 조회하는 기능을 제공합니다.

**Method**

  - void TnkSession.queryPublishState(Context context, boolean showProgress, ServiceCallback callback)

**Parameters**

| 파라메터 명칭 | 내용                                                         |
| -------------- | ----------------------------------------------------------- |
| context       | 현재 Activity 또는 Context 객체                              |
| showProgress  | 서버에서 결과가 올때까지 화면에 progress dialog를 띄울지 여부를 지정 |
| callback      | 서버에서 결과가 오면 callback 객체의 OnReturn(Context context, Object result) 메소드가 호출됩니다. 메소드 호출은 Main UI Thread 상에서 이루어 집니다. 전달된 result 객체는 Integer 객체이며 상태코드가 담겨 있습니다. 상태코드 값이 TnkSession.STATE_YES 인 경우(실제 값은 1)는 광고게시상태를 의미합니다. |

**적용예시**

```java
final Button button = (Button)findViewById(R.id.main_ad);

// ...

TnkSession.queryPublishState(this, false, new ServiceCallback() {

    @Override
    public void onReturn(Context context, Object result) {

        int state = (Integer)result;

        if (state == TnkSession.STATE_YES) {
            button.setVisibility(View.VISIBLE);
        }
    }
});
```

#### TnkSession.queryAdvertiseCount()

광고 게시 상태를 확인하여 충전소 버튼을 보이게하거나 안보이게 하는 것으로도 좋지만 실제적으로 현재 적립 가능한 광고가 있는지 여부를 판단해서 버튼을 노출하는 것이 보다 바람직합니다.
이를 위하여 현재 적립가능한 광고 정보를 확인하는 기능을 아래와 같이 제공합니다.

**Method**

  - void TnkSession.queryAdvertiseCount(Context context, boolean showProgress, ServiceCallback callback)

**Parameters**

| 파라메터 명칭 | 내용                                                         |
| -------------- | ----------------------------------------------------------- |
| context       | 현재 Activity 또는 Context 객체                              |
| showProgress  | 서버에서 결과가 올때까지 화면에 progress dialog를 띄울지 여부를 지정 |
| callback      | 서버에서 결과가 오면 callback 객체의 OnReturn(Context context, Object result) 메소드가 호출됩니다. 메소드 호출은 Main UI Thread 상에서 이루어 집니다. 전달된 result 객체는 int[] 객체이며 int[0]는 광고 건수, int[1] 에는 적립가능한 포인트 합계가 담겨 있습니다. 만약 현재 광고 게시상태가 아니라면 int[0]에는 0이 담겨있습니다. |

#### TnkSession.enableLogging()

Tnk의 SDK에서 생성하는 로그를 출력할지 여부를 결정합니다. 테스트 시에는 true로 설정하시고 Release 빌드시에는 false로 설정해주시기 바랍니다.

**Method**

  - void TnkSession.enableLogging(boolean trueOrFalse)

#### TnkSession.setAgreePrivacy()

개인정보 수집동의 여부를 설정합니다. true 설정시 오퍼월에서 개인정보 수집동의 팝업이 뜨지 않습니다. 다시 해당 팝업창을 띄우고 싶은 경우 false로 설정해주시기 바랍니다.

**Method**

  - void TnkSession.queryPoint(Context context, boolean isAgree)
