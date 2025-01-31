## TOAST > TOAST SDK使用ガイド > TOAST IAP > Android

## 事前準備

1\. [TOAST SDK](./getting-started-android)をインストールします。
2\. [TOASTコンソール](https://console.cloud.toast.com)で[IAPサービスを有効化](https://docs.toast.com/ko/Mobile%20Service/IAP/ko/console-guide/#iap-appkey)します。
3\. IAPコンソールで[AppKeyを確認](https://docs.toast.com/ko/Mobile%20Service/IAP/ko/console-guide/#appkey)します。

## ストア別アプリ内決済ガイド

- [Android Developersアプリ内決済](https://developer.android.com/google/play/billing)
- [ONE storeアプリ内決済API V5 (SDK V17)案内およびダウンロード](https://dev.onestore.co.kr/devpoc/reference/view/Tools)
- [Galaxy storeアプリ内課金APIのご案内とダウンロード](https://developer.samsung.com/iap/overview.html)

## ライブラリ設定

- Google Play Storeのアプリ内決済を使用するには、下記のようにbuild.gradleに依存性を追加します。

```groovy
repositories {
    google()
    mavenCentral()
}

dependencies {
    implementation 'com.toast.android:toast-iap-google:0.27.1'
    ...
}
```

- ONE storeのアプリ内決済を使用するには、下記のようにbuild.gradleに依存性を追加します。

```groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.toast.android:toast-iap-onestore:0.27.1'
    ...
}
```

- Galaxy storeのアプリ内決済を使用するには、下記のようにbuild.gradleに依存性を追加します。

```groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.toast.android:toast-iap-galaxy:0.27.1'
    ...
}
```

> Galaxy Store in-app purchases works on Android 4.3 (API level 18) or higher.

## AndroidManifest設定

### ONE store購入画面設定（オプション）

ONE storeは全決済画面とポップアップ決済画面をサポートします。
AndroidManifest.xmlにmeta-dataを追加して、全決済画面（"full"）またはポップアップ決済画面（"popup"）を選択することができます。
メタデータが設定されていない場合は、デフォルト（ "full"）が適用されます。

```xml
<application
  ...>
  <meta-data android:name="iap:view_option" android:value="popup | full"/>
</application>
```

| 決済画面 | 設定値 |
| -- | -- |
| 全決済画面 | "full" |
| ポップアップ決済画面 | "popup" |

詳細については、[ワンストア決済画面設定]https://dev.onestore.co.kr/devpoc/reference/view/Tools）を確認してください。

### Android 11 이상을 타겟팅하는 앱 (ONE store, Galaxy Store)

Android 11에서는 앱이 사용자가 기기에 설치한 다른 앱을 쿼리하고 상호작용하는 방법을 변경합니다.
Android 11 이상을 타겟팅하는 앱에서 ONE store 또는 Galaxy Store 결제를 사용하려면 아래와 같이 AndroidManifest.xml에 'queries' 요소를 정의해야합니다.

#### ONE store

```xml
<queries>
    <intent>
        <action android:name="com.onestore.ipc.iap.IapService.ACTION" />
    </intent>
    <intent>
        <action android:name="android.intent.action.VIEW" />
        <data android:scheme="onestore" />
    </intent>
</queries>
```

#### Galaxy Store

```xml
<queries>
    <package android:name="com.sec.android.app.samsungapps" />
</queries>
```

'queries' 요소는 Android Gradle Plugin 4.1 이상에서 동작합니다.
이전 버전의 Android Gradle Plugin을 사용하려면 [Android 11에서 패키지 가시성을 위해 Gradle 빌드 준비](https://android-developers.googleblog.com/2020/07/preparing-your-build-for-package-visibility-in-android-11.html)를 참고하세요.

## ストアコード

| ストア       | コード       |
| ----------- | ---------- |
| Google Play | "GG"       |
| ONE store   | "ONESTORE" |
| Galaxy store | "GALAXY" |

> [参考]ストアコードは[IapStoreCode](./iap-android/#iapstorecode)クラスに定義されています。

## 商品の種類

- 現在サポートしている商品の種類は3本で、消費性商品、サブスクリプションの商品、消費性のサブスクリプションの商品があります。

| 商品名   | 商品タイプ           | 説明                                   |
| ------ | ---------------- | -------------------------------------- |
| 消費性商品 | "CONSUMABLE"     | 消費可能な一回性商品。ゲーム内マネー、メディアファイルなどがあります。 |
| 購読商品 | "AUTO_RENEWABLE" | 指定された間隔および価格で決済が自動的に繰り返される商品。 <br>オンライン雑誌および音楽ストリーミングサービスなどがあります。 |
| Consumable Subscription Products | "CONSUMABLE_AUTO_RENEWABLE" | 소비가 가능한 구독 상품<br>정기적으로 게임내 재화, 아이템 등을 지급하는 결제 방식입니다. |

> Note :Subscription products and Consumable subscription products are supported by Google Play Store only.

## アプリ内決済設定

* [ToastIapConfiguration](./iap-android/#toastiapconfiguration)オブジェクトは、アプリ内決済設定情報を含んでいます。
* [ToastIapConfiguration](./iap-android/#toastiapconfiguration)オブジェクトは、[ToastIapConfiguration.Builder](./iap-android/#toastiapconfigurationbuilder)を使用して作成できます。
* IAPコンソールで発行された[AppKey](https://docs.toast.com/ko/Mobile%20Service/IAP/ko/console-guide/#appkey)を、setAppKeyメソッドを使用して設定します。
* setStoreCodeメソッドを使用して、アプリ内決済に使用する[ストアコード](./iap-android/#_3)を設定します。

### アプリ内決済設定例

```java
ToastIapConfiguration configuration =
    ToastIapConfiguration.newBuilder(getApplicationContext())
                .setAppKey(YOUR_APP_KEY)
                .setStoreCode(IapStoreCode.GOOGLE_PLAY_STORE)
                .build();
```

## アプリ内決済の初期化

- ToastIap.initialize()メソッドを呼び出してTOAST IAPを初期化します。

### アプリ内決済初期化API仕様

* アプリ内決済は、ToastIap.initializeメソッドを使用して初期化します。
* ToastIap.initializeメソッドは、[ToastIapConfiguration.Builder](./iap-android/#toastiapconfigurationbuilder)で作成された[ToastIapConfiguration](./iap-android/#toastiapconfiguration)オブジェクトをパラメータに使用します。

```java
/* ToastIap.java */
public static void initialize(ToastIapConfiguration configuration)
```

| Parameters    |                                    |
| ------------- | ---------------------------------- |
| configuration | ToastIapConfiguration：アプリ内決済設定情報 |

### アプリ内決済初期化例

- ToastIapを初期化します。

> [参考]初期化は、必ずApplication#onCreateで進行する必要があります。

```java
public class MainApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        initializeToastIap();
    }

    /**
     * ToastIapを初期化します。
     */
    private void initializeToastIap() {
        ToastIapConfiguration configuration = ToastIapConfiguration.newBuilder(getApplicationContext())
                .setAppKey(YOUR_APP_KEY)
                .setStoreCode(IapStoreCode.GOOGLE_PLAY_STORE)
                .build();
        ToastIap.initialize(configuration);
    }
}
```

## サービスログイン

* TOAST SDKで提供するすべてのサービス(IAP、Log & Crashなど)は、1つの同じユーザーIDを使用します。
    * [ToastSdk.setUserId](https://docs.toast.com/ko/TOAST/ko/toast-sdk/getting-started-android/#userid)でユーザーIDを設定できます。
    * ユーザーIDを設定していない場合、決済が行われません。
* サービスログイン段階でユーザーID設定、未消費決済履歴照会、有効になっている購読商品照会機能を導入することを推奨します。

### ログイン

```java
// Login.
ToastSdk.setUserId(userId);
```

### ログアウト

```java
// Logout.
ToastSdk.setUserId(null);
```

> [参考]サービスログアウト時に、必ずユーザーIDをnullに設定してください。プロモーションコードが使われたり、決済再処理動作時に誤ったユーザーIDで購入が行われることを防止できます。

## 決済アップデートリスナー登録

* 決済結果は、ToastIapに設定された[IapService.PurchasesUpdatedListener](./iap-android/#iapservicepurchasesupdatedlistener)を通して通知されます。
* 決済アップデートリスナーは、ToastIap.registerPurchasesUpdatedListenerメソッドを使用して登録できます。
* [IapService.PurchasesUpdatedListener](./iap-android/#iapservicepurchasesupdatedlistener)を通して伝達された[IapPurchaseResult](./iap-android/#iappurchaseresult)リストから決済情報を確認できます。

> [参考]決済アップデートリスナーは、Activity.onCreate()で登録し、Activity.onDestroy()で解除する必要があります。

### 決済アップデートリスナー登録API仕様

```java
/* ToastIap.java */
public static void registerPurchasesUpdatedListener(IapService.PurchasesUpdatedListener listener)
public static void unregisterPurchasesUpdatedListener(IapService.PurchasesUpdatedListener listener)
```

| Method                             | Parameters |                                          | Description            |
| ---------------------------------- | ---------- | ---------------------------------------- | ---------------------- |
| registerPurchasesUpdatedListener   | listener   | IapService.<br>PurchasesUpdatedListener: <br>決済アップデートリスナー | 決済アップデートリスナーを登録します。    |
| unregisterPurchasesUpdatedListener | listener   | IapService.<br>PurchasesUpdatedListener: <br>登録解除するリスナー | 決済アップデートリスナー登録を解除します。 |

#### 決済アップデートリスナーの登録例

```java
public class MainActivity extends AppCompatActivity {
    /**
     * アプリ内で消費性商品、購読、プロモーション商品を購入した時、結果を通知します。
     */
    private IapService.PurchasesUpdatedListener mPurchaseUpdatedListener =
            new IapService.PurchasesUpdatedListener() {
                @Override
                public void onPurchasesUpdated(@NonNull List<IapPurchaseResult> purchaseResults) {
                    for (IapPurchaseResult purchaseResult : purchaseResults) {
                        if (purchaseResult.isSuccess()) {
                            // 成功
                            IapPurchase purchase = purchaseResult.getPurchase();
                        } else {
                            // 失敗
                        }
                    }
                }
            };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // onCreateが呼び出された時、Listenerを登録します。
        ToastIap.registerPurchasesUpdatedListener(mPurchaseUpdatedListener);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // onDestroy()が呼び出された時、必ずListenerを削除します。
        ToastIap.unregisterPurchasesUpdatedListener(mPurchaseUpdatedListener);
    }
}
```

> [참고] 결제 결과가 IapService.PurchasesUpdatedListener로 통지되기 전 Activity가 종료되면 결제 데이터가 유실될 수 있습니다.
> 결제를 안전하게 처리하기 위해 결제 결과를 통지받기 전, 사용자가 Activity를 종료(백 버튼 또는 종료 버튼 클릭)할 수 없도록 해야 합니다.

## 商品リスト照会

* IAPコンソールに登録された商品のうち、使用可能な商品リストを照会します。
* IAPコンソールに登録された商品のうち、購入可能な商品は[IapProductDetails](./iap-android/#iapproductdetails)リスト(Product Details List)で返されます。
* IAPコンソールに登録された商品のうち、ストアに登録されていない商品は[IapProduct](./iap-android/#iapproduct)リスト(Invalid Product List)で返されます。

### 商品リスト照会API仕様

```java
/* ToastIap.java */
public static void queryProductDetails(Activity activity,
                                       IapService.ProductDetailsResponseListener listener)
```

| Method              | Parameters |                                          |
| ------------------- | ---------- | ---------------------------------------- |
| queryProductDetails | activity   | Activity: 現在有効になっているActivity               |
|                     | listener   | IapService.<br>ProductDetailsResponseListener: <br>商品照会結果リスナー |


### 商品リスト照会例

```java
/**
 * 購入可能な商品を照会します。
 * <p>
 * productDetails ：購入可能な商品リスト
 * invalidProducts ：TOAST IAPコンソールに商品を登録しましたが、ストアに登録されていない商品
 */
void queryProductDetails() {
    IapService.ProductDetailsResponseListener responseListener =
            new IapService.ProductDetailsResponseListener() {
                @Override
                public void onProductDetailsResponse(@NonNull IapResult result,
                                                     @Nullable List<IapProductDetails> productDetails,
                                                     @Nullable List<IapProduct> invalidProducts) {
                    if (result.isSuccess()) {
                        // 照会成功
                    } else {
                        // 照会失敗
                    }
                }
            }

    ToastIap.queryProductDetails(MainActivity.this, responseListener);
}
```

## 商品購入

* TOAST IAPは、ストアに登録された商品IDを使用して商品を購入できます。
* 商品情報はToastIap.queryProductDetails()メソッドを呼び出して返された[IapProductDetails](./iap-android/#iapproductdetails)オブジェクトに含まれています。
* 商品IDは、IapProductDetails.getProductId()メソッドを使用して獲得できます。
* 商品購入は[IapPurchaseFlowParams](./iap-android/#iappurchaseflowparams)オブジェクトに商品IDを設定した後、ToastIap.launchPurchaseFlow()メソッドを通して購入ステップを開始します。
* [IapPurchaseFlowParams](./iap-android/#iappurchaseflowparams)オブジェクトは、[IapPurchaseFlowParams.Builder](./iap-android/#iappurchaseflowparamsbuilder)を使用して作成できます。
* 商品購入結果は、ToastIapに登録した[IapService.PurchasesUpdatedListener](./iap-android/#iapservicepurchasesupdatedlistener)を通して返されます。

### 商品購入IAP仕様

```java
/* ToastIap.java */
public static void launchPurchaseFlow(Activity activity,
                                      IapPurchaseFlowParams params)
```

| Method             | Parameters |                                   |
| ------------------ | ---------- | --------------------------------- |
| launchPurchaseFlow | activity   | Activity: 現在有効になっているActivity        |
|                    | params     | IapPurchaseFlowParams:購入情報パラメータ |

### 商品購入例

```java
/**
 * 商品を購入します。
 */
void launchPurchaseFlow(Activity activity, String productId) {
    IapPurchaseFlowParams params = IapPurchaseFlowParams.newBuilder()
            .setProductId(productId)
            .build();
    ToastIap.launchPurchaseFlow(activity, params);
}
```
##ユーザーデータ設定

* TOAST IAPは、購入要求時にユーザー情報を追加することができます。
*ユーザー情報は、IapPurchaseFlowParams.BuilderのsetDeveloperPayloadメソッドに設定します。
*固定されたユーザー情報は、未消費決済照会とアクティブなサブスクリプション照会時に返される[IapPurchase](./iap-android / #iappurchase)のgetDeveloperPayloadメソッドで確認できます。

``java
String userData = "userData"
IapPurchase FlowParams params = IapPurchase FlowParams.newBuilder()
.setProductId(productId)
.setDeveloperPayload(userData)
.build()
ToastIap. launchPurchase Flow(activity、params)
````

Googleプレイストアでプロモーションコードで商品を購入した場合は、ユーザーデータは利用できません。

## 未消費決済照会

* まだ消費されていない一回の商品(CONSUMABLE)と消費性購読商品(CONSUMABLE_AUTO_RENEWABLE)情報を照会します。
* ユーザーに商品を支給した後、[Consume API](https://docs.toast.com/en/Mobile%20Service/IAP/en/api-guide-for-toast-sdk/#consume-api)を使用して商品を消費します。
* 未消費決済は、ToastIap.queryConsumablePurchases()メソッドを使用して照会できます。
* 照会結果は、[IapService.PurchasesResponseListener](./iap-android/#iapservicepurchasesresponselistener)を通して[IapPurchase](./iap-android/#iappurchase)オブジェクトリストで返されます。

### 未消費決済照会API仕様

```java
/* ToastIap.java */
public static void queryConsumablePurchases(Activity activity,
                                            IapService.PurchasesResponseListener listener)
```

| Method                   | Parameters |                                          |
| ------------------------ | ---------- | ---------------------------------------- |
| queryConsumablePurchases | activity   | Activity: 現在有効になっているActivity               |
|                          | listener   | IapService.PurchasesResponseListener: <br>未消費購入履歴照会結果リスナー |

### 未消費決済照会例

```java
/**
 * 未消費決済履歴を照会します。
 */
void queryConsumablePurchases() {
    PurchasesResponseListener responseListenr =
            new IapService.PurchasesResponseListener() {
                @Override
                public void onPurchasesResponse(@NonNull IapResult result,
                                                @Nullable List<IapPurchase> purchases) {
                    if (result.isSuccess()) {
                        // 成功
                    } else {
                        // 失敗
                    }
                }
            };
    ToastIap.queryConsumablePurchases(MainActivity.this, responseListenr);
}
```

## 有効になっている購読の照会

* User IDベースで有効になっている購読商品(AUTO_RENEWABLE & CONSUMABLE_AUTO_RENEWABLE)を照会できます。
* 決済が完了した購読商品は、使用期間が残っている場合、継続して照会できます。
* 有効になっている購読は、ToastIap.queryActivatedPurchases()メソッドを使用して照会できます。
* 照会結果は、[IapService.PurchasesResponseListener](./iap-android/#iapservicepurchasesresponselistener)を通して[IapPurchase](./iap-android/#iappurchase)オブジェクトリストに返されます。
* iOSで購読した商品をAndroidでも照会可能です。

> 現在、購読商品はGoogle Playストアのみサポートします。

### 有効になっている購読照会API仕様

```java
/* ToastIap.java */
public static void queryActivatedPurchases(Activity activity,
                                           PurchasesResponseListener listener)
```

| Method                  | Parameters |                                          |
| ----------------------- | ---------- | ---------------------------------------- |
| queryActivatedPurchases | activity   | Activity: 現在有効になっているActivity               |
|                         | listener   | IapService.PurchasesResponseListener: <br>有効になっている購読照会結果リスナー |

### 有効になっている購読照会例

```java
/**
 * 有効になっている購読商品照会
 */
void queryActivatedPurchases() {
    PurchasesResponseListener responseListener =
            new IapService.PurchasesResponseListener() {
                @Override
                public void onPurchasesResponse(@NonNull IapResult result,
                                                @Nullable List<IapPurchase> purchases) {
                    if (result.isSuccess()) {
                        // 成功
                    } else {
                        // 失敗
                    }
                }
            };
    ToastIap.queryActivatedPurchases(MainActivity.this, responseListener);
}
```

## 구독 상태 조회

* User ID 기준으로 구입한 구독 상품의 상태를 조회할 수 있습니다.
* 만료된 구독 상품은 includeExpiredSubscriptions 설정으로 조회 또는 제외할 수 있습니다. (default: false)
* 구독 상품 상태는 ToastIap.querySubscriptionsStatus() 메서드를 사용하여 조회할 수 있습니다.
* 조회 결과는 [IapService.SubscriptionsStatusResponseListener](./iap-android/#iapservicesubscriptionsstatusresponselistener)를 통해 [IapSubscriptionStatus](./iap-android/#iapsubscriptionstatus) 객체 리스트를 반환됩니다.
* [IapSubscriptionStatus](./iap-android/#iapsubscriptionstatus) 사용하는 구독 상태 코드는 [IapSubscriptionStatus.StatusCode](./iap-android/#iapsubscriptionstatusstatusCode)에 정의되어 있습니다.

```
현재 구독 상품은 Google Play 스토어만 지원합니다.
```

### 구독 상태 조회 API 명세

```java
/* ToastIap.java */
public static void querySubscriptionsStatus(Activity activity,
                                            boolean includeExpiredSubscriptions,
                                            IapService.SubscriptionsStatusResponseListener listener)
```

| Method | Parameters |  |
| --- | --- | --- |
| querySubscriptionsStatus | activity | Activity: 현재 활성화된 Activity |
|  | includeExpiredSubscriptions | boolean:<br>구독 만료된 구독 상품의 상태 포함 여부 |
|  | listener | IapService.SubscriptionsStatusResponseListener:<br>구독 상태 조회 결과 리스너 |

### 구독 상태 조회 예시

```java
/**
 * 구독 상태 조회
 */
private void querySubscriptionsStatus() {
    SubscriptionsStatusResponseListener listener =
            new SubscriptionsStatusResponseListener() {
                @Override
                public void onSubscriptionsStatusResponse(@NonNull String storeCode,
                                                          @Nullable List<IapSubscriptionStatus> subscriptionsStatus) {
                    if (result.isSuccess()) {
                        // 성공
                    } else {
                        // 실패
                    }
                }
            };
    ToastIap.querySubscriptionsStatus(MainActivity.this, false, listener);
}
```

## 구글 스토어 구독(정기 결제) 기능

구글 스토어의 구독 결제의 갱신 및 만료와 같은 수명주기에 따른 이벤트를 처리하는 방법을 설명합니다.
자세한 사항은 [정기 결제별 기능 추가](https://developer.android.com/google/play/billing/billing_subscriptions)을 참고하세요.

### 구독 수명 주기 처리

구글 스토어의 구독은 수명주기 동안 다양한 상태 변경을 거치며 앱은 각 상태에 따라 대응해야합니다.

* **활성화 상태(Active)**: 정기 결제 콘텐츠에 엑세스 할 수 있으며 자동 갱신이 진행되는 상태
* **취소(Cancelled)**: 정기 결제 콘텐츠에 엑세스 할 수 있으나 사용자가 구독 상품을 더 이상 사용하지 않는다고 취소하여 자동 갱신이 정지된 상태
* **유예 기간 (In grace period)**: 결제 수단 문제로 정기 결제가 실패하였으나 정기 결제 콘텐츠에는 엑세스 할 수 있는 상태 (사용자가 결제 수단을 변경하기를 기다리는 상태)
* **계정 보류 (On hold)**: 결제 수단 문제로 정기 결제가 실패하여 보류 상태 (유예 기간이 사용 설정되어있다면 유예 기간 동안 결제 수단을 변경하지 않아 결제가 보류된 상태)
* **일시중지 (Pause)**: 정기 결제 상품을 일시적으로 중지한 상태
* **만료 (Expired)**: 정기 결제 상품이 만료된 상태

| 상태 | 미소비 결제 조회<br>(ToastIap.queryConsumablePurchases) | 활성화된 구독 조회<br>(ToastIap.queryActivatedPurchases) | 만료 시간 | 자동 갱신 여부 |
| --- | --- | --- | --- | --- |
| 활성화 상태 (Active) | Yes | Yes | 미래시간 | Yes |
| 취소 (Cancelled) | Yes | Yes | 미래시간 | No |
| 유예 기간 (In grace period) | No | Yes | 미래시간 | Yes |
| 계정 보류 (On hold) | No | No | 과거시간 | Yes |
| 일시중지 (Pause) | No | No | 과거시간 | Yes |
| 만료 (Expired) | No | No | 과거시간 | No |

### 유예 기간

유예 기간이 사용 설정된 경우 결제 주기가 끝날 때 결제 수단에 문제가 있다면 정기 결제는 유예 기간으로 전환됩니다.
<span style="color:#e11d21">유예 기간 동안 사용자는 정기 결제 콘텐츠에 엑세스 할 수 있어야 합니다.</span>
자세한 사항은 [유예 기간](https://developer.android.com/google/play/billing/subs#grace)을 참고하세요.

> <span style="color:#e11d21">**주의!)**</span> 유예 기간 중 결제 수단 수정 등으로 복원되면 자동 갱신을 재개합니다. TOAST IAP는 갱신된 결제건을 결제 업데이트 리스너(IapService.PurchaseUpdatedListener)를 통해 결제 결과를 통지합니다. 게임이나 앱은 중요한 동작 중 결제 업데이트 리스너에 의해 불필요한 팝업이 사용자에게 노출되지 않도록 주의해야합니다.

#### 일반 구독 상품 (AUTO_RENEWABLE))

* 유예 기간 동안 일반 구독 상품은 정기 결제 콘텐츠에 엑세스 할 수 있어야 합니다.
* 유예 기간 동안 ToastIap.queryActivatedPurchases()로 조회할 수 있습니다.

#### 소비성 구독 상품 (CONSUMABLE_AUTO_RENEWABLE)

* 유예 기간이 시작되면 구글은 새로운 영수증을 발급하나 결제 수단을 수정하지 않으면 계정 보류 상태가 되거나 취소됩니다.
* 소비성 구독 상품은 유예 기간 동안 상품을 소비할 수 없도록 ToastIap.queryConsumablePurchases()로 조회되지 않습니다.

### 계정 보류

계정 보류는 결제 수단 문제로 갱신이 실패했을 때의 사용자 상태를 말합니다.
결제에 실패하면 유예 기간 동안 재시도하고, 유예 기간 동안에도 결제가 실패하면 정기 결제 상태는 보류 상태가 됩니다.
계정 보류 상태가 사용자는 정기 결제 콘텐츠에 액세스 할 수 없습니다.
계정 보류 기간은 최대 30일입니다.
계정 보류 기간이 종료되기 전에 결제 수단을 수정하지 않으면 취소 처리됩니다.
자세한 사항은 [계정 보류](https://developer.android.com/google/play/billing/subs#account-hold)를 참고하세요.

> <span style="color:#e11d21">**주의!)**</span> 계정 보류 기간 중 결제 수단 수정 등으로 복원되면 자동 갱신을 재개합니다. TOAST IAP는 갱신된 결제건을 결제 업데이트 리스너(IapService.PurchaseUpdatedListener)를 통해 결제 결과를 통지합니다. 게임이나 앱은 중요한 동작 중 결제 업데이트 리스너에 의해 불필요한 팝업이 사용자에게 노출되지 않도록 주의해야합니다.

#### 일반 구독 상품 (AUTO_RENEWABLE))

* 계정 보류 기간 동안 일반 구독 상품은 정기 결제 콘텐츠에 엑세스 할 수 없습니다.
* 계정 보류 기간 동안 ToastIap.queryActivatedPurchases()로 조회되지 않습니다.

#### 소비성 구독 상품 (CONSUMABLE_AUTO_RENEWABLE)

* 계정 보류 기간 동안 소비성 구독 상품은 새로운 구매를 생성하지 않습니다.
* 계정 보류 기간 동안 ToastIap.queryConsumablePurchases()로 새로운 구매가 조회되지 않습니다.

### 일시중지

일시중지 기능을 설정하면 사용자가 정기 결제를 1주일에서 3개월 사이로 일시중지 할 수 있습니다.
정기 결제 일시중지는 현재 구독 기간이 종료된 이후에 적용됩니다.
일시중지 기간이 끝나면 정기 결제가 자동으로 재개됩니다.
자세한 사항은 [일시중지](https://developer.android.com/google/play/billing/subs#pause)를 참고하세요.

> <span style="color:#e11d21">**주의!)**</span> 일시중지 기간이 끝나면 자동 갱신을 재개합니다. TOAST IAP는 갱신된 결제건을 결제 업데이트 리스너(IapService.PurchaseUpdatedListener)를 통해 결제 결과를 통지합니다. 게임이나 앱은 중요한 동작 중 결제 업데이트 리스너에 의해 불필요한 팝업이 사용자에게 노출되지 않도록 주의해야합니다.

#### 일반 구독 상품 (AUTO_RENEWABLE))

* 일시중지 기간 동안 일반 구독 상품은 정기 결제 콘텐츠에 엑세스 할 수 없습니다.
* 일시중지 기간 동안 ToastIap.queryActivatedPurchases()로 조회되지 않습니다.

#### 소비성 구독 상품 (CONSUMABLE_AUTO_RENEWABLE)

* 일시중지 기간 동안 소비성 구독 상품은 새로운 구매를 생성하지 않습니다.
* 일시중지 기간 동안 ToastIap.queryConsumablePurchases()로 새로운 구매가 조회되지 않습니다.

### 정기 결제 재신청

정기 결제 재신청 기능을 설정하면 사용자가 정기 결제 만료일로 부터 12개월 이내에 취소한 정기 결제를 재신청할 수 있습니다.
정기 결제 재신청은 새 정기 결제 및 구매 토큰이 생성됩니다.
정기 결제가 만료된 이후 사용자는 구글 플레이 정기 결제 센터를 통해 만료 후 1년까지 동일한 상품을 다시 구매할 수 있습니다.
자세한 사항은 [정기 결제 재신청](https://developer.android.com/google/play/billing/subs#resubscribe)을 참고하세요.

> <span style="color:#e11d21">**주의!)**</span> 앱이나 게임 내 화면에서 구매가 진행되지 않으므로 사용자 데이터(IapPurchase.getDeveloperPayload())를 사용할 수 없습니다.
> <span style="color:#e11d21">**주의!)**</span> 구글 플레이 스토어에서 정기 결제 재신청으로 구독 상품을 구매할 경우 TOAST IAP는 구매한 결제건을 결제 업데이트 리스너(IapService.PurchaseUpdatedListener)를 통해 결제 결과를 통지합니다. 게임이나 앱은 중요한 동작 중 결제 업데이트 리스너에 의해 불필요한 팝업이 사용자에게 노출되지 않도록 주의해야합니다.

## TOAST IAP Class Reference

### ToastIapConfiguration

TOAST IAP初期化メソッドのパラメータに使用されるアプリ内決済設定情報です。

```java
/* ToastIapConfiguration.java */
public String getAppKey();
public String getStoreCode();
```

| Method       | Returns |                                     |
| ------------ | ------- | ----------------------------------- |
| getAppKey    | String  | IAPサービスアプリキー                        |
| getStoreCode | String  | ストアコード情報("GG" or "ONESTORE", "GALAXY", ...) |

### ToastIapConfiguration.Builder

IAPサービスアプリキー、ストア種類などを入力し、[ToastIapConfiguration](./iap-android/#toastiapconfiguration)オブジェクトを作成します。

```java
/* ToastIapConfiguration.java */
public void setAppKey(String appKey)
public void setStoreCode(String storeCode)
```

| Method       | Parameters |                     | Description                              |
| ------------ | ---------- | ------------------- | ---------------------------------------- |
| setAppKey    | appKey     | String: IAPサービスアプリキー | TOAST IAPコンソールで作成したアプリキーを設定します。      |
| setStoreCode | storeCode  | String: ストアコード情報 | ストアコードを設定します。<br>("GG" or "ONESTORE", "GALAXY", ...) |

### IapStoreCode

```java
/* IapStoreCode.java */
String GOOGLE_PLAY_STORE
String ONE_STORE
String GALAXY_STORE
```

* GOOGLE_PLAY_STORE<br>Google Playストアアプリ内決済を使用します。<br>Constant Value: "GG"
* ONE_STORE<br>ONE storeアプリ内決済を使用します。<br>Constant Value: "ONESTORE"
* GALAXY_STORE<br>Galaxy storeアプリ内決済を使用します。<br>Constant Value: "GALAXY"

### IapPurchaseResult

* 決済結果および決済情報を含むオブジェクトです。

```java
/* IapPurchaseResult.java */
public IapPurchase getPurchase()
public boolean isSuccess()
public boolean isFailure()
public int getCode()
public String getMessage()
public Throwable getCause()
```

| Method      | Returns     |                                  |
| ----------- | ----------- | -------------------------------- |
| getPurchase | IapPurchase | 決済情報があるIapPurchaseオブジェクトを返します。 |
| getCode     | int         | 決済結果コードを返します。                 |
| getMessage  | String      | 決済結果メッセージを返します。                |
| getCause    | Throwable   | 決済失敗原因を返します。                 |
| isSuccess   | boolean     | 決済に成功したかを返します。                 |
| isFailure   | boolean     | 決済に失敗したかを返します。                 |

### IapResult

```java
/* IapResult.java */
public boolean isSuccess()
public boolean isFailure()
public int getCode()
public String getMessage()
public Throwable getCause()
```

| Method     | Returns   |                |
| ---------- | --------- | -------------- |
| getCode    | int       | 結果コードを返します。  |
| getMessage | String    | 結果メッセージを返します。 |
| getCause   | Throwable | 失敗原因を返します。  |
| isSuccess  | boolean   | 成功したかを返します。  |
| isFailure  | boolean   | 失敗したかを返します。  |

### IapPurchase

* IapPurchaseオブジェクトで、決済情報を確認できます。

```java
/* IapPurchase.java */
public String getPaymentId()
public String getOriginalPaymentId()
public String getPaymentSequence()
public String getProductId()
public String getProductType()
public String getUserId()
public float getPrice()
public String getPriceCurrencyCode()
public String getAccessToken()
public String getPurchaseType()
public String getPurchaseTime()
public String getExpiryTime()
```

| Method               | Returns |                      |
| -------------------- | ------- | -------------------- |
| getPaymentId         | String  | 決済IDを返します。        |
| getOriginalPaymentId | String  | 原本決済IDを返します。     |
| getPaymentSequence   | String  | 決済固有番号を返します。     |
| getProductId         | String  | 商品IDを返します。        |
| getProductType       | String  | 商品タイプを返します。        |
| getUserId            | String  | ユーザーIDを返します。       |
| getPrice             | float   | 価格情報を返します。        |
| getPriceCurrencyCode | String  | 通貨情報を返します。        |
| getAccessToken       | String  | 消費に使用されるトークンを返します。  |
| getPurchaseType      | String  | 商品タイプを返します。        |
| getPurchaseTime      | long    | 商品購入時間を返します。     |
| getExpiryTime        | long    | 購読商品の残り時間を返します。 |

### IapProductDetails

* IapProductDetailsオブジェクトで、商品詳細情報を確認できます。
* TOAST IAPコンソールに登録された情報とGoogle PlayコンソールまたはONE store Developerに登録された詳細な情報を含みます。

```java
/* IapProductDetails.java */
public String getProductId()
public String getProductSequence()
public float getPrice()
public String getLocalizedPrice()
public String getPriceCurrencyCode()
public long getPriceAmountMicros()
public String getFreeTrialPeriod()
public String getSubscriptionPeriod()
public String getProductType()
public String getProductTitle()
public String getProductDescription()
public boolean isActivated()
```

| Method                | Returns |                 |
| --------------------- | ------- | --------------- |
| getProductId          | String  | 商品のID          |
| getProductSequence    | String  | 商品固有番号      |
| getPrice              | float   | 価格            |
| getLocalizedPrice     | String  | 現地価格         |
| getPriceCurrencyCode  | String  | 通貨             |
| getPriceAmountMicros  | long    | 1,000,000単位価格|
| getFreeTrialPeriod    | String  | 無料使用期間      |
| getSubscriptionPeriod | String  | 購読期間         |
| getProductType        | String  | 商品タイプ         |
| getProductTitle       | String  | 商品タイトル(title)    |
| getProductDescription | String  | 商品説明         |
| isActivated           | boolean | 商品が有効になっているか      |

### IapProduct

* TOAST IAPコンソールに登録された簡略な情報を確認できます。

```java
/* IapProduct.java */
public String getProductId()
public String getProductSequence()
public String getProductType()
public String getProductTitle()
public String getProductDescription()
public boolean isActivated()
```

| Method                | Returns |              |
| --------------------- | ------- | ------------ |
| getProductId          | String  | 商品のID       |
| getProductSequence    | String  | 商品固有番号   |
| getProductType        | String  | 商品タイプ      |
| getProductTitle       | String  | 商品タイトル(title) |
| getProductDescription | String  | 商品説明      |
| isActivated           | boolean | 商品が有効になっているか   |

### IapPurchaseFlowParams

* IapPurchaseFlowParamsは、購入しようとする商品情報を含みます。

```java
/* IapPurchaseFlowParams.java */
public String getProductId()
```

| Method       | Returns |       |
| ------------ | ------- | ----- |
| getProductId | String  | 商品ID |

### IapPurchaseFlowParams.Builder

* IapPurchaseFlowParamsオブジェクトを作成します。

```java
/* IapPurchaseFlowParams.java */
public void setProductId(String productId)
```

| Method       | Parameters |               | Description   |
| ------------ | ---------- | ------------- | ------------- |
| setProductId | productId  | String: 商品ID | 商品IDを設定します。 |

### IapSubscriptionStatus

* IapSubscriptionStatus 객체로 구독 상태 정보를 확인할 수 있습니다.
* 구독 상태 코드는 IapSubscriptionStatus.StatusCode에 정의되어 있습니다.

```java
/* IapSubscriptionStatus.java */
public String getStoreCode()
public String getPaymentId()
public String getOriginalPaymentId()
public String getPaymentSequence()
public String getProductId()
public String getProductType()
public String getProductSequence()
public String getUserId()
public float getPrice()
public String getPriceCurrencyCode()
public String getAccessToken()
public String getPurchaseType()
public String getPurchaseTime()
public String getExpiryTime()
public String getDeveloperPayload()
public int getStatusCode()
public String getStatusDescription()
```

| Method | Returns |  |
| --- | --- | --- |
| getStoreCode | String | 스토어 코드를 반환합니다. |
| getPaymentId | String | 결제 ID를 반환합니다. |
| getOriginalPaymentId | String | 원본 결제 ID를 반환합니다. |
| getPaymentSequence | String | 결제 고유 번호를 반환합니다. |
| getProductId | String | 상품 ID를 반환합니다. |
| getProductType | String | 상품 유형을 반환합니다. |
| getProductSeq | String | 상품 고유 번호를 반환합니다. |
| getUserId | String | 사용자 ID를 반환합니다. |
| getPrice | float | 가격 정보를 반환합니다. |
| getPriceCurrencyCode | String | 통화 정보를 반환합니다. |
| getAccessToken | String | 소비에 사용되는 토큰을 반환합니다. |
| getPurchaseType | String | 결제 유형을 반환합니다.<br>"Test" or "Promo" or null |
| getPurchaseTime | long | 상품 구매 시간을 반환합니다. |
| getExpiryTime | long | 구독 상품의 남은 시간을 반환합니다. |
| getDeveloperPayload | String | 사용자 데이터를 반환합니다. |
| getStatusCode | int | 구독 상태 코드를 반환합니다. |
| getStatusDescription | String | 구독 상태 코드에 대한 설명을 반환합니다. |

### IapSubscriptionStatus.StatusCode

* 구독 상태를 나타내는 코드 입니다.

```java
/* IapSubscriptionStatus.java */
int ACTIVE
int CANCELED
int ON_HOLD
int IN_GRACE_PERIOD
int PAUSED
int REVOKED
int EXPIRED
int UNKNOWN
```

| Name | Code | Status | Description |
| --- | --- | --- | --- |
| ACTIVE | 0 | 활성 | 구독이 활성 상태입니다. |
| CANCELED | 3 | 취소 | 구독이 취소되었습니다. |
| ON\_HOLD | 5 | 계정 보류 | 정기 결제가 계정 보류 상태가 되었습니다(사용 설정된 경우). |
| IN\_GRACE\_PERIOD | 6 | 유예 기간 | 정기 결제가 유예 기간 상태로 전환되었습니다(사용 설정된 경우). |
| PAUSED | 10 | 일시 중지 | 구독이 일시 중지되었습니다. |
| REVOKED | 12 | 해지 | 정기 결제가 만료 시간 전에 사용자에 의해 취소되었습니다. |
| EXPIRED | 13 | 만료 | 정기 결제가 만료되었습니다. |
| UNKNOWN | 9999 | 미정의 | 정의 되지 않은 상태입니다. |

### IapService.PurchasesUpdatedListener

* 決済情報がアップデートされた時、IapService.PurchasesUpdatedListenerを継承実装したオブジェクトのonPurchasesUpdatedメソッドを通して通知されます。

```java
void onPurchasesUpdated(List<IapPurchaseResult> purchaseResults)
```

### IapService.PurchasesResponseListener

* 未消費決済照会または有効化された購読の照会時、IapService.PurchasesResponseListenerを継承実装したオブジェクトのonPurchasesResponseメソッドを通して通知されます。

```java
void onPurchasesResponse(IapResult result,
                         List<IapPurchase> purchaseList)
```

### IapService.SubscriptionsStatusResponseListener

* 구독 상태 조회 시 SubscriptionsStatusResponseListener 상속 구현한 객체의 onSubscriptionsStatusResponse 메서드를 통해 통지됩니다.

```java
void onSubscriptionsStatusResponse(IapResult result,
                                   List<IapSubscriptionStatus> subscriptionsStatus);
```

## エラーコード

### 共通エラーコード

| RESULT                 | CODE | DESC                                     |
| ---------------------- | ---- | ---------------------------------------- |
| FEATURE_NOT_SUPPORTED  | -2   | 要請した機能はサポートしません。<br>Requested feature is not supported. |
| SERVICE_DISCONNECTED   | -1   | ストアサービスに接続できませんでした。<br>Store service is not connected. |
| OK                     | 0    | 成功。<br>Success.                          |
| USER_CANCELED          | 1    | ユーザーキャンセル。<br>User canceled.                |
| SERVICE_UNAVAILABLE    | 2    | ネットワークが接続されませんでした。<br>Network connection is down. |
| BILLING_UNAVAILABLE    | 3    | 要請されたタイプに対して、API Versionがサポートされていません。<br>API version is not supported for the type requested. |
| PRODUCT_UNAVAILABLE    | 4    | 要請した商品を使用できません。<br>Requested product is not available. |
| DEVELOPER_ERROR        | 5    | 無効な引数がAPIに提供されました。開発段階で発生するエラーです。<br>Developer error. |
| ERROR                  | 6    | API作業中に深刻なエラーが発生しました。<br>Fatal error during the API action. |
| PRODUCT_ALREADY_OWNED  | 7    | すでに所持している商品のため、購入できませんでした。<br>Failure to purchase since item is already owned. |
| PRODUCT_NOT_OWNED      | 8    | 所持していない商品のため、消費できません。<br>Failure to consume since item is not owned. |
| USER_ID_NOT_REGISTERED | 9    | ユーザーIDが登録されていません。<br>User ID Is not registered. |
| UNDEFINED_ERROR        | 9999 | 定義されていないエラー<br>Undefined error.           |

### サーバーエラーコード

| RESULT                    | CODE | DESC                                     |
| ------------------------- | ---- | ---------------------------------------- |
| INACTIVATED_APP           | 101  | 有効になっていないアプリです。<br>App is not active.     |
| NETOWRK_NOT_CONNECTED     | 102  | ネットワークが接続されていません。<br>Network not connected. |
| VERIFY_PURCHASE_FAILED    | 103  | 決済の検証に失敗しました。<br>Failure to verify purchase. |
| PURCHASE_ALREADY_CONSUMED | 104  | すでに消費した購入です。<br>Purchase already consumed. |
| PURCHASE_ALREADY_REFUNDED | 105  | 返金された購入です。<br>Purchase already refunded. |
| PURCHASE_LIMIT_EXCEEDED   | 106  | 구매 한도를 초과했습니다.<br>Purchase limit exceeded. |

### ONE storeエラーコード

| RESULT                   | CODE | DESC                                     |
| ------------------------ | ---- | ---------------------------------------- |
| ONESTORE_NEED_LOGIN      | 301  | ONE storeサービスにログインしていません。<br>ONE store service is not logged in. |
| ONESTORE_NEED_UPDATE     | 302  | ONE storeサービスがアップデートまたはインストールされませんでした。<br>ONE store service is not updated or installed. |
| ONESTORE_SECURITY_ERROR  | 303  | 正常ではないアプリで決済を要請しました。<br>Abnormal purchase request. |
| ONESTORE_PURCHASE_FAILED | 304  | 決済要請に失敗しました。<br>Purchase request failed. |

### Galaxy storeエラーコード

| RESULT                   | CODE | DESC                                     |
| ------------------------ | ---- | ---------------------------------------- |
| GALAXY_NOT_LOGGED_IN      | 501  | Galaxy storeサービスにログインしていません。<br>Galaxy service is not logged in. |
| GALAXY_NOT_UPDATED     | 502  | Galaxy storeサービスがアップデートまたはインストールされませんでした。<br>Galaxy service is not updated or installed. |
| GALAXY_PURCHASE_FAILED  | 503  | 正常ではないアプリで決済を要請しました。<br>Galaxy purchase failed. |
| GALAXY_SERVICE_DENIED | 504  | 決済要請に失敗しました。<br>PurGalaxy service denied. |
