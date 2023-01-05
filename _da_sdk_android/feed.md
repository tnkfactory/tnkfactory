---
layout: default
title: 4. 피드형 광고 (Feed Ad)
parent: Tnkfactory SDK DA
nav_order: 4
---

# 4. 피드형 광고 (Feed Ad)
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
피드형 광고를 사용하는 방법은 Xml 방식과 뷰 동적 생성 방식 두 가지가 있습니다.

### Xml 뷰 삽입 방식

#### 피드 뷰 생성

레이아웃 Xml 내에 아래와 같이 피드 뷰를 넣어줍니다.

이때 Placement ID를 입력해줍니다.

```xml
<RelativeLayout
   ...
   >
      ...

        <com.tnkfactory.ad.FeedAdView
            android:id="@+id/feed_ad_view"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            app:placement_id="YOUR-PLACEMENT-ID"/>

      ...
</RelativeLayout>
```

#### 피드 광고 로드

SDK 클래스들을 import 해주세요.
```java
import com.tnkfactory.ad.*;
```

XML에 삽입된 피드 뷰에 아래와 같이 광고를 로드합니다.

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        FeedAdView feedAdView = findViewById(R.id.feed_ad_view);

        // 피드 광고 로드
        feedAdView.load();
    }
}
```

### 뷰 동적 생성 방식

#### 부모 레이아웃 생성

레이아웃 XML 내에 아래와 같이 피드 뷰를 넣어 줄 부모 레이아웃을 생성합니다.

```xml
<RelativeLayout
   ...
   >
      ...

        <RelativeLayout
            android:id="@+id/feed_ad_layout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

      ...
</RelativeLayout>
```

#### 피드 광고 로드

SDK 클래스들을 import 해주세요.
```java
import com.tnkfactory.ad.*;
```

아래와 같이 Placement ID를 입력하여 피드 뷰 생성 후 배너 광고를 로드해줍니다.

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      ...

        RelativeLayout feedAdLayout = findViewById(R.id.feed_ad_layout);

        // 피드 뷰 객체 생성
        FeedAdView feedAdView = new FeedAdView(this, "YOUR-PLACEMENT-ID");

        // 부모 레이아웃에 피드 뷰 삽입
        feedAdLayout.addView(feedAdView);

        // 피드 광고 로드
        feedAdView.load();

      ...
    }
}
```
