# cosmosfarm_members_after_coupon_calculate_price

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Controller.class.php`class/Cosmosfarm_Members_Controller.class.php``
- **실행 시점**: 쿠폰 적용 후 최종 계산된 가격을 필터링합니다. (교정된 정식 훅명)
- **인자 정보**:
  - `$first_price (float|int)`: 쿠폰 적용 후 계산된 최종 가격 (결제할 금액)
  - `$product_id (int)`: 상품 ID
- **예제 코드**:

  ```php
// 신규 권장 훅 사용
add_filter('cosmosfarm_members_after_coupon_calculate_price', function($price, $product_id){
    if ($product_id == 123) {
        $price -= 500; // 정액 추가 할인
    }
    return $price;
}, 10, 2);
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
