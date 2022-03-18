---
layout: default
title: 디자인 변경하기
parent: 2. Publisher API
grand_parent: Tnkfactory SDK Rwd
permalink: /docs/sdk_rwd/publisher_api/style_setting/
nav_order: 4
---

# 디자인 변경하기
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
광고 리스트 화면(AdListView)는 기본 스타일을 그대로 사용하셔도 충분하지만, 원하시는 경우 매체앱과 통일감 있도록 UI를 변경하실 수 있습니다.

AdListView의 UI를 변경하기 위해서 TemplateLayoutUtils와 TnkLayout 기능을 제공합니다.  TemplateLayoutUtils은 다양한 디자인을 쉽게 사용할 수 있도록 몇가지 디자인을 가지고 있으며 원하시는 디자인을 선택하여 사용하시면 됩니다. 만약 TemplateLayoutUtils에서도 원하는 디자인을 찾을 수 없고 기본 화면 구성과 완전히 다르게 UI를 배치하고자 하신다면 TnkLayout 기능를 사용하시어 원하는 화면 구성으로 완전히 변경하실 수 있습니다.

[**템플릿 디자인 보기**](#템플릿-디자인)

## TnkLayout
<br>
TnkLayout 기능을 사용하면 화면 구성 자체를 원하는 UI로 변경이 가능합니다.

SDK에 포함된 템플릿 또한 TnkLayout을 이용해 구성된 UI로 어떤 형태든 원하는 UI로 변경이 가능합니다.



TnkLayout을 적용하기 위한 단계는 다음과 같습니다.

1. 광고 리스트 화면 구성, 리스트 Item의 화면구성(아이콘형, 피드형), 상세 팝업 화면구성을 위한 Layout을 XML로 정의합니다. 3가지 Layout XML을 모두 작성해야하는 것은 아니며 변경하기를 윈하는 Layout만 작성하시면됩니다.
2. 작성한 Layout XML 내에서 정의한 구성 요소의 ID 들을 TnkLayout 객체에 지정합니다.
3. 화면을 띄울때 TnkLayout 객체를 같이 전달합니다.



### TnkLayout 객체


TnkLayout 객체를 생성하시고 아래의 속성값을 지정합니다. 모든 속성을 지정할 필요는 없습니다.

| 광고 목록 화면 Layout        | 상세 설명                                                    |
| ---------------------------- | ------------------------------------------------------------ |
| adwall                       | 광고목록 화면의 Layout을 설정하기 위한 속성                  |
| adwall.numColumnsPortrait    | 화면이 세로 모드일때 item의 컬럼수 (기본값 : 1)              |
| adwall.numColumnsLandscape   | 화면이 가로 모드일때 item의 컬럼수 (기본값 : 2)              |
| adwall.layout                | 광고 목록 화면의 Layout ID                                   |
| adwall.idTitle               | 광고 목록 화면내의 상단 타이틀을 출력하기 위한 TextView의 ID |
| adwall.idList                | 광고 목록을 출력하기 위한 ListView의 ID                      |
| adwall.idClose               | 광고 목록 화면 닫기 용 Button 의 ID                          |
| adwall.idHelpdesk            | 포인트 지급 문의 용 Button 의 ID                             |
| adwall.idListStyle           | 리스트 스타일 변경 Button 의 ID                              |
| adwall.bgListStyleIcon       | Icon형 리스트 스타일 변경 Button 의 배경 이미지 Drawable ID  |
| adwall.bgListStyleFeed       | Feed형 리스트 스타일 변경 Button 의 배경 이미지 Drawable ID  |
| adwall.listDividerHeightIcon | Icon형 리스트 아이템 간 구분선 Height                        |
| adwall.listDividerHeightFeed | Feed형 리스트 아이템 간 구분선 Height                        |
| adwall.isHelpDeskPopupStyle  | 이용문의 팝업 스타일 사용 여부                               |

| 광고 목록의 Header Layout   | 상세 설명                                                    |
| --------------------------- | ------------------------------------------------------------ |
| adwall.header               | 광고 목록 상단 지금 획득 가능 포인트 Layout을 설정하기 위한 속성 |
| adwall.header.layout        | 광고 목록 상단 지금 획득 가능 포인트 Layout 의 ID            |
| adwall.header.idPointAmount | 광고 상단 지금 획득 가능 포인트 TextView 의 ID               |
| adwall.header.idPointUnit   | 광고 상단 지금 획득 가능 포인트 단위 TextView 의 ID          |

| 광고 항목 화면 Layout (아이콘형) | 상세 설명                                                    |
| -------------------------------- | ------------------------------------------------------------ |
| adwall.itemIcon                  | 광고 항목의 Layout을 설정하기 위한 속성                      |
| adwall.itemIcon.layout           | 광고 항목 화면의 Layout ID                                   |
| adwall.itemIcon.height           | 광고 항목 화면의 Height                                      |
| adwall.itemIcon.idIcon           | 광고 아이콘 이미지 용 ImageView 의 ID                        |
| adwall.itemIcon.idTitle          | 광고 명칭 TextView 의 ID                                     |
| adwall.itemIcon.idSubtitle       | 광고 설명 TextView 의 ID                                     |
| adwall.itemIcon.idTag            | 광고 태그 표시용 TextView 의 ID                              |
| adwall.itemIcon.idTagPoint       | 광고 적립금 표시용 TextView 의 ID                            |
| adwall.itemIcon.idTagUnit        | 광고 적립금 단위 표시용 TextView 의 ID                       |
| adwall.itemIcon.idCampnType      | 광고 종류 TextView의 ID                                      |
| adwall.itemIcon.idImage          | 광고 전면 이미지 용 ImageView 의 ID                          |
| adwall.itemIcon.bgItemEven       | 광고 항목 배경을 번갈이 다르게 지정하고 싶을 경우 사용.  짝수번째에 표시할 배경 이미지의 Drawable ID를 지정 |
| adwall.itemIcon.bgItemOdd        | 광고 항목 배경을 번갈이 다르게 지정하고 싶을 경우 사용.   홀수번째에 표시할 배경 이미지의 Drawable ID를 지정 |
| adwall.itemIcon.campn            | 광고 종료 TextView의 배경 이미지와 색상을 정의 (아래 별도 설명) |
| adwall.itemIcon.tag              | 광고 적립금 표시용 Tag의 배경 이미지와 색상을 정의 (아래 별도 설명) |

| 광고 항목 화면 Layout (피드형) | 상세 설명                                                    |
| -------------------------------- | ------------------------------------------------------------ |
| adwall.itemFeed              | 광고 항목의 Layout을 설정하기 위한 속성                      |
| adwall.itemFeed.layout       | 광고 항목 화면의 Layout ID                                   |
| adwall.itemFeed.height       | 광고 항목 화면의 Height                                      |
| adwall.itemFeed.idIcon       | 광고 아이콘 이미지 용 ImageView 의 ID                        |
| adwall.itemFeed.idTitle      | 광고 명칭 TextView 의 ID                                     |
| adwall.itemFeed.idSubtitle   | 광고 설명 TextView 의 ID                                     |
| adwall.itemFeed.idTag        | 광고 태그 표시용 TextView 의 ID                              |
| adwall.itemFeed.idTagPoint   | 광고 적립금 표시용 TextView 의 ID                            |
| adwall.itemFeed.idTagUnit    | 광고 적립금 단위 표시용 TextView 의 ID                       |
| adwall.itemFeed.idCampnType  | 광고 종류 TextView의 ID                                      |
| adwall.itemFeed.idImage      | 광고 전면 이미지 용 ImageView 의 ID                          |
| adwall.itemFeed.bgItemEven   | 광고 항목 배경을 번갈이 다르게 지정하고 싶을 경우 사용.  짝수번째에 표시할 배경 이미지의 Drawable ID를 지정 |
| adwall.itemFeed.bgItemOdd    | 광고 항목 배경을 번갈이 다르게 지정하고 싶을 경우 사용.   홀수번째에 표시할 배경 이미지의 Drawable ID를 지정 |
| adwall.itemFeed.campn        | 광고 종료 TextView의 배경 이미지와 색상을 정의 (아래 별도 설명) |
| adwall.itemFeed.tag          | 광고 적립금 표시용 Tag의 배경 이미지와 색상을 정의 (아래 별도 설명) |

| 광고 상세 화면 Layout            | 상세 설명                                                    |
| -------------------------------- | ------------------------------------------------------------ |
| adwall.detail                    | 광고 상세 화면의 Layout을 설정하기 위한 속성                 |
| adwall.detail.layout             | 광고 상세 화면의 Layout ID                                   |
| adwall.detail.idHeaderTitle      | 광고 상세 화면의 헤더 타이틀 TextView ID                     |
| adwall.detail.idIcon             | 광고 아이콘 이미지 용 ImageView 의 ID                        |
| adwall.detail.idTitle            | 광고 명칭 TextView 의 ID                                     |
| adwall.detail.idSubtitle         | 광고 설명 TextView 의 ID                                     |
| adwall.detail.idTag              | 광고 태그 표시용 TextView 의 ID                              |
| adwall.detail.idAction           | 사용자 수행 내용 표시 TextView 의 ID                         |
| adwall.detail.idActionList       | 사용자 수행 내용 표시 리스트 ViewGrop 의 ID                  |
| adwall.detail.idConfirm          | 이동(광고 참여) Button 의 ID                                 |
| adwall.detail.idCancel           | 닫기 Button 의 ID                                            |
| adwall.detail.idJoinDesc         | 참여시 주의사항 TextView 의 ID                               |
| adwall.detail.idAppDesc          | 설명문 TextView 의 ID                                        |
| adwall.detail.idAppDescSeparator | 참여시 주의 사항과 설명문 사이의 구분선 View 의 ID           |
| adwall.detail.idContent          | 광고 컨텐츠 ViewGroup 의 ID (이미지 or 비디오 표시)          |
| adwall.detail.idCampnType        | 광고 종류 TextView의 ID                                      |
| adwall.detail.confirmText        | 이동 버튼 Default Text                                       |
| adwall.detail.confirmTextCPS     | 이동 버튼 Default Text (구매형)                              |
| adwall.detail.campn              | 광고 종료 TextView의 배경 이미지와 색상을 정의 (아래 별도 설명) |
| adwall.detail.tag                | 광고 적립금 표시용 Tag의 배경 이미지와 색상을 정의 (아래 별도 설명) |

| 사용자 수행 내용 Layout | 상세 설명                            |
| --------------------- | -------------------------------------------------------- |
| adwall.detail.actionItem | 사용자 수행 내용 Layout을 설정하기 위한 속성 |
| adwall.detail.actionItem.layout | 사용자 수행 내용 Layout ID |
| adwall.detail.actionItem.idTag | 태그 TextView 의 ID |
| adwall.detail.actionItem.idAction | 설명 TextView 의 ID |
| adwall.detail.actionItem.idTagPoint | 태그 포인트 TextView 의 ID |
| adwall.detail.actionItem.idTagUnit | 태그 포인트 단위 TextView 의 ID |

| Campaign 속성 | 상세 설명                            |
| ------------- | ------------------------------------ |
| bgCampnCPI    | CPI인 경우 배경 이미지의 Drawable ID |
| bgCampnCPS    | CPS인 경우 배경 이미지의 Drawable ID |
| tcCampnCPI    | CPI인 경우 Text Color 값 (ARGB)      |
| tcCampnCPS    | CPS의 Text Color 값 (ARGB)           |

| Tag 속성        | 상세 설명                                               |
| --------------- | ------------------------------------------------------- |
| bgTagNormal     | 참여 전 대상 태그 TextView 의 배경 이미지 Drawable ID   |
| bgTagCheck      | 참여 확인 대상 태그 TextView 의 배경 이미지 Drawable ID |
| tcTagNormal     | 참여 전 대상 태그 TextView 의 Text Color 값 (ARGB)      |
| tcTagCheck      | 참여 확인 대상 태그 TextView 의 Text Color 값 (ARGB)    |
| tagNormalFormat | 참여 전 대상 태그 TextView 의 텍스트 포맷               |
| tagCheckformat  | 참여 확인 대상 태그 TextView 의 텍스트 포맷             |
| pointFormat     | 포인트 TextView 의 포맷                                 |
| pointUnitFormat | 포인트 단위 TextView 의 포맷                            |


### 적용예시

#### 광고 목록 화면 Layout XML 작성

> offerwall_layout.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <RelativeLayout
        android:id="@+id/com_tnk_offerwall_layout_header"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:background="@color/com_tnk_offerwall_list_header_blue">

        <Button
            android:id="@+id/com_tnk_offerwall_layout_help"
            android:layout_width="24dp"
            android:layout_height="24dp"
            android:layout_alignParentLeft="true"
            android:layout_centerVertical="true"
            android:layout_marginLeft="10dp"
            android:background="@drawable/com_tnk_icon_help"/>

        <TextView
            android:id="@+id/com_tnk_offerwall_layout_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_toRightOf="@+id/com_tnk_offerwall_layout_help"
            android:layout_toLeftOf="@+id/com_tnk_offerwall_layout_style"
            android:layout_centerVertical="true"
            android:layout_marginLeft="45dp"
            android:layout_marginRight="10dp"
            android:textColor="@color/color_white"
            android:textSize="20dp"
            android:maxLines="1"
            android:ellipsize="end"
            android:gravity="center"
            tools:text="Test Title Test TitleTest Title Test Title" />

        <Button
            android:id="@+id/com_tnk_offerwall_layout_style"
            android:layout_width="20dp"
            android:layout_height="20dp"
            android:layout_toLeftOf="@+id/com_tnk_offerwall_layout_close"
            android:layout_centerVertical="true"
            android:layout_marginRight="15dp"
            android:background="@drawable/com_tnk_icon_feed"/>

        <Button
            android:id="@+id/com_tnk_offerwall_layout_close"
            android:layout_width="20dp"
            android:layout_height="20dp"
            android:layout_alignParentRight="true"
            android:layout_centerVertical="true"
            android:layout_marginRight="10dp"
            android:background="@drawable/com_tnk_icon_close"/>

    </RelativeLayout>

    <ListView
        android:id="@+id/com_tnk_offerwall_layout_adlist"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:divider="#EEEEEE"
        android:dividerHeight="5dp"
        android:background="@color/com_tnk_offerwall_list_bg_color"/>
</LinearLayout>
```

#### 광고 목록의 Header Layout XML 작성

> offerwall_layout_header.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/color_white">

    <TextView
        android:id="@+id/com_tnk_offerwall_layout_header_msg"
        android:layout_width="match_parent"
        android:layout_height="40dp"
        android:layout_alignParentLeft="true"
        android:layout_toLeftOf="@+id/com_tnk_offerwall_layout_header_point"
        android:layout_marginLeft="10dp"
        android:textSize="14dp"
        android:lines="1"
        android:maxLines="1"
        android:ellipsize="end"
        android:gravity="center_vertical"
        android:text="지금 획득 가능한 코인"/>

    <TextView
        android:id="@+id/com_tnk_offerwall_layout_header_point"
        android:layout_width="wrap_content"
        android:layout_height="40dp"
        android:layout_toLeftOf="@+id/com_tnk_offerwall_layout_header_unit"
        android:textColor="@color/color_blue"
        android:textSize="16dp"
        android:textStyle="bold"
        android:lines="1"
        android:maxLines="1"
        android:gravity="center"
        tools:text="9999999"/>

    <TextView
        android:id="@+id/com_tnk_offerwall_layout_header_unit"
        android:layout_width="wrap_content"
        android:layout_height="40dp"
        android:layout_alignParentRight="true"
        android:layout_marginLeft="5dp"
        android:layout_marginRight="10dp"
        android:textColor="@color/color_blue"
        android:textSize="16dp"
        android:textStyle="bold"
        android:lines="1"
        android:maxLines="1"
        android:gravity="center"
        android:text="코인"/>
</RelativeLayout>
```



#### 광고 항목 화면 Layout XML 작성

리스트 스타일은 아이콘형과 피드형 총 2가지가 존재합니다. 둘 다 변경을 원하시는 경우 두 레이아웃 모두 작성하셔야 합니다.

> offerwall_item_icon.xml (아이콘형)

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="10dp"
    android:background="@drawable/com_tnk_offerwall_item_bg">

    <ImageView
        android:id="@+id/com_tnk_offerwall_item_icon"
        android:layout_width="70dp"
        android:layout_height="70dp"
        android:layout_centerVertical="true"
        android:layout_alignParentLeft="true"
        android:layout_marginRight="8dp"
        android:scaleType="fitXY"
        tools:background="@color/color_orange"/>

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:layout_toRightOf="@+id/com_tnk_offerwall_item_icon"
        android:layout_toLeftOf="@+id/com_tnk_offerwall_item_tag_container">

        <TextView
            android:id="@+id/com_tnk_offerwall_item_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_above="@+id/com_tnk_offerwall_item_campaign"
            android:textColor="@color/com_tnk_offerwall_item_title_text_color"
            android:textSize="15dp"
            android:textStyle="bold"
            android:maxLines="2"
            android:ellipsize="end"
            android:gravity="center_vertical"
            tools:text="Test Title Test Title Test Title Test Title Test Title Test Title Test Title Test Title Test Title"
            tools:background="@color/color_blue"/>

        <TextView
            android:id="@+id/com_tnk_offerwall_item_campaign"
            android:layout_width="wrap_content"
            android:layout_height="20dp"
            android:layout_alignParentBottom="true"
            android:paddingLeft="10dp"
            android:paddingRight="10dp"
            android:textSize="11dp"
            android:lines="1"
            android:maxLines="1"
            android:ellipsize="end"
            android:gravity="center_vertical"
            tools:text="액션형"
            tools:textColor="@color/color_blue"
            tools:background="@drawable/com_tnk_campaign_label_cpi"/>
    </RelativeLayout>

    <RelativeLayout
        android:id="@+id/com_tnk_offerwall_item_tag_container"
        android:layout_width="55dp"
        android:layout_height="55dp"
        android:layout_centerVertical="true"
        android:layout_alignParentRight="true"
        android:layout_marginLeft="8dp" >

        <TextView
            android:id="@+id/com_tnk_offerwall_item_tag"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingTop="10dp"
            android:textSize="13dp"
            android:textColor="@color/color_blue"
            android:textStyle="bold"
            android:gravity="center_horizontal"
            tools:text="7777777"
            tools:background="@drawable/com_tnk_tag_label_square_blue" />

        <TextView
            android:id="@+id/com_tnk_offerwall_item_tag_unit"
            android:layout_width="match_parent"
            android:layout_height="17dp"
            android:layout_alignParentBottom="true"
            android:textSize="11dp"
            android:textColor="@color/color_white"
            android:gravity="center_horizontal"
            tools:text="코인받기"/>
    </RelativeLayout>
</RelativeLayout>
```

> offerwall_item_feed.xml (피드형)

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/color_white">

    <ImageView
        android:id="@+id/com_tnk_offerwall_item_image"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:adjustViewBounds="true"
        tools:layout_height="250dp"
        tools:background="#FF9800"/>

    <RelativeLayout
        android:layout_width="match_parent"
        android:layout_height="80dp"
        android:layout_below="@+id/com_tnk_offerwall_item_image"
        android:layout_margin="10dp">

        <TextView
            android:id="@+id/com_tnk_offerwall_item_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_toLeftOf="@+id/com_tnk_offerwall_item_tag_container"
            android:textSize="15dp"
            android:textColor="@color/com_tnk_offerwall_item_title_text_color"
            android:textStyle="bold"
            android:lines="1"
            android:maxLines="1"
            android:ellipsize="end"
            tools:text="Test Title Test Title Test Title Test Title Test Title"
            tools:background="@color/color_blue"/>

        <TextView
            android:id="@+id/com_tnk_offerwall_item_sub_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@+id/com_tnk_offerwall_item_title"
            android:layout_above="@+id/com_tnk_offerwall_item_campaign"
            android:layout_toLeftOf="@+id/com_tnk_offerwall_item_tag_container"
            android:textSize="13dp"
            android:textColor="@color/com_tnk_offerwall_item_subtitle_text_color"
            android:lines="2"
            android:maxLines="2"
            android:ellipsize="end"
            tools:text="Test Sub Title Test Sub Title Test Sub Title Test Sub Title Test Sub Title Test Sub Title Test Sub Title Test Sub Title"
            tools:background="@color/color_yellow"/>

        <TextView
            android:id="@+id/com_tnk_offerwall_item_campaign"
            android:layout_width="wrap_content"
            android:layout_height="20dp"
            android:layout_alignParentBottom="true"
            android:paddingLeft="10dp"
            android:paddingRight="10dp"
            android:textSize="11dp"
            android:lines="1"
            android:maxLines="1"
            android:ellipsize="end"
            android:gravity="center_vertical"
            tools:text="액션형"
            tools:textColor="@color/color_blue"
            tools:background="@drawable/com_tnk_campaign_label_cpi"/>

        <RelativeLayout
            android:id="@+id/com_tnk_offerwall_item_tag_container"
            android:layout_width="55dp"
            android:layout_height="55dp"
            android:layout_centerVertical="true"
            android:layout_alignParentRight="true"
            android:layout_marginLeft="8dp" >

            <TextView
                android:id="@+id/com_tnk_offerwall_item_tag"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:paddingTop="10dp"
                android:textSize="13dp"
                android:textColor="@color/color_blue"
                android:textStyle="bold"
                android:gravity="center_horizontal"
                tools:text="7777777"
                tools:background="@drawable/com_tnk_tag_label_square_blue" />

            <TextView
                android:id="@+id/com_tnk_offerwall_item_tag_unit"
                android:layout_width="match_parent"
                android:layout_height="17dp"
                android:layout_alignParentBottom="true"
                android:textSize="11dp"
                android:textColor="@color/color_white"
                android:gravity="center_horizontal"
                tools:text="코인받기"/>
        </RelativeLayout>
    </RelativeLayout>
</RelativeLayout>
```

#### 광고 상세 화면 Layout XML 작성

> offerwall_detail.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/color_white">

    <RelativeLayout
        android:id="@+id/com_tnk_offerwall_detail_header"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:background="@color/com_tnk_offerwall_list_header_blue">

        <TextView
            android:id="@+id/com_tnk_offerwall_detail_header_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_toLeftOf="@+id/com_tnk_offerwall_detail_close"
            android:layout_centerVertical="true"
            android:layout_marginLeft="34dp"
            android:textColor="@color/color_white"
            android:textSize="20dp"
            android:gravity="center"
            android:text="무료 코인 받기" />

        <Button
            android:id="@+id/com_tnk_offerwall_detail_close"
            android:layout_width="20dp"
            android:layout_height="20dp"
            android:layout_alignParentRight="true"
            android:layout_centerVertical="true"
            android:layout_marginRight="10dp"
            android:background="@drawable/com_tnk_icon_close"/>
    </RelativeLayout>

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@+id/com_tnk_offerwall_detail_header">

        <RelativeLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@+id/com_tnk_offerwall_detail_header">

            <ImageView
                android:id="@+id/com_tnk_offerwall_detail_image"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_alignParentTop="true"
                android:adjustViewBounds="true"
                tools:layout_height="350dp"
                tools:background="#FF9800"/>

            <TextView
                android:id="@+id/com_tnk_offerwall_detail_title"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_below="@+id/com_tnk_offerwall_detail_image"
                android:layout_marginTop="15dp"
                android:layout_marginLeft="10dp"
                android:layout_marginRight="10dp"
                android:textColor="@color/com_tnk_offerwall_detail_title_text_color"
                android:textSize="17sp"
                android:textStyle="bold"
                android:maxLines="2"
                android:ellipsize="end"
                tools:text="Test Title Tes Test Title Test Title Test Title Test Title Tes Test Title Test Title Test Title Test Title Test Title"
                tools:background="@color/color_blue"/>

            <TextView
                android:id="@+id/com_tnk_offerwall_detail_sub_title"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_below="@+id/com_tnk_offerwall_detail_title"
                android:layout_marginTop="5dp"
                android:layout_marginLeft="10dp"
                android:layout_marginRight="10dp"
                android:textColor="@color/com_tnk_offerwall_detail_subtitle_text_color"
                android:textSize="13sp"
                android:maxLines="2"
                android:ellipsize="end"
                tools:text="Test Description Test Description Test Description Test Description Test Description Test Description Test Description Test Description"
                tools:background="@color/color_yellow"/>

            <View
                android:id="@+id/com_tnk_offerwall_detail_separator_1"
                android:layout_width="match_parent"
                android:layout_height="0.5dp"
                android:layout_below="@+id/com_tnk_offerwall_detail_sub_title"
                android:layout_marginTop="15dp"
                android:layout_marginBottom="10dp"
                android:background="#aaa" />

            <LinearLayout
                android:id="@+id/com_tnk_offerwall_detail_action_items"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_below="@+id/com_tnk_offerwall_detail_separator_1"
                android:layout_marginBottom="10dp"
                android:orientation="vertical"
                tools:layout_height="50dp"/>

            <TextView
                android:id="@+id/com_tnk_offerwall_detail_confirm"
                android:layout_width="match_parent"
                android:layout_height="60dp"
                android:layout_below="@+id/com_tnk_offerwall_detail_action_items"
                android:textSize="25dp"
                android:textStyle="bold"
                android:textColor="@color/color_white"
                android:gravity="center"
                android:background="@color/color_blue"
                tools:text="코인받기" />

            <TextView
                android:id="@+id/com_tnk_offerwall_detail_join_desc"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_below="@+id/com_tnk_offerwall_detail_confirm"
                android:paddingTop="10dp"
                android:paddingLeft="15dp"
                android:paddingRight="15dp"
                android:textSize="13sp"
                android:textColor="@color/com_tnk_offerwall_detail_desc_text_color"
                android:lineSpacingExtra="2dp"
                tools:text="참여시 주의사항"/>

            <View
                android:id="@+id/com_tnk_offerwall_detail_separator_2"
                android:layout_width="match_parent"
                android:layout_height="0.5dp"
                android:layout_below="@+id/com_tnk_offerwall_detail_join_desc"
                android:layout_marginLeft="10dp"
                android:layout_marginRight="10dp"
                android:layout_marginBottom="35dp"
                android:background="#aaa" />

            <TextView
                android:id="@+id/com_tnk_offerwall_detail_app_desc"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_below="@+id/com_tnk_offerwall_detail_separator_2"
                android:paddingLeft="15dp"
                android:paddingRight="15dp"
                android:textSize="13sp"
                android:textColor="@color/com_tnk_offerwall_detail_desc_text_color"
                android:lineSpacingExtra="2dp"
                tools:text="앱 설명문"/>

            <View
                android:id="@+id/com_tnk_offerwall_detail_bottom_margin"
                android:layout_width="match_parent"
                android:layout_height="40dp"
                android:layout_below="@id/com_tnk_offerwall_detail_app_desc"/>
        </RelativeLayout>
    </ScrollView>
</RelativeLayout>
```



##### TnkLayout 객체 생성 및 AdListView 띄우기

```java
public class OfferwallTemplateActivity extends AppCompatActivity {
	...

    @Override
    protected void onCreate(Bundle savedInstanceState) {
    	...

        TnkSession.showAdList(OfferwallTemplateActivity.this, "Title", makeCustomLayout());

    	...
    }

    private TnkLayout makeCustomLayout() {
        TnkLayout res = new TnkLayout();

        res.adwall.layout = com.tnkfactory.ad.R.layout.com_tnk_offerwall_layout_blue;
        res.adwall.idTitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_title;
        res.adwall.idList = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_adlist;
        res.adwall.idClose = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_close;
        res.adwall.idHelpdesk = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_help;
        res.adwall.idListStyle = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_style;
        res.adwall.bgListStyleIcon = com.tnkfactory.ad.R.drawable.com_tnk_icon_list;
        res.adwall.bgListStyleFeed = com.tnkfactory.ad.R.drawable.com_tnk_icon_feed;
        res.adwall.listDividerHeightIcon = 3;
        res.adwall.listDividerHeightFeed = 20;

        res.adwall.header.layout = com.tnkfactory.ad.R.layout.com_tnk_offerwall_layout_header_blue;
        res.adwall.header.idPointAmount = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_header_point;
        res.adwall.header.idPointUnit = com.tnkfactory.ad.R.id.com_tnk_offerwall_layout_header_unit;

        res.adwall.itemIcon.layout = com.tnkfactory.ad.R.layout.com_tnk_offerwall_item_icon_square;
        res.adwall.itemIcon.idIcon = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_icon;
        res.adwall.itemIcon.idTitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_title;
        res.adwall.itemIcon.idTag = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_tag;
        res.adwall.itemIcon.idTagUnit = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_tag_unit;
        res.adwall.itemIcon.idCampnType = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_campaign;
        res.adwall.itemIcon.campn.bgCampnCPI = com.tnkfactory.ad.R.drawable.com_tnk_campaign_label_cpi;
        res.adwall.itemIcon.campn.bgCampnCPS = com.tnkfactory.ad.R.drawable.com_tnk_campaign_label_cps;
        res.adwall.itemIcon.campn.tcCampnCPI = Color.parseColor("#28A5FF");
        res.adwall.itemIcon.campn.tcCampnCPS = Color.parseColor("#CC003F");
        res.adwall.itemIcon.tag.bgTagNoraml = com.tnkfactory.ad.R.drawable.com_tnk_tag_label_square_blue;
        res.adwall.itemIcon.tag.bgTagCheck = com.tnkfactory.ad.R.drawable.com_tnk_tag_label_square_grey;
        res.adwall.itemIcon.tag.tcTagNormal = Color.parseColor("#28A5FF");
        res.adwall.itemIcon.tag.tcTagCheck = Color.parseColor("#BDBDBD");
        res.adwall.itemIcon.tag.tagNormalFormat = "{point}";
        res.adwall.itemIcon.tag.tagCheckFormat = "{point}";
        res.adwall.itemIcon.tag.pointUnitFormat = "{unit}받기";

        res.adwall.itemFeed.layout = com.tnkfactory.ad.R.layout.com_tnk_offerwall_item_feed_square;
        res.adwall.itemFeed.idImage = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_image;
        res.adwall.itemFeed.idTitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_title;
        res.adwall.itemFeed.idSubtitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_sub_title;
        res.adwall.itemFeed.idTag = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_tag;
        res.adwall.itemFeed.idTagUnit = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_tag_unit;
        res.adwall.itemFeed.idCampnType = com.tnkfactory.ad.R.id.com_tnk_offerwall_item_campaign;
        res.adwall.itemFeed.campn.bgCampnCPI = com.tnkfactory.ad.R.drawable.com_tnk_campaign_label_cpi;
        res.adwall.itemFeed.campn.bgCampnCPS = com.tnkfactory.ad.R.drawable.com_tnk_campaign_label_cps;
        res.adwall.itemFeed.campn.tcCampnCPI = Color.parseColor("#28A5FF");
        res.adwall.itemFeed.campn.tcCampnCPS = Color.parseColor("#CC003F");
        res.adwall.itemFeed.tag.bgTagNoraml = com.tnkfactory.ad.R.drawable.com_tnk_tag_label_square_blue;
        res.adwall.itemFeed.tag.bgTagCheck = com.tnkfactory.ad.R.drawable.com_tnk_tag_label_square_grey;
        res.adwall.itemFeed.tag.tcTagNormal = Color.parseColor("#28A5FF");
        res.adwall.itemFeed.tag.tcTagCheck = Color.parseColor("#BDBDBD");
        res.adwall.itemFeed.tag.tagNormalFormat = "{point}";
        res.adwall.itemFeed.tag.tagCheckFormat = "{point}";
        res.adwall.itemFeed.tag.pointUnitFormat = "{unit}받기";

        res.adwall.detail.layout = com.tnkfactory.ad.R.layout.com_tnk_offerwall_detail_blue;
        res.adwall.detail.idHeaderTitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_header_title;
        res.adwall.detail.idCancel = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_close;
        res.adwall.detail.idImage = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_image;
        res.adwall.detail.idTitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_title;
        res.adwall.detail.idSubtitle = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_sub_title;
        res.adwall.detail.idConfirm = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_confirm;
        res.adwall.detail.idJoinDesc = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_join_desc;
        res.adwall.detail.idAppDescSeparator = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_separator_2;
        res.adwall.detail.idAppDesc = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_app_desc;
        res.adwall.detail.idActionList = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_action_items;
        res.adwall.detail.actionItem.layout = com.tnkfactory.ad.R.layout.com_tnk_offerwall_detail_action_item_blue;
        res.adwall.detail.actionItem.idAction = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_aciton_item_desc;
        res.adwall.detail.actionItem.idTagPoint = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_aciton_item_point;
        res.adwall.detail.actionItem.idTagUnit = com.tnkfactory.ad.R.id.com_tnk_offerwall_detail_aciton_item_unit;
        res.adwall.detail.confirmText = "{unit}받기";
        res.adwall.detail.confirmTextCPS = "구매하고 {unit}받기";
        return res;
    }

  ...
}
```

## 템플릿 디자인 제공

SDK는 템플릿 디자인 16가지를 내장하고 있습니다. 내장되어 있는 디자인은 TemplateLayoutUtils을 통해 사용이 가능합니다.

```java
// Blue Style
TemplateLayoutUtils.getBlueStyle_01(); // IconItem : Basic Square / FeedItem : Square
TemplateLayoutUtils.getBlueStyle_02(); // IconItem : Basic Square / FeedItem : Button
TemplateLayoutUtils.getBlueStyle_03(); // IconItem : Basic Ellipse / FeedItem : Square
TemplateLayoutUtils.getBlueStyle_04(); // IconItem : Basic Ellipse / FeedItem : Button
TemplateLayoutUtils.getBlueStyle_05(); // IconItem : Tall Square / FeedItem : Square
TemplateLayoutUtils.getBlueStyle_06(); // IconItem : Tall Square / FeedItem : Button
TemplateLayoutUtils.getBlueStyle_07(); // IconItem : Tall Ellipse / FeedItem : Square
TemplateLayoutUtils.getBlueStyle_08(); // IconItem : Tall Ellipse / FeedItem : Button

// Red Style
TemplateLayoutUtils.getRedStyle_01(); // IconItem : Basic Square / FeedItem : Square
TemplateLayoutUtils.getRedStyle_02(); // IconItem : Basic Square / FeedItem : Button
TemplateLayoutUtils.getRedStyle_03(); // IconItem : Basic Ellipse / FeedItem : Square
TemplateLayoutUtils.getRedStyle_04(); // IconItem : Basic Ellipse / FeedItem : Button
TemplateLayoutUtils.getRedStyle_05(); // IconItem : Tall Square / FeedItem : Square
TemplateLayoutUtils.getRedStyle_06(); // IconItem : Tall Square / FeedItem : Button
TemplateLayoutUtils.getRedStyle_07(); // IconItem : Tall Ellipse / FeedItem : Square
TemplateLayoutUtils.getRedStyle_08(); // IconItem : Tall Ellipse / FeedItem : Button

```

### 사용방법 예시

```java
// 광고 목록 (Activity)
TnkSession.showAdList(this, "Title", TemplateLayoutUtils.getBlueStyle_01());

// 광고 목록 (View)
TnkSession.popupAdList(this, "Title", null, TemplateLayoutUtils.getBlueStyle_01());

// AdListView
TnkSession.createAdListView(this, TemplateLayoutUtils.getBlueStyle_01());
```

### 템플릿 디자인
---
**BlueStyle_01**

![BlueStyle_01](/assets/sdk_rwd/style_setting/BlueStyle_01.png)

**BlueStyle_02**

![BlueStyle_02](/assets/sdk_rwd/style_setting/BlueStyle_02.png)

**BlueStyle_03**

![BlueStyle_03](/assets/sdk_rwd/style_setting/BlueStyle_03.png)

**BlueStyle_04**

![BlueStyle_04](/assets/sdk_rwd/style_setting/BlueStyle_04.png)

**BlueStyle_05**

![BlueStyle_05](/assets/sdk_rwd/style_setting/BlueStyle_05.png)

**BlueStyle_06**

![BlueStyle_06](/assets/sdk_rwd/style_setting/BlueStyle_06.png)

**BlueStyle_07**

![BlueStyle_07](/assets/sdk_rwd/style_setting/BlueStyle_07.png)

**BlueStyle_08**

![BlueStyle_08](/assets/sdk_rwd/style_setting/BlueStyle_08.png)



**RedStyle_01**

![RedStyle_01](/assets/sdk_rwd/style_setting/RedStyle_01.png)

**RedStyle_02**

![RedStyle_02](/assets/sdk_rwd/style_setting/RedStyle_02.png)

**RedStyle_03**

![RedStyle_03](/assets/sdk_rwd/style_setting/RedStyle_03.png)

**RedStyle_04**

![RedStyle_04](/assets/sdk_rwd/style_setting/RedStyle_04.png)
**RedStyle_05**

![RedStyle_05](/assets/sdk_rwd/style_setting/RedStyle_05.png)
**RedStyle_06**

![RedStyle_06](/assets/sdk_rwd/style_setting/RedStyle_06.png)
**RedStyle_07**

![RedStyle_07](/assets/sdk_rwd/style_setting/RedStyle_07.png)
**RedStyle_08**

![RedStyle_08](/assets/sdk_rwd/style_setting/RedStyle_08.png)

## 문의하기, 스타일 변경, 닫기 버튼 기능 구현

TnkLayout을 사용하면 통합오퍼월의 거의 모든 디자인을 변경할 수 있어 문의하기, 스타일 변경, 닫기 버튼의 위치나 이미지의 변경이 가능합니다.

### 구현방법

- 커스텀 레이아웃 Xml 생성
- 커스텀 레이아웃과 각 뷰의 ID를 TnkLayout에 연결
- TnkLayout 사용하여 AdListView 생성

### 적용예시

**custom_offerwall_layout.xml 생성**

```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <RelativeLayout
        android:id="@+id/layout_title"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:layout_alignParentTop="true"
        android:background="#000000">

        <Button
            android:id="@+id/btn_style"
            android:layout_width="20dp"
            android:layout_height="20dp"
            android:layout_alignParentLeft="true"
            android:layout_centerVertical="true"
            android:layout_marginLeft="15dp"
            android:background="@drawable/icon_feed"/>

        <TextView
            android:id="@+id/txt_title"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_toRightOf="@+id/btn_style"
            android:layout_toLeftOf="@+id/btn_close"
            android:layout_centerVertical="true"
            android:textColor="#FFFFFF"
            android:textSize="20dp"
            android:maxLines="1"
            android:ellipsize="end"
            android:gravity="center"
            tools:text="Test Title" />

        <Button
            android:id="@+id/btn_close"
            android:layout_width="20dp"
            android:layout_height="20dp"
            android:layout_alignParentRight="true"
            android:layout_centerVertical="true"
            android:layout_marginRight="10dp"
            android:background="@drawable/icon_close"/>
    </RelativeLayout>

    <ListView
        android:id="@+id/list_ad"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@+id/layout_title"
        android:layout_above="@+id/btn_help"
        android:divider="#EEEEEE"
        android:dividerHeight="3dp"
        android:background="#FFFFFF"/>

    <Button
        android:id="@+id/btn_help"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        android:layout_alignParentBottom="true"
        android:text="포인트 지급 관련 문의하기"/>
</RelativeLayout>
```

![custom_layout_01](/assets/sdk_rwd/style_setting/custom_layout_01.png)

**activity_layout_custom.xml**

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <!-- 오퍼월을 삽입할 컨테이너 -->
    <FrameLayout
        android:id="@+id/container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@id/my_text"
        android:layout_above="@id/bottom_buttons" />
</LinearLayout>
```

**LayoutCustomActivity**

```java
public class LayoutCustomActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_layout_custom);

        // 기본 스타일 TnkLayout 가져오기 (베이스 디자인)
        TnkLayout customLayout = TemplateLayoutUtils.getBlueStyle_01();

        /*
         * 레이아웃 커스텀을 위해 custom_offerwall_layout.xml을 생성 후 각 뷰의 id를 TnkLayout에 연결해줍니다.
         */
        // 레이아웃 xml 지정 (필수)
        customLayout.adwall.layout = R.layout.custom_offerwall_layout;
        // 리스트 뷰 id 연결 (필수)
        customLayout.adwall.idList = R.id.list_ad;
        // 타이틀 텍스트뷰 id 연결
        customLayout.adwall.idTitle = R.id.txt_title;
        // 닫기 버튼 뷰 id 연결
        customLayout.adwall.idClose = R.id.btn_close;
        // 문의하기 버튼 뷰 id 연결
        customLayout.adwall.idHelpdesk = R.id.btn_help;
        // 스타일 변경 버튼 뷰 id 연결
        customLayout.adwall.idListStyle = R.id.btn_style;
        // 스타일 변경 버튼 이미지 지정 - 아이콘형
        customLayout.adwall.bgListStyleIcon = R.drawable.icon_list;
        // 스타일 변경 버튼 이미지 지정 - 피드형
        customLayout.adwall.bgListStyleFeed = R.drawable.icon_feed;
        // 리스트 아이템 간격 지정 - 아이콘형 스타일
        customLayout.adwall.listDividerHeightIcon = 3;
        // 리스트 아이템 간격 지정 - 피드형 스타일
        customLayout.adwall.listDividerHeightFeed = 20;

        // AdListView 생성 - 위에서 만든 customLayout 사용
        AdListView offerwallView = TnkSession.createAdListView(this, customLayout);

        // AdListView 삽입
        ViewGroup.LayoutParams layoutParams = new ViewGroup.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT);
        addContentView(offerwallView, layoutParams);

        // 리스트 로드
        offerwallView.loadAdList();

        // 닫기 버튼
        Button btn_close = offerwallView.getCloseButton();
        btn_close.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                finish();
            }
        });
    }
}
```
