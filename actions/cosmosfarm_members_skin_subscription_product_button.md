# cosmosfarm_members_skin_subscription_product_button

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1036`
- **실행 시점**: 구독 상품 카드에서 구매/자세히 보기 버튼을 출력하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_button', function ($skin, $product) {
      $url = get_permalink($product->product_id());
      printf('<a class="button buy" href="%s">%s</a>', esc_url($url), esc_html__('Subscribe', 'textdomain'));
  }, 10, 2);
  ```

- **주의 사항**:
  - 새 창 이동이나 추적 파라미터가 필요하면 `add_query_arg()`로 URL을 빌드하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product`
