# cosmosfarm_members_redeem_point_coupon_success

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:5494`
- **실행 시점**: 포인트 쿠폰(MyCred) 교환이 정상적으로 완료된 직후 호출됩니다.
- **인자 정보**:
  - `$coupon_id (int)`: 교환된 쿠폰 게시글 ID입니다.
  - `$mycred_coupon (array)`: MyCred 쿠폰 정보 배열입니다.
  - `$user_id (int)`: 쿠폰을 사용한 사용자 ID입니다.
- **예제 코드**:
  ```php
  // 쿠폰 차감 후 사용자에게 감사 알림을 보낸다.
  add_action('cosmosfarm_members_redeem_point_coupon_success', function ($coupon_id, $mycred_coupon, $user_id) {
      $user = get_userdata($user_id);
      if (!$user) {
          return;
      }

      wp_mail(
          $user->user_email,
          __('Coupon redeemed successfully', 'textdomain'),
          sprintf(__('You have redeemed coupon #%d. Balance: %s', 'textdomain'), $coupon_id, mycred_get_users_balance($user_id))
      );
  }, 10, 3);
  ```
- **주의 사항**:
  - `$mycred_coupon` 구조는 MyCred 버전에 따라 달라질 수 있으므로, 키 존재 여부를 확인 후 사용하세요.
  - 포인트 잔액을 재계산하거나 추가 메타를 저장할 때는 MyCred API를 사용해 일관성을 유지하세요.
- **관련 훅**: `cosmosfarm_members_send_notification`, `cosmosfarm_members_mail_send`
