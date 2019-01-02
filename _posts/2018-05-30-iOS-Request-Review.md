---
title: "iOS Request Review"
date: 2018-05-30 17:08:00 +09:00
categories: iOS Native Code
---

# Unity
## Assets - Plugins - iOS
### iOSRequestView.m

#impot <StoreKit/StoreKit.h>

void requestReview()
{
  [SKStroeReviewController requestReview];
}

### iOSRequestReview.cs
```ruby
using System.Collection;
using System.Collections.Generic;
using UnityEngine;
using System.Runtime.interopServices;

public class iOSRequestReview
{
  [DllImport("__Internal")
  private static extern void requestReview();
  
  public static void RequestReview()
  {
    requestReview();
  }
}
```

### iOSRequestReviewScene.cs
```ruby
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class iOSRequestReviewScene : MonoBehaviour
{
  void OnGUI()
  {
    if (GUI.Button (new Rect(0, 0, 320, 100), "Request Review");
    {
      TouchBtnRequestReview();
    }
  }
  
  void TouchBtnRequestReview()
  {
    iOSReviewRequest.Request();
  }
}
```
빌드 후 xcodeproj 실행 -> 프로비저닝 설정후 빌드를 진행합니다.

저같은 경우에는 Linker Error 가 발생했습니다.

>Showing Recent Issues "_OBJC_CLASS_$_SKStoreReviewController", referenced from: objc-class-ref in iOSReviewRequest.old: symbol(s) not found for architecture arm64 clang: error: linker command failed with exit code 1 (use -v to see invocation)
> 
#문제해결
Build Phases -> Link Binary With Libraries 에 StoreKit.framework 가 없어서 추가한 뒤 빌드하면 문제없이 빌드가 되었습니다.


실행한뒤에 버튼을 클릭해주면 해당하는 어플 내에서 별점 팝업이 나타납니다.
별점을 조절하게 되면 Submit 버튼이 비활성화 되어있는데 테스트 버전에서 나타나는 증상이므로 크게 신경 안 쓰셔도 됩니다.
