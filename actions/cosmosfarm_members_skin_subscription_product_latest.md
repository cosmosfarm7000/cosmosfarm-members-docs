# cosmosfarm_members_skin_subscription_product_latest

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1100`
- **실행 시점**: 최신 구독 상품 목록을 출력하는 지점에서 호출됩니다. 최근 등록된 상품 몇 개만 별도 영역에 렌더링할 때 후킹됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
  - `$query (WP_Query)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_subscription_product_latest', function ($skin, $query) {
      echo '<div class="latest-intro">' . esc_html__('Latest subscription products', 'textdomain') . '</div>';
  }, 10, 2);
  ```

- **주의 사항**:
  - 최신 상품 개수, 정렬 기준은 스킨 구현이나 쿼리 인자에 좌우됩니다. UI 기대치에 맞게 CSS/JS를 최소한으로 추가하세요.
- **관련 훅**: `cosmosfarm_members_skin_subscription_product_list`
