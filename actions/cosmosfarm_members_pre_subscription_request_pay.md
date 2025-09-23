# cosmosfarm_members_pre_subscription_request_pay

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3447`
- **실행 시점**: 사용자가 구독 결제를 요청하기 전에(`Cosmosfarm_Members_Controller::pre_subscription_request_pay()`가 사용자/상품 검증을 마친 뒤) 호출됩니다. 프런트 결제 폼에서 AJAX로 호출되며, 로그인 상태 확인이나 사전 검증을 추가할 수 있습니다.
- **인자 정보**:
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 결제 대상 구독 상품 객체입니다. `ID()`, `price()`, `subscription_type()` 등을 확인할 수 있습니다.
  - `$meta_input (array|null)`: 결제 폼에서 전달된 메타 데이터 배열입니다. 일부 경로에서는 `null`일 수 있으므로 사용 전 null 여부를 확인하세요.
  - `$custom_data (array|null)`: 사용자 정의 데이터(예: 추가 필드, 쿠폰, 주소 정보). 마찬가지로 경로에 따라 `null`일 수 있습니다.
- **예제 코드**:

  ```php
  // 결제 전 쿠폰 유효성을 검증한다.
  add_action('cosmosfarm_members_pre_subscription_request_pay', function ($product, $meta_input, $custom_data) {
      if (!$product->ID()) {
          wp_send_json(array('result' => 'error', 'message' => __('Product not found.', 'textdomain')));
      }
  
      $coupon_code = isset($custom_data['coupon_code']) ? sanitize_text_field($custom_data['coupon_code']) : '';
      if ($coupon_code && !my_custom_coupon_is_valid($coupon_code, $product->ID())) {
          wp_send_json(array('result' => 'error', 'message' => __('Coupon is invalid or expired.', 'textdomain')));
      }
  }, 10, 3);
  ```
- **주의 사항**:
  - 이 훅 내에서 `wp_send_json()`으로 응답을 종료할 수 있으며, 반환 형식은 `{ result: 'success'|'error', message: '...' }` 형태를 유지해야 프런트 스크립트와 호환됩니다.
  - `$meta_input`과 `$custom_data`는 상황에 따라 `null`일 수 있으므로, 배열 접근 전 `is_array()` 검사를 수행하세요.
  - 결제 전 민감 정보(카드번호 등)는 이미 정리되어 있으나, 커스텀 필드에 개인정보가 있을 수 있으니 별도 처리 규정을 준수하세요.
- **관련 훅**: `cosmosfarm_members_subscription_request_pay`, `cosmosfarm_members_subscription_request_pay_result`
