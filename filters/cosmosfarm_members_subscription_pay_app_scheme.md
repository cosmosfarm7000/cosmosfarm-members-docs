# cosmosfarm_members_subscription_pay_app_scheme

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 모바일 앱에서 구독 결제를 진행할 때 사용할 앱 스킴을 설정할 때 실행됩니다. 결제 완료 후 앱으로 돌아가기 위한 스킴을 지정할 수 있습니다.
- **인자 정보**:
  - `$scheme (string)`: 앱 스킴 (예: 'myapp://payment').
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_subscription_pay_app_scheme', 'my_custom_pay_app_scheme', 10, 2);
function my_custom_pay_app_scheme($scheme, $product) {
    return 'mycustomapp://payment';
}
```

- **주의 사항**: 필터 함수는 반드시 문자열(앱 스킴)을 반환해야 합니다. 모바일 앱에서 결제 후 돌아올 때 사용되는 URL 스킴입니다.
- **관련 훅**: `cosmosfarm_members_subscription_iamport_pg_mid`
