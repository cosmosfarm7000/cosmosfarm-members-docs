# cosmosfarm_members_skin_subscription_checkout_field_after

- **분류**: Action
- **정의 위치**: `skin/default/subscription-checkout.php`, `skin/two/subscription-checkout.php`
- **실행 시점**: 구독 결제 폼의 필드 섹션 종료 후에 호출됩니다. 필드 출력 후에 커스텀 요소를 추가할 수 있습니다.
- **인자 정보**:
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 결제 상품 객체.
  - `$skin (Cosmosfarm_Members_Skin)`: 스킨 객체.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_checkout_field_after', 'my_custom_field_after', 10, 2);
  function my_custom_field_after($product, $skin) {
      echo '</div>';
  }
  ```

- **주의 사항**: 필드 섹션 전체에 적용되는 커스텀 요소를 추가할 때 사용하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_checkout_field_before`
