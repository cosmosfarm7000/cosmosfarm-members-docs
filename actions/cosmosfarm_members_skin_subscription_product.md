# cosmosfarm_members_skin_subscription_product

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:853`
- **실행 시점**: 구독 상품 스킨이 단일 상품 블록을 렌더링할 때, 기본 정보(제목/가격/유형 등) 출력 직전에 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`: 현재 스킨 객체. `the_title()`, `the_price()`, `the_type()` 같은 헬퍼를 가질 수 있으며, 내부적으로 현재 상품 컨텍스트를 참조합니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 렌더링 대상 상품 객체.
- **예제 코드**:

  ```php
  // 상품 카드 상단에 배지 추가
  add_action('cosmosfarm_members_skin_subscription_product', function ($skin, $product) {
      if ($product->is_first_free()) {
          echo '<span class="badge badge-free">' . esc_html__('First month free', 'textdomain') . '</span>';
      }
  }, 10, 2);
  
  ```

- **주의 사항**:
  - 출력 위치는 스킨 구현에 의존합니다. 과도한 마크업은 레이아웃을 깨뜨릴 수 있으므로, 최소한의 래퍼만 추가하세요.
- **관련 훅**: `cosmosfarm_members_skin_after_subscription_product`, `cosmosfarm_members_skin_subscription_product_title`, `cosmosfarm_members_skin_subscription_product_price`, `cosmosfarm_members_skin_subscription_product_type`
