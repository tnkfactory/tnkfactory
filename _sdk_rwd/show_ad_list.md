---
layout: default
title: 광고 목록 띄우기
parent: 2. Publisher API
grand_parent: Tnkfactory SDK Rwd
permalink: /docs/sdk_rwd/publisher_api/show_ad_list/
nav_order: 1
---

## 광고 목록 띄우기
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
<u>테스트 상태에서는 테스트하는 장비를 개발 장비로 등록하셔야 광고목록이 정상적으로 나타납니다.</u>

#### 유저 식별 값 설정

앱이 실행되면 우선 앱 내에서 사용자를 식별하는 고유한 ID를 아래의 API를 사용하시어 Tnk SDK에 설정하시기 바랍니다.

사용자 식별 값으로는 게임의 로그인 ID 등을 사용하시면 되며, 적당한 값이 없으신 경우에는 Device ID 값 등을 사용할 수 있습니다.

(유저 식별 값이 Device ID 나 전화번호, 이메일 등 개인 정보에 해당되는 경우에는 암호화하여 설정해주시기 바랍니다.)

유저 식별 값을 설정하셔야 이후 사용자가 적립한 포인트를 개발사의 서버로 전달하는 callback 호출 시에  같이 전달받으실 수 있습니다.

##### Method

- void TnkSession.setUserName(Context context, String userName)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| context       | 현재 Activity 또는 Context 객체                              |
| userName      | 앱에서 사용자를 식별하기 위하여 사용하는 고유 ID 값 (로그인 ID 등)  길이는 256 bytes 이하입니다. |

#### 광고 목록 띄우기 (Activity)

자신의 앱에서 광고 목록을 띄우기 위하여 TnkSession.showAdList() 함수를 사용합니다. 광고목록을 보여주기 위하여 새로운 Activity를 띄웁니다.

##### Method

- void TnkSession.showAdList(Activity activity)
- void TnkSession.showAdList(Activity activity, AdListType adListType)
- void TnkSession.showAdList(Activity activity, String title)
- void TnkSession.showAdList(Activity activity, String title, AdListType adListType)
- void TnkSession.showAdList(Activity activity, String title, TnkLayout userLayout)
- void TnkSession.showAdList(Activity activity, String title, AdListType adListType, TnkLayout userLayout)

##### Description

광고 목록 화면 (AdWallActivity)를 화면에 띄웁니다.

반드시 Main UI Thread 상에서 호출하여야 합니다.

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| activity      | 현재 Activity 객체                                           |
| title         | 광고 리스트의 타이틀을 지정함  (기본값 : 무료 포인트 받기)   |
|adListType | 광고 리스트의 타입 (ALL : 보상형과 구매형 모두 표시, PPI : 보상형, CPS : 구매형) |
| userLayout    | 원하는 Layout을 지정할 수 있습니다. 자세한 내용은  [[디자인 변경하기](#라-디자인-변경하기)] 내용을 참고해주세요. |

##### 적용예시

```java
@Override

public void onCreate(Bundle savedInstanceState) {

    ...

    final Button button = (Button)findViewById(R.id.main_ad);

    button.setOnClickListener(new OnClickListener() {

        @Override

        public void onClick(View v) {

            TnkSession.showAdList(MainActivity.this,"Your title here");

        }

    });
}
```

#### 광고 목록 띄우기 (View)

광고 목록을 현재 화면에 팝업으로 띄우기 위하여 TnkSession.popupAdList() 함수를 사용합니다. 광고목록을 보여주기 위하여 AdListView를 생성하여 현재 화면에 팝업형태로 띄워줍니다.

##### Method

- void TnkSession.popupAdList(Activity activity)
- void TnkSession.popupAdList(Activity activity, AdListType adListType)
- void TnkSession.popupAdList(Activity activity, String title)
- void TnkSession.popupAdList(Activity activity, String title, AdListType adListType)
- void TnkSession.popupAdList(Activity activity, String title, TnkAdListener listener)
- void TnkSession.popupAdList(Activity activity, String title, AdListType adListType, TnkAdListener listener)
- void TnkSession.popupAdList(Activity activity, String title, TnkAdListener listener, TnkLayout userLayout)
- void TnkSession.popupAdList(Activity activity, String title, AdListType adListType, TnkAdListener listener, TnkLayout userLayout)

##### Description

광고 목록 화면 (AdListView)를 현재 화면에 팝업형태로 띄웁니다.

반드시 Main UI Thread 상에서 호출하여야 합니다.

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| activity      | 현재 Activity 객체                                           |
| title         | 광고 리스트의 타이틀을 지정함  (기본값 : 무료 포인트 받기)   |
|adListType | 광고 리스트의 타입 (ALL : 보상형과 구매형 모두 표시, PPI : 보상형, CPS : 구매형) |
| listnener     | TnkAdListener 객체. 자세한 내용은 아래 [[Listener 이용하기](#listener-이용하기)] 내용을 참고해주세요. |
| userLayout    | 원하는 Layout을 지정할 수 있습니다. 자세한 내용은  [[디자인 변경하기](#라-디자인-변경하기)] 내용을 참고해주세요. |

##### 적용예시

```java
@Override

public void onCreate(Bundle savedInstanceState) {

    ...

    final Button button = (Button)findViewById(R.id.main_ad);

    button.setOnClickListener(new OnClickListener() {

        @Override

        public void onClick(View v) {

            TnkSession.popupAdList(MainActivity.this,"Your title here");

        }

    });
}
```

#### 멀티탭 광고 목록 띄우기 (Activity)

자신의 앱에서 탭이 여러개인 광고 목록을 띄우기 위하여 TnkSession.showAdListByType() 함수를 사용합니다. 멀티탭 광고목록을 보여주기 위하여 새로운 Activity를 띄웁니다.

##### Method

- void TnkSession.showAdListByType(Activity activity)
- void TnkSession.showAdListByType(Activity activity, String title, AdListType... adListType)
- void TnkSession.showAdListByType(Activity activity, String title, TnkLayout userLayout, AdListType... adListType)
- void TnkSession.showAdListByType(Activity activity, TnkLayout userLayout, AdListType... adListType)

##### Description

멀티탭 광고 목록 화면 (AdWallActivity)를 화면에 띄웁니다.

반드시 Main UI Thread 상에서 호출하여야 합니다.

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| activity      | 현재 Activity 객체                                           |
| title         | 광고 리스트의 타이틀을 지정함  (기본값 : 무료 포인트 받기)   |
|adListType | 광고 리스트의 타입 (ALL : 보상형과 구매형 모두 표시, PPI : 보상형, CPS : 구매형) |
| userLayout    | 원하는 Layout을 지정할 수 있습니다. 자세한 내용은  [[디자인 변경하기](#라-디자인-변경하기)] 내용을 참고해주세요. |

##### 적용예시

```java
@Override

public void onCreate(Bundle savedInstanceState) {

    ...

    final Button button = (Button)findViewById(R.id.main_ad);

    button.setOnClickListener(new OnClickListener() {

        @Override

        public void onClick(View v) {
            // AdListType은 가변인자로 사용하기 원하는 타입을 n개 넣어주시면 n개만큼 탭이 생성됩니다.
            TnkSession.showAdListByType(MainActivity.this,
                                  "Your title here",
                                  AdListType.ALL,
                                  AdListType.PPI,
                                  AdListType,CPS      
                                 );
        }

    });
}
```

#### AdListView

AdListView는 보상형 광고목록을 제공하는 View 객체입니다. 개발자는 createAdListView() 메소드를 사용하여 AdListView 객체를 생성할 수 있습니다.

생성된 AdListView 객체를 현재 Activity에 팝업형태로 띄우거나 자신의 구성한 화면의 하위 View로 추가(addView) 할 수 있습니다.

##### Method

- AdListView TnkSession.createAdListView(Activity activity)
- AdListView TnkSession.createAdListView(Activity activity, AdListType adListType)
- AdListView TnkSession.createAdListView(Activity activity, AdListType adListType, TnkAdListener listener)
- AdListView TnkSession.createAdListView(Activity activity, boolean popupStyle)
- AdListView TnkSession.createAdListView(Activity activity, boolean popupStyle, TnkAdListener listener)
- AdListView TnkSession.createAdListView(Activity activity, TnkLayout userLayout)
- AdListView TnkSession.createAdListView(Activity activity, TnkLayout userLayout, TnkAdListener listener)
- AdListView TnkSession.createAdListView(Activity activity, TnkLayout userLayout, boolean popupStyle, , AdListType adListType, TnkAdListener listener)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| activity      | 현재 Activity 객체                                           |
| adListType      |  광고 리스트의 타입을 설정합니다. (ALL : 보상형과 구매형 모두 표시, PPI : 보상형, CPS : 구매형)  |
| popupStyle    | 생성되는 AdListView 화면을 팝업 화면 형태(true) 또는 전체 화면 형태(false)로 지정합니다. |
| listnener     | TnkAdListener 객체. 자세한 내용은 아래 [[Listener 이용하기](#listener-이용하기)] 내용을 참고해주세요. |
| userLayout    | 원하는 Layout을 지정할 수 있습니다. 자세한 내용은  [[디자인 변경하기](#라-디자인-변경하기)] 내용을 참고해주세요. |

아래의 메소드들은 AdListView에서 제공하는 기능들입니다.

###### void loadAdList()

- 광고목록을 서버에서 가져와 화면에 뿌려줍니다.
- 주로 AdListView를 하위 View로 추가하는 경우에 사용합니다.


###### void show(Activity activity)

- AdListView를 현재 Activity의 최상위 View로 팝업형태로 띄워줍니다.
- 내부적으로는 activity의 addContentView() 를 사용합니다.
- 화면에 나타날때에 Animation 효과가 적용됩니다.  아래의 setAnimationType() 메소드를 참고하세요.
- 화면에 나타난 후에는 내부적으로 loadAdList()가 호출되어 바로 광고목록이 나타납니다.

###### void setTitle(String title)

- 광고목록 상단 타이틀을 설정합니다.

###### void setListener(TnkAdListener listener)

- AdListView 팝업 화면이 나타날때와 사라질때의 event를 받기 위하여 TnkAdListener 객체를 설정합니다.

- show() 메소드를 사용할 때에만 적용됩니다.

- 자세한 내용은 하단의 TnkAdListener 내용을 참고해주세요.

###### void setAnimationType(int showType, int hideType)

- AdListView를 화면에 팝업으로 띄울 때 사용하는 애니메이션을 지정합니다.
- 나타날 때(showType)와 사라질 때(hideType)을 별도로 지정합니다.
- show() 메소드를 사용할 때에만 적용됩니다.
- 사용가능한 Animation의 종류들은 아래와 같습니다.

| 값                          | 나타날때                                        | 사라질때                                        |
| --------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| TnkSession.ANIMATION_RANDOM | 임의의 애니메이션이 적용됩니다.                 | 임의의 애니메이션이 적용됩니다.                 |
| TnkSession.ANIMATION_NONE   | 애니메이션이 적용되지 않습니다.                 | 애니메이션이 적용되지 않습니다.                 |
| TnkSession.ANIMATION_ALPHA  | 서서히 화면에 나타납니다.                       | 서서히 화면에서 사라집니다.                     |
| TnkSession.ANIMATION_BOTTOM | 아래에서 위로 슬라이드되어 나타납니다.          | 아래로 슬라이드되어 사라집니다.                 |
| TnkSession.ANIMATION_TOP    | 화면 위에서 아래로 슬라이드되어 나타납니다.     | 화면 위로 슬라이드되어 사라집니다.              |
| TnkSession.ANIMATION_LEFT   | 화면 왼쪽에서 슬라이드되어 나타납니다.          | 화면 왼쪽으로 슬라이드되어 사라집니다.          |
| TnkSession.ANIMATION_RIGHT  | 화면 오른쪽에서 슬라이드되어 나타납니다.        | 화면 오른쪽으로 슬라이드되어 사라집니다.        |
| TnkSession.ANIMATION_SPIN   | 화면 중앙에서 빙빙돌면서 커지면서 나타납니다.   | 화면 중앙에서 빙빙돌면서 작아지면서 사라집니다. |
| TnkSession.ANIMATION_FLIP   | 화면 왼쪽에서부터 뒤집히는 방식으로 나타납니다. | 화면 오른쪽으로 뒤집히면서 사라집니다.          |

##### Popup Sample

```java
AdListView adlistView = TnkSession.createAdListView(MainActivity.this, true);
adlistView.setListener(new TnkAdListener() {
  @Override
  public void onClose(int type) {
    Log.d("tnkad", "#### onClose " + type);
  }

  @Override
  public void onShow() {
    Log.d("tnkad", "#### onShow ");
  }

  @Override
  public void onFailure(int errCode) {
  }

  @Override
  public void onLoad() {
  }
});

adlistView.setTitle("Get Free Coins!!");

adlistView.setAnimationType(TnkSession.ANIMATION_BOTTOM, TnkSession.ANIMATION_BOTTOM);

adlistView.show(MainActivity.this);
```

##### Embed Sample

```java
AdListView adlistView = TnkSession.createAdListView(this, true);
adlistView.setTitle("Get Free Coins!!");

ViewGroup viewGroup = (ViewGroup)findViewById(R.id.adlist);
viewGroup.addView(adlistView);

adlistView.loadAdList();
```

#### AdListTabView

AdListTabView 보상형 탭형 광고목록을 제공하는 View 객체입니다. 개발자는 createAdListTabView() 메소드를 사용하여 AdListTabView 객체를 생성할 수 있습니다.

생성된 AdListTabView 객체를 현재 Activity에 팝업형태로 띄우거나 자신의 구성한 화면의 하위 View로 추가(addView) 할 수 있습니다.

##### Method

- AdListTabView TnkSession.createAdListTabView(Activity activity, AdListType... adListType)
- AdListTabView TnkSession.createAdListTabView(Activity activity, String title, AdListType... adListType)
- AdListTabView TnkSession.createAdListTabView(Activity activity, String title, TnkLayout userLayout, AdListType... adListType)
- AdListTabView TnkSession.createAdListTabView(Activity activity, TnkLayout userLayout, AdListType... adListType)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| activity      | 현재 Activity 객체                                           |
| adListType      |  광고 리스트의 타입을 설정합니다. (ALL : 보상형과 구매형 모두 표시, PPI : 보상형, CPS : 구매형)  |
| userLayout    | 원하는 Layout을 지정할 수 있습니다. 자세한 내용은  [[디자인 변경하기](#라-디자인-변경하기)] 내용을 참고해주세요. |

아래의 메소드들은 AdListTabView에서 제공하는 기능들입니다.

###### void setListener(TnkAdListener listener)

- AdListTabView 팝업 화면이 나타날때와 사라질때의 event를 받기 위하여 TnkAdListener 객체를 설정합니다.

- 자세한 내용은 하단의 TnkAdListener 내용을 참고해주세요.

##### Embed Sample

```java
// AdListType은 가변인자로 사용하기 원하는 타입을 n개 넣어주시면 n개만큼 탭이 생성됩니다.
AdListTabView adListTabView = TnkSession.createAdListTabView(this, "Get Free Coins!!", layout, AdListType.ALL, AdListType.PPI, AdListType.CPS);

ViewGroup viewGroup = (ViewGroup)findViewById(R.id.adlist);
viewGroup.addView(adlistView);
```
#### Listener 이용하기

AdListView를 팝업화면으로 화면에 띄울 경우 화면이 나타나는 시점과 화면이 닫히는 시점을 알고 싶을 때 아래의 TnkAdListener 인터페이스를 사용합니다.

TnkAdListener는 원래 전면 광고([Interstitial Ad](http://docs.tnkad.net/tnk-interstitial-ad) 참고)에서 사용되지만 광고 리스트 화면에서도 화면이 팝업형태로 나타날 때 (onShow)와 닫힐 때(onClose)의 이벤트를 받기 위하여 사용될 수 있습니다.

##### TnkAdListener Interface

```java
 // 사용자가 닫기버튼이나 Back key를 눌러서 광고화면을 닫은 경우
 public static final int CLOSE_SIMPLE = 0;

 // 사용자가 광고를 클릭해서 화면이 닫히는 경우
 public static final int CLOSE_CLICK = 1;

 // 종료시 띄워주는 광고화면에서 종료 버튼을 클릭해서 닫은 경우
 public static final int CLOSE_EXIT = 2;

 public static final int FAIL_NO_AD = -1;  // no ad available
 public static final int FAIL_NO_IMAGE = -2; // ad image not available
 public static final int FAIL_TIMEOUT = -3; // ad arrived after 5 secs.
 public static final int FAIL_CANCELED = -4; // ad frequency settings

 public static final int FAIL_SYSTEM = -9;

 /**
  * 팝업 화면이 닫힐 때 호출됩니다.
  * 화면이 닫히는 이유를 파라메터로 전달해 줍니다.
  * @param type
  */
 public void onClose(int type);


 /**
  * 팝업 화면이 나타나는 시점에 호출됩니다.
  */
 public void onShow();

 public void onFailure(int errCode);

 public void onLoad();
}
```

AdListView와 관련되어 TnkAdListener에서 발생하는 이벤트의 내용은 아래와 같습니다.

- onClose(int type) : 팝업 화면이 닫히는 시점에 호출됩니다. 화면이 닫히는 이유가 type 파라메터로 전달됩니다.
- - CLOSE_SIMPLE (0) : 사용자가 전면 화면의 닫기 버튼이나 Back 키를 눌러서 닫은 경우입니다.
  - CLOSE_CLICK (1) : 사용자가 전면 화면의 광고를 클릭하여 해당 광고로 이동하는 경우 입니다.
- onShow() : 팝업화면이 나타날 때 호출됩니다.
- AdListView에서는 위 2가지 이외의 이벤트는 발생하지 않습니다.
