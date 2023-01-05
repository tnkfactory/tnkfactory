---
layout: default
title: 3. 배너 광고 (Banner Ad)
parent: Tnkfactory SDK DA
nav_order: 3
---

# 3. 배너 광고 (Banner Ad)
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

배너 광고를 사용하는 방법은 XML 뷰 삽입 방식과 뷰 동적 생성 방식 두 가지가 있습니다.

### XML 뷰 삽입 방식

#### 배너 뷰 생성

레이아웃 XML 내에 아래와 같이 배너 뷰를 생성합니다.

이때 Placement ID를 입력해줍니다.

```xml
<RelativeLayout
   ...
   >
      ...

        <com.tnkfactory.ad.BannerAdView
            android:id="@+id/banner_ad_view"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:placement_id="YOUR-PLACEMENT-ID" />

      ...
</RelativeLayout>
```

#### 배너 광고 로드

SDK 클래스들을 import 해주세요.
```java
import com.tnkfactory.ad.*;
```

XML에 삽입된 배너 뷰에 아래와 같이 광고를 로드합니다.

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
    	...

        BannerAdView bannerAdView = findViewById(R.id.banner_ad_view);

    		// 배너 광고 로드
        bannerAdView.load();

    	...
    }
}
```

### 뷰 동적 생성 방식

#### 부모 레이아웃 생성

레이아웃 XML 내에 아래와 같이 배너 뷰를 넣어 줄 부모 레이아웃을 생성합니다.

```xml
<RelativeLayout
   ...
   >
      ...

        <RelativeLayout
            android:id="@+id/banner_ad_layout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

      ...
</RelativeLayout>
```

#### 배너 광고 로드

SDK 클래스들을 import 해주세요.
```java
import com.tnkfactory.ad.*;
```

아래와 같이 Placement ID를 입력하여 배너 뷰 생성 후 배너 광고를 로드해줍니다.

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      ...

        RelativeLayout bannerAdLayout = findViewById(R.id.banner_ad_layout);

      	// 배너 뷰 객체 생성
        BannerAdView bannerAdView = new BannerAdView(this, "YOUR-PLACEMENT-ID");

      	// 부모 레이아웃에 배너 뷰 삽입
        bannerAdLayout.addView(bannerAdView);

      	// 배너 광고 로드
        bannerAdView.load();

      ...
    }
}
```
