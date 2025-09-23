# cosmosfarm_members_skin_subscription_product_type

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:964`
- **실행 시점**: 구독 상품 스킨이 상품 유형(반복/일회성 등)을 표시하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_type', function ($skin, $product) {
      echo '<span class="type">' . esc_html($product->subscription_type_format()) . '</span>';
  }, 10, 2);
  ```

- **주의 사항**:
  - 유형 텍스트는 스킨의 라벨과 중복될 수 있으니, 출력 결과를 확인 후 보조 정보로만 사용하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product`
