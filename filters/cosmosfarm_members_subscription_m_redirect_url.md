# cosmosfarm_members_subscription_m_redirect_url

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1271`
- **실행 시점**: 모바일 기기에서 구독 결제 시 결제 완료 후 리다이렉트될 URL을 설정할 때 실행됩니다. 모바일 결제 후 사용자를 보낼 목적지를 지정할 수 있습니다.
- **인자 정보**:
  - `$url (string)`: 모바일 결제 후 리다이렉트될 URL.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_subscription_m_redirect_url', 'my_custom_m_redirect_url', 10, 2);
  function my_custom_m_redirect_url($url, $product) {
    return home_url('/mobile-payment-redirect/');
  }
  ```

- **주의 사항**: 필터 함수는 반드시 유효한 URL 문자열을 반환해야 합니다. 모바일 앱이나 웹뷰에서 결제 완료 후 이동할 페이지의 URL입니다.
- **관련 훅**: `cosmosfarm_members_subscription_pay_success_url`
