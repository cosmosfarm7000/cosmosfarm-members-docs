# cosmosfarm_members_skin_subscription_product_list

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1067`
- **실행 시점**: 구독 상품 목록을 쿼리해 루프를 돌며 카드 목록을 출력하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$query (WP_Query)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_list', function ($skin, $query) {
      echo '<div class="product-list-intro">' . esc_html__('Our Subscriptions', 'textdomain') . '</div>';
  }, 10, 2);
  ```

- **주의 사항**:
  - `$query`는 글로벌 루프가 아닐 수 있으니, 커스텀 루프를 사용하는 코드에서는 `wp_reset_postdata()` 등이 이미 호출되는지 확인하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product_latest`
