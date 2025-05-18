# portone_flutter
[![pub package](https://img.shields.io/pub/v/portone_flutter.svg)](https://pub.dev/packages/portone_flutter)

---
포트원 V1 플러터 모듈입니다.

## 목차
- [버전정보](CHANGELOG.md)
- [지원정보](SUPPORT.md)
- 설치하기
- 설정하기
  - 공통 사항
  - IOS 설정하기
  - Android 설정하기
  - [실시간 계좌이체 설정하기](example/manuals/TRANS.md)
- [예제](example/README.md)
- [콜백 함수 설정하기](example/manuals/CALLBACK.md)

## 버전정보
최신버전은 [v0.12.0](https://github.com/portone-io/portone_flutter/tree/main) 입니다. 버전 히스토리는 [버전정보](CHANGELOG.md)를 참고하세요.

## 지원정보
포트원 V1 플러터 모듈은 일반/정기결제 및 휴대폰 본인인증 기능을 지원합니다. 결제 모듈이 지원하는 PG사 및 결제수단에 대한 자세한 내용은 [지원정보](SUPPORT.md)를 참고해주세요.

## 설치하기
`pubspec.yaml` 파일에 `portone_flutter` 모듈을 추가해 귀하의 프로젝트에 포트원 V1 플러터 모듈을 설치할 수 있습니다.

```
dependencies:
  portone_flutter: ^0.12.0
```

## 설정하기

### IOS 설정하기
IOS에서 포트원 V1 결제연동 모듈을 사용하기 위해서는 `info.plist` 파일에 아래 3가지 항목을 설정해주셔야 합니다. `[프로젝트 이름]/ios/Runner.xcworkspace` 파일을 열어 왼쪽 프로젝트 패널 > Runner > info.plist 파일을 클릭합니다.

#### 1. App Scheme 등록
외부 결제 앱(예) 페이코, 신한 판 페이)에서 결제 후 돌아올 때 사용할 URL identifier를 설정해야합니다.

![](assets/images/app-scheme-registry.gif)

1. `URL types` 속성을 추가합니다.
2. item `0`를 확장하여 `URL schemes` 속성을 추가합니다.
3. item `0`에 App URL Scheme 값(EX. example)을 작성합니다.

```html
...
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleTypeRole</key>
    <string>Editor</string>
    <key>CFBundleURLSchemes</key>
    <array>
      <!-- URL Scheme 값 설정 -->
      <string>example</string>
    </array>
  </dict>
</array>
...
```

#### 2. 외부 앱 리스트 등록
3rd party앱(예) 카드사 앱, 간편결제 앱 등)을 실행할 수 있도록 외부 앱 리스트를 등록해야합니다. 

1. [LSApplicationQueriesSchemes](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/LaunchServicesKeys.html#//apple_ref/doc/uid/TP40009250-SW14) 속성을 추가합니다.
2. 외부 앱 URL Scheme 값을 하나씩 추가합니다.

```html
...
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>kftc-bankpay</string> <!-- 계좌이체 -->
  <string>ispmobile</string> <!-- ISP모바일 -->
  <string>itms-apps</string> <!-- 앱스토어 -->
  <string>hdcardappcardansimclick</string> <!-- 현대카드-앱카드 -->
  <string>smhyundaiansimclick</string> <!-- 현대카드-공인인증서 -->
  <string>shinhan-sr-ansimclick</string> <!-- 신한카드-앱카드 -->
  <string>smshinhanansimclick</string> <!-- 신한카드-공인인증서 -->
  <string>kb-acp</string> <!-- 국민카드-앱카드 -->
  <string>mpocket.online.ansimclick</string> <!-- 삼성카드-앱카드 -->
  <string>ansimclickscard</string> <!-- 삼성카드-온라인결제 -->
  <string>ansimclickipcollect</string> <!-- 삼성카드-온라인결제 -->
  <string>vguardstart</string> <!-- 삼성카드-백신 -->
  <string>samsungpay</string> <!-- 삼성카드-삼성페이 -->
  <string>scardcertiapp</string> <!-- 삼성카드-공인인증서 -->
  <string>lottesmartpay</string> <!-- 롯데카드-모바일결제 -->
  <string>lotteappcard</string> <!-- 롯데카드-앱카드 -->
  <string>cloudpay</string> <!-- 하나카드-앱카드 -->
  <string>nhappcardansimclick</string> <!-- 농협카드-앱카드 -->
  <string>nonghyupcardansimclick</string> <!-- 농협카드-공인인증서 -->
  <string>citispay</string> <!-- 씨티카드-앱카드 -->
  <string>citicardappkr</string> <!-- 씨티카드-공인인증서 -->
  <string>citimobileapp</string> <!-- 씨티카드-간편결제 -->
  <string>kakaotalk</string> <!-- 카카오톡 -->
  <string>payco</string> <!-- 페이코 -->
  <string>lpayapp</string> <!-- (구)롯데 L페이 -->
  <string>hanamopmoasign</string> <!-- 하나카드 공인인증앱 -->
  <string>wooripay</string> <!-- (구) 우리페이 -->
  <string>nhallonepayansimclick</string> <!-- NH 올원페이 -->
  <string>hanawalletmembers</string> <!-- 하나카드(하나멤버스 월렛) -->
  <string>chaipayment</string> <!-- 차이 -->
  <string>kb-auth</string> <!-- 국민 -->
  <string>hyundaicardappcardid</string>  <!-- 현대카드 -->
  <string>com.wooricard.wcard</string>  <!-- 우리WON페이 -->
  <string>lmslpay</string>  <!-- 롯데 L페이 -->
  <string>lguthepay-xpay</string>  <!-- 페이나우 -->
  <string>liivbank</string>  <!-- Liiv 국민 -->
  <string>supertoss</string> <!-- 토스 -->
  <string>newsmartpib</string> <!-- 우리WON뱅킹 -->
  <string>naversearchthirdlogin</string> <!-- 네이버페이 앱 로그인 -->
</array>
...
```

#### 3. App Transport Security 설정

![](assets/images/allow-arbitrary.gif)

1. `App Transport Security Settings` 속성에 [Allow Arbitrary Loads in Web Content](https://developer.apple.com/documentation/bundleresources/information_property_list/nsapptransportsecurity/nsallowsarbitraryloadsinwebcontent) 속성을 추가합니다.
2. 그 값을 `true`로 설정합니다.

```html
...
<key>NSAppTransportSecurity</key>
<dict>
  <!-- Allow Arbitrary Loads in Web Content 속성을 true로 설정 -->
  <key>NSAllowsArbitraryLoadsInWebContent</key>
  <true/>
  <key>NSAllowsArbitraryLoads</key>
  <true/>
</dict>
...
```

#### 4. PASS 앱 Universal Link 설정 (선택 사항)
Push 알림 없이 PASS 앱(SKT PASS, KT 인증, U+인증)을 실행해 본인인증을 진행하고 앱으로 복귀하기 위해서는 Universal Link 설정이 필요합니다.

##### 4.1 mRedirectUrl 설정
본인인증 요청 시 `CertificationData` 객체의 `mRedirectUrl` 파라미터에 `UrlData.redirectUrl` 값을 설정해야 합니다. 다날의 경우, mRedirectUrl 설정 시 carrier 파라미터로 전달한 통신사 선택을 사용자가 변경할 수 없으므로 주의해주세요.

```dart
import 'package:portone_flutter/model/certification_data.dart';
import 'package:portone_flutter/model/url_data.dart'; // UrlData import 추가

// ...

CertificationData data = CertificationData(
  mRedirectUrl: UrlData.redirectUrl
  // ... 기타 본인인증 데이터
);

// ...
```

##### 4.2 Associated Domains 설정
IOS 프로젝트의 `Runner.entitlements` 파일 또는 Xcode의 Signing & Capabilities 탭에서 Associated Domains 설정을 추가해야 합니다.

1.  Xcode를 사용하여 프로젝트를 엽니다.
2.  **Runner** 타겟을 선택합니다.
3.  **Signing & Capabilities** 탭으로 이동합니다.
4.  **+ Capability** 버튼을 클릭하여 **Associated Domains**를 추가합니다.
5.  Associated Domains 목록에 다음 도메인들을 추가합니다. 각 도메인 앞에는 `applinks:`를 붙여야 합니다.
    *   `applinks:www.sktpass.com`
    *   `applinks:fido.kt.com`
    *   `applinks:fido.uplus.co.kr`

또는 `ios/Runner/Runner.entitlements` 파일을 직접 수정하여 아래와 같이 추가할 수 있습니다.

```xml
<!--?xml version="1.0" encoding="UTF-8"?-->
<plist version="1.0">
<dict>
  <key>com.apple.developer.associated-domains</key>
  <array>
    <string>applinks:www.sktpass.com</string>
    <string>applinks:fido.kt.com</string>
    <string>applinks:fido.uplus.co.kr</string>
    <!-- 기존에 다른 applinks가 있다면 여기에 추가합니다. -->
  </array>
  <!-- 다른 capabilities 설정이 있다면 유지합니다. -->
</dict>
</plist>
```

자세한 Universal Link 설정 방법은 Flutter 공식 문서 [Set up universal links for iOS](https://docs.flutter.dev/cookbook/navigation/set-up-universal-links#add-associated-domains)를 참고하세요.

### Android 설정하기
안드로이드 API 레벨 30에서 특정 카드사로 결제 시도시 `net::ERR_CLEARTEXT_NOT_PERMITTED` 오류가 발생한다는 버그가 보고되었습니다. 이를 해결하기 위해서는 [AndroidManifest.xml](https://github.com/portone-io/portone_flutter/blob/develop/example/android/app/src/main/AndroidManifest.xml#L13) 파일에 아래와 같이 [usesclearTextTraffic](https://developer.android.com/guide/topics/manifest/application-element#usesCleartextTraffic) 속성을 `true`로 설정해주셔야 합니다.

```xml
<manifest ...>
    ...
    <application
        ...
        android:usesCleartextTraffic="true"
    >
    </application>
</manifest>
```

### 실시간 계좌이체 설정하기
웹 표준 이니시스와 나이스 정보통신은 뱅크페이 앱을 통해 실시간 계좌이체를 진행합니다. 뱅크페이에서 결제 인증 후 본래의 앱으로 복귀 해 다음단계로 진행을 하려면 별도 설정이 요구됩니다. 자세한 내용은 [실시간 계좌이체 설정하기](example/manuals/TRANS.md)를 참고해주세요.


## 예제
포트원 V1 플러터 모듈로 아래와 같이 일반/정기결제 및 휴대폰 본인인증 기능을 구현할 수 있습니다. 보다 자세한 내용은 [예제](example/README.md)를 참고하세요.

#### 일반/정기결제 예제
```dart
import 'package:flutter/material.dart';

/* 포트원 V1 결제 모듈을 불러옵니다. */
import 'package:portone_flutter/iamport_payment.dart';
/* 포트원 V1 결제 데이터 모델을 불러옵니다. */
import 'package:portone_flutter/model/payment_data.dart';

class Payment extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return IamportPayment(
      appBar: new AppBar(
        title: new Text('포트원 V1 결제'),
      ),
      /* 웹뷰 로딩 컴포넌트 */
      initialChild: Container(
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/iamport-logo.png'),
              Padding(padding: EdgeInsets.symmetric(vertical: 15)),
              Text('잠시만 기다려주세요...', style: TextStyle(fontSize: 20)),
            ],
          ),
        ),
      ),
      /* [필수입력] 가맹점 식별코드 */
      userCode: 'iamport',
      /* [필수입력] 결제 데이터 */
      data: PaymentData(
        pg: 'html5_inicis',                                          // PG사
        payMethod: 'card',                                           // 결제수단
        name: '포트원 V1 결제데이터 분석',                                  // 주문명
        merchantUid: 'mid_${DateTime.now().millisecondsSinceEpoch}', // 주문번호
        amount: 39000,                                               // 결제금액
        buyerName: '홍길동',                                           // 구매자 이름
        buyerTel: '01012345678',                                     // 구매자 연락처
        buyerEmail: 'example@naver.com',                             // 구매자 이메일
        buyerAddr: '서울시 강남구 신사동 661-16',                         // 구매자 주소
        buyerPostcode: '06018',                                      // 구매자 우편번호
        appScheme: 'example',                                        // 앱 URL scheme
        cardQuota : [2,3]                                            //결제창 UI 내 할부개월수 제한
      ),
      /* [필수입력] 콜백 함수 */
      callback: (Map<String, String> result) {
        Navigator.pushReplacementNamed(
          context,
          '/result',
          arguments: result,
        );
      },
    );
  }
}
```


#### 본인인증 예제

이니시스 통합인증의 경우 다날 휴대폰 본인인증과 달리 `mRedirectUrl` 파라미터를 필수로 설정해주셔야 합니다.

##### 다날 휴대폰 본인인증
```dart
import 'package:flutter/material.dart';

/* 포트원 V1 휴대폰 본인인증 모듈을 불러옵니다. */
import 'package:portone_flutter/iamport_certification.dart';
/* 포트원 V1 휴대폰 본인인증 데이터 모델을 불러옵니다. */
import 'package:portone_flutter/model/certification_data.dart';

class Certification extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return IamportCertification(
      appBar: new AppBar(
        title: new Text('포트원 V1 본인인증'),
      ),
      /* 웹뷰 로딩 컴포넌트 */
      initialChild: Container(
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/iamport-logo.png'),
              Padding(padding: EdgeInsets.symmetric(vertical: 15)),
              Text('잠시만 기다려주세요...', style: TextStyle(fontSize: 20)),
            ],
          ),
        ),
      ),
      /* [필수입력] 가맹점 식별코드 */
      userCode: 'iamport',
      /* [필수입력] 본인인증 데이터 */
      data: CertificationData(
        pg: 'danal',                                                  // PG사
        merchantUid: 'mid_${DateTime.now().millisecondsSinceEpoch}',  // 주문번호
        company: '포트원 V1',                                           // 회사명 또는 URL
        carrier: 'SKT',                                               // 통신사
        name: '홍길동',                                                // 이름
        phone: '01012341234',                                         // 전화번호
      ),
      /* [필수입력] 콜백 함수 */
      callback: (Map<String, String> result) {
        Navigator.pushReplacementNamed(
          context,
          '/result',
          arguments: result,
        );
      },
    );
  }
}
```
##### 이니시스 통합인증
```dart
import 'package:flutter/material.dart';

/* 포트원 V1 휴대폰 본인인증 모듈을 불러옵니다. */
import 'package:portone_flutter/iamport_certification.dart';
/* 포트원 V1 휴대폰 본인인증 데이터 모델을 불러옵니다. */
import 'package:portone_flutter/model/certification_data.dart';

class Certification extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return IamportCertification(
      appBar: new AppBar(
        title: new Text('포트원 V1 본인인증'),
      ),
      /* 웹뷰 로딩 컴포넌트 */
      initialChild: Container(
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Image.asset('assets/images/iamport-logo.png'),
              Padding(padding: EdgeInsets.symmetric(vertical: 15)),
              Text('잠시만 기다려주세요...', style: TextStyle(fontSize: 20)),
            ],
          ),
        ),
      ),
      /* [필수입력] 가맹점 식별코드 */
      userCode: 'iamport',
      /* [필수입력] 본인인증 데이터 */
      data: CertificationData(
        pg: 'inicis_unified',                                         // PG사
        merchantUid: 'mid_${DateTime.now().millisecondsSinceEpoch}',  // 주문번호
        mRedirectUrl: 'https://example.com',                          // 본인인증 후 이동할 URL
      ),
      /* [필수입력] 콜백 함수 */
      callback: (Map<String, String> result) {
        Navigator.pushReplacementNamed(
          context,
          '/result',
          arguments: result,
        );
      },
    );
  }
}
```

## 콜백 함수 설정하기
콜백 함수는 필수입력 필드로, 결제/본인인증 완료 후 라우트 이동을 위해 아래와 같이 로직을 작성할 수 있습니다. 콜백 함수에 대한 자세한 설명은 [콜백 설정하기](example/manuals/CALLBACK.md)를 참고하세요.

```dart
...
callback: (Map<String, String> result) {
  Navigator.pushReplacementNamed(
    context,
    '/result',
    arguments: result,
  );
},
...
```
