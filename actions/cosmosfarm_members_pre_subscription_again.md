# cosmosfarm_members_pre_subscription_again

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:4465`
- **실행 시점**: 구독 재결제를 시도하기 직전에 호출됩니다. 재시도가 시작되기 전에 두 번(사용자 존재 여부 확인 시, 실제 결제 실행 전) 트리거되며, 결제 한도나 사용자 상태를 재검증할 수 있습니다.
- **인자 정보**:
  - `$old_order (Cosmosfarm_Members_Subscription_Order)`: 재결제 대상이 되는 기존 주문 객체입니다.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 재결제 대상 상품 객체입니다.
- **예제 코드**:
  ```php
  // 재결제 전에 사용자 계정이 정지 상태인지 확인한다.
  add_action('cosmosfarm_members_pre_subscription_again', function ($old_order, $product) {
      $user = $old_order->user();
      if ($user && get_user_meta($user->ID, '_membership_suspended', true)) {
          $old_order->set_subscription_next('cancel');
          $old_order->set_error_message(__('Membership is suspended. Billing skipped.', 'textdomain'));
          wp_send_json(array('result' => 'error', 'message' => __('Membership suspended', 'textdomain')));
      }
  }, 10, 2);
  ```
- **주의 사항**:
  - 훅 내에서 `wp_send_json()`을 호출하면 재결제 루틴이 중단되므로, 이후 처리(예: 알림)도 직접 수행해야 합니다.
  - 같은 요청 안에서 두 번 호출될 수 있으므로, 멱등성을 고려해 조건 검사나 로그 저장을 구현하세요.
  - 재결제 가격 조정은 `cosmosfarm_members_subscription_again_price` 필터를 사용해 처리하는 것이 적합합니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_failure`, `cosmosfarm_members_subscription_again_success`
