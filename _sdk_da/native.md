---
layout: default
title: 5. 네이티브 광고 (Native Ad)
parent: Tnkfactory SDK DA
nav_order: 5
---

# 5. 네이티브 광고 (Native Ad)
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

### 레이아웃 생성

네이티브 광고를 보여줄 레이아웃(native_ad_item.xml)을 생성합니다.

아래 레이아웃은 예시이며 실제로 사용시 원하시는 구조로 만드시면 됩니다.

```xml
<RelativeLayout
	android:layout_width="match_parent"
	android:layout_height="wrap_content"
	android:padding="6dp"
	android:background="#DDDDDD">

	<RelativeLayout
		android:id="@+id/native_ad_image_layout"
		android:layout_width="match_parent"
		android:layout_height="wrap_content">

		<FrameLayout
			android:id="@+id/native_ad_content"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"/>

		<ImageView
			android:id="@+id/native_ad_watermark_container"
			android:layout_width="wrap_content"
			android:layout_height="wrap_content"
			android:layout_alignParentRight="true"/>
	</RelativeLayout>

	<RelativeLayout
		android:layout_width="match_parent"
		android:layout_height="wrap_content"
		android:layout_marginTop="10dp"
		android:layout_below="@+id/native_ad_image_layout">

		<ImageView
			android:id="@+id/native_ad_icon"
			android:layout_width="72dp"
			android:layout_height="72dp"
			android:layout_alignParentTop="true"
			android:layout_alignParentLeft="true"
			android:padding="4dp"
			android:scaleType="fitXY"/>
		<TextView
			android:id="@+id/native_ad_title"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:layout_toRightOf="@id/native_ad_icon"
			android:layout_alignParentTop="true"
			android:layout_marginTop="3dp"
			android:layout_marginLeft="8dp"
			android:gravity="center_vertical"
			android:textColor="#ff020202"
			android:textSize="17sp"/>
		<TextView
			android:id="@+id/native_ad_desc"
			android:layout_width="match_parent"
			android:layout_height="wrap_content"
			android:layout_toRightOf="@id/native_ad_icon"
			android:layout_below="@id/native_ad_title"
			android:layout_marginLeft="8dp"
			android:layout_marginTop="8dp"
			android:gravity="center_vertical"
			android:textColor="#ff179dce"
			android:textSize="13sp"/>
	</RelativeLayout>
</RelativeLayout>
```

### 네이티브 객체 생성

SDK 클래스들을 import 해주세요.
```java
import com.tnkfactory.ad.*;
```

```java
@Override
public void onCreate(Bundle savedInstanceState) {
  ...

    NativeAdItem nativeAdItem = new NativeAdItem(this, "YOUR-PlACEMENT-ID");

  ...
}
```

### 네이티브 광고 띄우기

#### 광고 로드 후 바로 노출

네이티브 광고가 로드되는 시점에 바로 광고를 띄우려면 AdListener 를 사용합니다.

```java
public class MainActivity extends AppCompatActivity {
  ...

    @Override
    protected void onCreate(Bundle savedInstanceState) {
      ...

        NativeAdItem nativeAdItem = new NativeAdItem(this, "YOUR-PlACEMENT-ID");

        // AdListener를 사용해 네이티브 광고가 로드되는 시점에 노출
        nativeAdItem.setListener(new AdListener() {

            @Override
            public void onLoad(AdItem adItem) {
                // 네이티브 광고 노출
                showNativeAd((NativeAdItem) adItem);
            }
        });

        // 네이티브 광고 로드
        nativeAdItem.load();

      ...
    }

  ...

    // 네이티브 광고 노출
    private void showNativeAd(NativeAdItem nativeAdItem) {

        if (nativeAdItem != null & nativeAdItem.isLoaded()) {

            // 네이티브 광고가 삽입될 컨테이너 초기화
            ViewGroup adContainer = findViewById(R.id.native_ad_container);
            adContainer.removeAllViews();

            // 컨테이너에 네이티브 아이템 레이아웃 삽입
            ViewGroup view = (ViewGroup) View.inflate(this, R.layout.native_ad_item, adContainer);

            // 네이티브 바인더 객체 생성
            // 생성자에 메인 컨텐츠가 표시될 뷰 ID 필수 입력
            NativeViewBinder binder = new NativeViewBinder(R.id.native_ad_content);

            // 네이티브 바인더 셋팅
            binder.iconId(R.id.native_ad_icon)
                    .titleId(R.id.native_ad_title)
                    .textId(R.id.native_ad_desc)
                    .watermarkIconId(R.id.native_ad_watermark_container)
                    .addClickView(R.id.native_ad_content);

            // 네이티브 광고 노출
            nativeAdItem.attach(view, binder);
        }
    }

  ...
}
```

#### 광고 로드 후 일정시간 후에 노출

만약 광고를 로드하고 일정시간 후에 광고를 띄우시려면 아래와 같이 광고가 성공적으로 로딩되었는지 확인한 후 광고를 띄우실 수 있습니다.

```java
// 전면 광고 객체 생성
NativeAdItem nativeAdItem = new NativeAdItem(this,"YOUR-PlACEMENT-ID");
// 네이티브 광고 로드
nativeAdItem.load();

...

// 일정시간 후에 광고가 로드 되었는지 확인 후 show 호출
// load와 show를 동시 호출하면 광고 미로드 상태로 전면 광고가 노출되지 않습니다.
if (nativeAdItem.isLoaded()) {

    // 네이티브 광고가 삽입될 컨테이너 초기화
    ViewGroup adContainer = findViewById(R.id.native_ad_container);
    adContainer.removeAllViews();

    // 컨테이너에 네이티브 아이템 레이아웃 삽입
 		ViewGroup view = (ViewGroup) View.inflate(this, R.layout.native_ad_item, adContainer);

    // 네이티브 바인더 객체 생성
    // 생성자에 메인 컨텐츠가 표시될 뷰 ID 필수 입력
    NativeViewBinder binder = new NativeViewBinder(R.id.native_ad_content);

    // 네이티브 바인더 셋팅
    binder.iconId(R.id.native_ad_icon)
            .titleId(R.id.native_ad_title)
            .textId(R.id.native_ad_desc)
            .watermarkIconId(R.id.native_ad_watermark_container)
            .addClickView(R.id.native_ad_content);

    // 네이티브 광고 노출
    nativeAdItem.attach(view, binder);
}
```


## 광고 정보를 사용하여 직접 광고 출력 구현


### 광고 타이틀

광고의 타이틀을 출력하기 위한 광고 타이틀을 반환하는 함수입니다.

##### Method

- String getAdTitle()

##### Parameters

- none


##### Return

| 데이터 타입 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| String       | 광고의 제목을 반환합니다.                              |

---

### 광고 설명 문구

광고 내용 문구를 반환하는 함수입니다.

##### Method

- String getAdDesc()

##### Parameters

- none

##### Return

| 데이터 타입 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| String       | 광고 내용 문구를 반환합니다.                              |


---

### 광고 아이콘

광고의 아이콘을 반환합니다.

##### Method

- Bitmap getAdIconBitmap()

##### Parameters

- none

##### Return

| 데이터 타입 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| Bitmap       | 광고 이미지뷰, 웹뷰 타입의 컨텐츠는 웹뷰 리턴                              |

---
### 광고 컨텐츠

광고의 컨텐츠가 출력되는 뷰를 반환합니다.
(광고 이미지뷰, 웹뷰 타입의 컨텐츠는 웹뷰 리턴.)
##### Method

- View getImageView(Context)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| context       | 현재 Activity 또는 Context 객체                              |

##### Return

| 데이터 타입 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| View       | 광고 이미지뷰, 웹뷰 타입의 컨텐츠는 웹뷰 리턴.                              |

---

### 워터마크

광고의 아이콘을 반환합니다.

##### Method

- Bitmap getAdMarkBitmap()

##### Parameters

- none

##### Return

| 데이터 타입 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| Bitmap       | 정책 정보를 출력 하기 위해 제공되는 워터마크 이미지 입니다.      |


---

### 이벤트 처리 대상 뷰 지정

광고의 아이콘을 반환합니다.

##### Method

- void setAdEventView(View)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| View       | 터치 이벤트를 처리 할 대상 뷰 입니다.                              |

##### Return

- none

---

### 광고 정책 이동 이벤트 처리 대상 지전

광고의 아이콘을 반환합니다.

##### Method

- void setPolicyEventView(View)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| View       | 정책 정보로 이동시키기 위해 터치 이벤트를 지정 할 뷰 입니다.                           |

##### Return

- none

---

### **광고 노출 이벤트 전달**

광고가 노출되었음을 서버에 전달 하는 함수 입니다.
광고 노출 후 이 함수를 반드시 호출 하셔야 합니다.
이 함수를 호출 하지 않을 경우 불이익을 받을 수 있습니다.

##### Method

- void sendImpression(Context)

##### Parameters

| 파라메터 명칭 | 내용                                                         |
| ------------- | ------------------------------------------------------------ |
| Context       | 현재 Activity 또는 Context 객체                              |

##### Return

 - none
