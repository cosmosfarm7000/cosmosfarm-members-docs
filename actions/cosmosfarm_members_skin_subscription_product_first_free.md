# cosmosfarm_members_skin_subscription_product_first_free

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1000`
- **실행 시점**: 구독 상품 스킨이 "첫 달 무료" 등의 프로모션 정보를 표시하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$product (Cosmosfarm_Members_Subscription_Product)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_first_free', function ($skin, $product) {
      if ($product->is_first_free()) {
          echo '<span class="promo">' . esc_html__('Free for the first month', 'textdomain') . '</span>';
      }
  }, 10, 2);
  ```

- **주의 사항**:
  - 무료 기간이 일(day) 단위로 지정되는 경우가 있으므로, 상세 레이블을 출력하려면 `subscription_first_free()` 값을 해석해 표시하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product`
