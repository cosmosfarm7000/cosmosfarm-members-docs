# cosmosfarm_members_skin_subscription_product_single_template

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1137`
- **실행 시점**: 단일 구독 상품 상세 템플릿에서 메인 콘텐츠를 출력하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_single_template', function ($skin, $product) {
      echo '<section class="hero">' . esc_html($product->name()) . '</section>';
  }, 10, 2);
  ```

- **주의 사항**:
  - 상세 페이지 레이아웃과 충돌하지 않도록 최소한의 래퍼를 사용하세요.
- **관련 훅**: `cosmosfarm_members_pre_subscription_checkout`
