# cosmosfarm_members_skin_after_subscription_product

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:858`
- **실행 시점**: 구독 상품 스킨에서 단일 상품 블록 기본 출력이 끝난 직후 호출됩니다. 상품 카드 하단에 부가 정보를 붙일 때 적합합니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`: 현재 스킨 객체.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 렌더링된 상품 객체.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_after_subscription_product', function ($skin, $product) {
      echo '<p class="meta">' . esc_html(sprintf(__('Purchase count: %d', 'textdomain'), (int) get_post_meta($product->product_id(), '_purchase_count', true))) . '</p>';
  }, 10, 2);
  
  ```

- **주의 사항**:
  - 스타일 충돌을 피하기 위해 스킨이 제공하는 클래스 네이밍을 재사용하는 것이 좋습니다.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product`
