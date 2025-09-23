# cosmosfarm_members_skin_subscription_checkout

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1360`
- **실행 시점**: 구독 결제 스킨에서 결제 요약/폼 영역을 출력하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_checkout', function ($skin, $product) {
      echo '<div class="checkout-note">' . esc_html__('Please review your order before payment.', 'textdomain') . '</div>';
  }, 10, 2);
  ```

- **주의 사항**:
  - 결제용 스크립트는 보안 상 이유로 테마에 상주시키기보다 `wp_enqueue_script()`로 큐잉하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_checkout_field_template`, `cosmosfarm_members_pre_subscription_checkout`
