---
layout: default
title: 6. 동영상 광고 (Video Ad)
parent: Tnkfactory SDK DA
nav_order: 6
---

# 6. 동영상 광고 (Video Ad)
{: .no_toc }
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---


동영상 광고는 전면 광고와 사용 방법이 같아서 Placement ID를 생성할 때 동영상 광고 설정을 진행해주시고 [전면 광고 가이드](#2-전면-광고-interstitial-ad)를 그대로 활용하시면 됩니다.

### 리워드 동영상 광고 적립 여부 확인

리워드 동영상 광고의 경우 재생 완료 후 AdListener를 사용하여 적립 여부를 확인할 수 있습니다.

```java
interstitialAdItem.setListener(new AdListener() {
  ...

    /**
     * 광고의 재생이 완료되었을 경우 호출됩니다.
     * @param adItem 광고 아이템
     * @param verifyCode 적립 여부
     */
    @Override
    public void onVideoCompletion(AdItem adItem, int verifyCode) {
        super.onVideoCompletion(adItem, verifyCode);

        if (verifyCode >= VIDEO_VERIFY_SUCCESS_SELF) {
            // 적립 성공
        } else {
            // 적립 실패
        }
    }

  ...
});
```
