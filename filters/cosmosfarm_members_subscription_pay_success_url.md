# cosmosfarm_members_subscription_pay_success_url

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1200`
- **실행 시점**: 구독 결제 완료 후 사용자를 리다이렉트할 URL을 설정할 때 실행됩니다. 결제 성공 페이지나 완료 페이지로의 이동을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$pay_success_url (string)`: 결제 성공 후 리다이렉트될 URL. 기본적으로는 결제 완료 페이지 설정이 있으면 해당 페이지 URL로, 없으면 referrer URL로 설정됩니다. 상품 ID가 쿼리 파라미터로 추가됩니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체. 상품 정보를 기반으로 리다이렉트 URL을 결정할 때 사용할 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_pay_success_url', 'my_custom_pay_success_url', 10, 2);
  function my_custom_pay_success_url($pay_success_url, $product) {
      // 상품별로 다른 성공 페이지로 리다이렉트
      if ($product->ID() === 123) {
          return home_url('/premium-success/');
      }
      return home_url('/payment-success/');
  }
  ```



- **주의 사항**: 필터 함수는 반드시 유효한 URL 문자열을 반환해야 합니다. 반환된 URL은 결제 성공 후 사용자를 리다이렉트하는 데 사용됩니다.
- **관련 훅**: `cosmosfarm_members_subscription_m_redirect_url` (모바일 결제 후 리다이렉트 URL)

