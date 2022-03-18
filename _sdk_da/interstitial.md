---
layout: default
title: 2. 전면 광고 (Interstitial Ad)
parent: Tnkfactory SDK DA
nav_order: 2
---

# 2. 전면 광고 (Interstitial Ad)
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### 전면 광고 객체 생성

SDK 클래스들을 import 해주세요.
```java
import com.tnkfactory.ad.*;
```

아래와 같이 Placement ID를 입력하여 전면 광고 객체를 생성합니다.
```java
@Override
public void onCreate(Bundle savedInstanceState) {
  ...

    InterstitialAdItem interstitialAdItem = new InterstitialAdItem(this, "YOUR-PlACEMENT-ID");

  ...
}
```

### 전면 광고 띄우기

#### 광고 로드 후 바로 노출

전면 광고가 로드되는 시점에 바로 광고를 띄우려면 AdListener 를 사용합니다.

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      ...

        // 전면 광고 객체 생성
        InterstitialAdItem interstitialAdItem = new InterstitialAdItem(this,"YOUR-PlACEMENT-ID");
      	// AdListener를 사용해 전면 광고가 로드되는 시점에 노출
        interstitialAdItem.setListener(new AdListener() {
            @Override
            public void onLoad(AdItem adItem) {
                adItem.show();
            }
        });

      	// 전면 광고 로드
        interstitialAdItem.load();

      ...
    }
}
```

#### 광고 로드 후 일정시간 후에 노출

만약 광고를 로드하고 일정시간 후에 광고를 띄우시려면 아래와 같이 광고가 성공적으로 로딩되었는지 확인한 후 광고를 띄우실 수 있습니다.

```java
// 전면 광고 객체 생성
InterstitialAdItem interstitialAdItem = new InterstitialAdItem(this,"YOUR-PlACEMENT-ID");
// 전면 광고 로드
interstitialAdItem.load();

...

// 일정시간 후에 광고가 로드 되었는지 확인 후 show 호출
// load와 show를 동시 호출하면 광고 미로드 상태로 전면 광고가 노출되지 않습니다.
if (interstitialAdItem.isLoaded()) {
    interstitialAdItem.show();
}
```

#### 액티비티 변경 후 노출

```java
...

// InterstitialAdItem 생성한 액티비티가 아닌 액티비티가 변경되었을 경우 아래와 같이
// show() 호출시 Context 교체를 해줘야 현재 화면에서 광고가 노출됩니다.
interstitialAdItem.show(this);
```

### 종료 시 전면 광고 사용 방법

'2-Button' 프레임을 사용하여 앱 종료 시 전면 팝업 광고를 자연스럽게 삽입 가능합니다.

우선 Publisher Site 에서 해당 Placement의 프레임을 2-Button 프레임으로 설정하시고, 앱에서 종료버튼 클릭시 처리내용을 AdListener의 onClose() 에서 아래의 내용을 참고하여 구현하시면 됩니다.

```java
interstitialAdItem.setListener(new AdListener() {
  ...

    /**
     * 화면 닫힐 때 호출됨
     * @param adItem 이벤트 대상이되는 AdItem 객체
     * @param type 0:simple close, 1: auto close, 2:exit
     */
    @Override
    public void onClose(AdItem adItem, int type) {
        // 종료 버튼 선택 시 앱을 종료합니다.
        if (type == AdListener.CLOSE_EXIT) {
            MainActivity.this.finish();
        }
    }

  ...
});
```

### 전면 광고 관리를 위한 클래스 AdManager

Publisher SDK에서 전면 광고를 사용하기 위해서는 InterstitialAdItem 생성하여 광고 로드한 뒤 로딩이 완료되면 광고 노출을 실행해야 합니다. 이때 광고 노출전까지 InterstitialAdItem 객체를 유지해주어야 하는데 액티비티 전환이 일어날 경우 객체를 전달하기 어려운 경우가 발생합니다.

위와 같은 상황에 쉽게 InterstitialAdItem 객체를 유지하고 원하는 액티비티에서 광고 노출을 할 수 있도록 하기 위해 AdManager 클래스가 구현이 되어 있습니다. AdManager는 싱글톤 패턴으로 구현되어 있어 액티비티 1에서 광고를 로드한 뒤 액티비티 2에서 광고를 노출하는 것이 가능합니다.

#### 전면 광고 로드

아래와 같이 loadInterstitialAd()를 사용하여 전면 광고 로드를 실행할 수 있습니다.

```java
// AdListener 미사용시
AdManager.getInstance().loadInterstitialAd(this, "YOUR-PlACEMENT-ID");

// AdListener 사용시
AdManager.getInstance().loadInterstitialAd(this, "YOUR-PlACEMENT-ID", new AdListener() {

    @Override
    public void onLoad(AdItem adItem) {
      ...
    }
});
```

#### 전면 광고 노출

```java
// AdListener 미사용시
AdManager.getInstance().showInterstitialAd(this, "YOUR-PlACEMENT-ID");

// AdListener 사용시
// loadInterstitialAd() 시 등록했던 AdListener를 교체할 때 사용
AdManager.getInstance().showInterstitialAd(this, "YOUR-PlACEMENT-ID",new AdListener() {

    @Override
    public void onShow(AdItem adItem) {
      ...
    }
});
```

#### AdManager를 사용하면 전면 광고 로드와 동시에 노출이 가능

InterstitialAdItem에서는 load() 후 광고 로딩이 완료된 상태에서 show()를 호출해야 광고가 노출되지만 AdManager에서는 아래와 같이 loadInterstitialAd()를 호출함과 동시에 showInterstitialAd()를 호출이 가능합니다. 로드와 노출을 동시에 호출하게 되면 광고 로딩이 완료되는 시점에 노출이 자동으로 호출되어 광고가 보여지게 됩니다.

```
AdManager.getInstance().loadInterstitialAd(this, "YOUR-PlACEMENT-ID");
AdManager.getInstance().showInterstitialAd(this, "YOUR-PlACEMENT-ID");
```
