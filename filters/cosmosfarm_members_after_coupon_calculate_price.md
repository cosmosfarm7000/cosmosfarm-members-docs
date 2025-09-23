# cosmosfarm_members_after_coupon_calculate_price

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 쿠폰 적용 후 최종 계산된 가격을 필터링합니다. (교정된 정식 훅명)
- **인자 정보**:
  - `$first_price (float|int)`: 쿠폰 적용 후 계산된 최종 가격 (결제할 금액). 이 값은 상품의 원래 가격에 옵션 가격을 더한 후 쿠폰 할인을 적용한 결과값입니다. 음수나 0이 될 수 있으며, 결제 처리 시 검증됩니다.
  - `$product_id (int)`: 정기결제 상품의 ID. 이 ID를 통해 상품 정보를 조회하여 추가적인 가격 조정 로직을 적용할 수 있습니다.
- **예제 코드**:

  ```php
  // 상품별 추가 할인 적용
  add_filter('cosmosfarm_members_after_coupon_calculate_price', function($price, $product_id){
      // 특정 상품에 대해 추가 10% 할인
      if ($product_id == 123) {
          $price = $price * 0.9; // 10% 추가 할인
      }
      return $price;
  }, 10, 2);
  
  // 최소 결제 금액 설정
  add_filter('cosmosfarm_members_after_coupon_calculate_price', function($price, $product_id){
      // 결제 금액이 1000원 미만이면 1000원으로 설정
      return max($price, 1000);
  }, 10, 2);
  
  // 회원 등급별 추가 혜택
  add_filter('cosmosfarm_members_after_coupon_calculate_price', function($price, $product_id){
      $user = wp_get_current_user();
      if (in_array('premium', $user->roles)) {
          $price -= 1000; // 프리미엄 회원 추가 할인
      }
      return $price;
  }, 10, 2);
  ```



- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다. 반환값이 음수이거나 0인 경우 결제 처리에서 검증될 수 있습니다. 가격 계산 로직을 변경할 때는 상품의 결제 흐름을 충분히 이해하고 테스트해야 합니다.
- **관련 훅**: `cosmosfarm_members_subscription_again_price` (정기결제 재결제 시 가격 필터링)

