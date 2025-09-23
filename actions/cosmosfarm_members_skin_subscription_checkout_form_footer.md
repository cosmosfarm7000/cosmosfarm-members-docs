# cosmosfarm_members_skin_subscription_checkout_form_footer

- **분류**: Action
- **정의 위치**: `skin/default/subscription-checkout.php`, `skin/two/subscription-checkout.php`
- **실행 시점**: 구독 결제 폼 푸터를 출력할 때 호출됩니다. 폼 하단에 커스텀 메시지나 요소를 추가할 수 있습니다.
- **인자 정보**:
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 결제 상품 객체.
  - `$skin (Cosmosfarm_Members_Skin)`: 스킨 객체.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_checkout_form_footer', 'my_custom_checkout_form_footer', 10, 2);
  function my_custom_checkout_form_footer($product, $skin) {
      echo '<p>결제 폼 하단에 표시될 사용자 정의 메시지입니다.</p>';
  }
  ```

- **주의 사항**: 스킨 레이아웃과 충돌하지 않도록 최소한의 마크업을 사용하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_checkout_form_header`
