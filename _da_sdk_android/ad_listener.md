---
layout: default
title: 7. AdListener 사용 방법
parent: Tnkfactory SDK DA
nav_order: 7
---

# 7. AdListener 사용 방법
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

전면, 배너, 피드형, 네이티브 등 모든 광고는 setListener()를 통해 AdListener를 등록하여 사용할 수 있습니다.

필요한 메소드만 Override하여 사용하면 됩니다.

```java
public abstract class AdListener {

    public static int CLOSE_SIMPLE = 0; // 클릭하지 않고 그냥 close
    public static int CLOSE_AUTO = 1; // 자동 닫기 시간이 지나서 close
    public static int CLOSE_EXIT = 2; // 전면인 경우 종료 버튼으로 close

    // video completion 확인 코드
    public static int VIDEO_VERIFY_SUCCESS_S2S = 1; // 매체 서버를 통해서 검증됨
    public static int VIDEO_VERIFY_SUCCESS_SELF = 0; // 매체 서버 URL이 설정되지 않아 Tnk 자체 검증
    public static int VIDEO_VERIFY_FAILED_S2S = -1; // 매체 서버를 통해서 지급불가 판단됨
    public static int VIDEO_VERIFY_FAILED_TIMEOUT = -2; // 매체 서버 호출시 타임아웃 발생
    public static int VIDEO_VERIFY_FAILED_NO_DATA = -3; // 광고 송출 및 노출 이력 데이터가 없음
    public static int VIDEO_VERIFY_FAILED_TEST_VIDEO = -4; // 테스트 동영상 광고임
    public static int VIDEO_VERIFY_FAILED_ERROR = -9; // 그외 시스템 에러가 발생

    /**
     * 화면 닫힐 때 호출됨
     * @param adItem 이벤트 대상이되는 AdItem 객체
     * @param type 0:simple close, 1: auto close, 2:exit
     */
    public void onClose(AdItem adItem, int type) {

    }

    /**
     * 광고 클릭시 호출됨
     * 광고 화면은 닫히지 않음
     * @param adItem 이벤트 대상이되는 AdItem 객체
     */
    public void onClick(AdItem adItem) {

    }

    /**
     * 광고 화면이 화면이 나타나는 시점에 호출된다.
     * @param adItem 이벤트 대상이되는 AdItem 객체
     */
    public void onShow(AdItem adItem) {

    }

    /**
     * 광고 처리중 오류 발생시 호출됨
     * @param adItem 이벤트 대상이되는 AdItem 객체
     * @param error AdError
     */
    public void onError(AdItem adItem, AdError error) {

    }

    /**
     * 광고 load() 후 광고가 도착하면 호출됨
     * @param adItem 이벤트 대상이되는 AdItem 객체
     */
    public void onLoad(AdItem adItem) {

    }

    /**
     * 동영상이 포함되어 있는 경우 동영상을 끝까지 시청하는 시점에 호출된다.
     * @param adItem 이벤트 대상이되는 AdItem 객체
     * @param verifyCode 동영상 시청 완료 콜백 결과.
     */
    public void onVideoCompletion(AdItem adItem, int verifyCode) {

    }
}
```
