# cosmosfarm_members_skin_subscription_product_price

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:928`
- **실행 시점**: 구독 상품 스킨이 상품 가격을 출력하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_price', function ($skin, $product) {
      echo '<div class="price">' . esc_html(cosmosfarm_members_currency_format($product->price())) . '</div>';
  }, 10, 2);
  
  ```

- **주의 사항**:
  - 통화 포맷은 플러그인에서 제공하는 헬퍼 함수를 사용하면 일관성을 유지할 수 있습니다.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product`
