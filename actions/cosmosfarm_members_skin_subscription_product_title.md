# cosmosfarm_members_skin_subscription_product_title

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:892`
- **실행 시점**: 구독 상품 스킨이 상품 제목을 출력하는 지점에서 호출됩니다. 기본 제목 출력 대신 커스텀 마크업을 추가하거나, 보조 정보를 함께 표기할 수 있습니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_title', function ($skin, $product) {
      printf('<h3 class="product-title">%s <small class="muted">%s</small></h3>',
          esc_html($product->name()),
          esc_html($product->subscription_type_format())
      );
  }, 10, 2);

  ```

- **주의 사항**:
  - 제목에 링크를 포함해야 한다면 `get_permalink($product->product_id())`를 사용하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product`
