# cosmosfarm_members_pre_subscription_checkout

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Page_Builder.class.php:381`
- **실행 시점**: 페이지 빌더가 구독 결제 페이지 요소를 초기화하고, 실제 체크아웃 스킨 템플릿을 렌더링하기 직전에 호출됩니다. 상품 객체가 준비된 상태이므로, 접근 제어·리다이렉트·추가 데이터 프리로딩 등에 활용합니다.
- **인자 정보**:
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 현재 결제하려는 구독 상품 객체. `product_id()`, `name()`, `price()`, `subscription_first_free()`, `subscription_type()`/`subscription_type_format()` 등의 정보를 제공합니다.
- **예제 코드**:

  ```php
  // 특정 역할에게만 결제 페이지 접근 허용
  add_action('cosmosfarm_members_pre_subscription_checkout', function ($product) {
      if (!current_user_can('read')) {
          wp_die(__('You are not allowed to access checkout.', 'textdomain'));
      }

      // 1회 결제(onetime) 상품은 커스텀 알림 후 계속 진행
      if ($product->subscription_type() === 'onetime') {
          add_action('wp_footer', function () use ($product) {
              echo '<script>console.info("Checkout product: ' . esc_js($product->name()) . '");</script>';
          });
      }
  }, 10, 1);

  ```

- **주의 사항**:
  - 이 훅에서 `wp_redirect()`를 사용하는 경우 즉시 `exit;` 호출로 뒤따르는 템플릿 로드를 중단해야 합니다.
  - 유료 결제 전 민감한 검증(로그인 여부, 자격 요건 등)은 이 지점에서 수행하면 UX를 해치지 않습니다.
- **관련 훅**: `cosmosfarm_members_skin_subscription_checkout`, `template_redirect`
