# cosmosfarm_members_subscription_iamport_pg_mid

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1338`
- **실행 시점**: 구독 결제 시 아임포트 결제 모듈의 PG MID(결제 대행사 ID)를 설정할 때 실행됩니다. 상품별로 다른 결제 대행사를 사용하도록 설정할 수 있습니다.
- **인자 정보**:
  - `$mid (string)`: 아임포트 PG MID 값.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_iamport_pg_mid', 'my_custom_iamport_pg_mid', 10, 2);
  function my_custom_iamport_pg_mid($mid, $product) {
    // 특정 상품에 대한 다른 MID 사용
    if ($product->ID() === 789) {
        return 'my_special_mid';
    }
    return $mid;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 문자열(MID 값)을 반환해야 합니다. 잘못된 MID를 반환하면 결제에 실패할 수 있습니다.
- **관련 훅**: `cosmosfarm_members_subscription_pay_app_scheme`
