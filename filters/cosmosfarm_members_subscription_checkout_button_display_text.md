# cosmosfarm_members_subscription_checkout_button_display_text

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 구독 결제 페이지에서 결제 버튼의 텍스트를 설정할 때 실행됩니다. 결제 버튼에 표시될 텍스트를 상황에 따라 변경할 수 있습니다.
- **인자 정보**:
  - `$text (string)`: 버튼에 표시될 텍스트.
  - `$product (Cosmosfarm_Members_Subscription_Product)`: 구독 상품 객체.
  - `$is_subscription_first_free (bool)`: 첫 달 무료 구독인지 여부.
  - `$coupon (object)`: 적용된 쿠폰 객체 (있는 경우).
- **예제 코드**:

```php
add_filter('cosmosfarm_members_subscription_checkout_button_display_text', 'my_custom_checkout_button_text', 10, 4);
function my_custom_checkout_button_text($text, $product, $is_subscription_first_free, $coupon) {
    if ($is_subscription_first_free) {
        return '첫 달 무료로 시작하기';
    }
    return '지금 결제하기';
}
```

- **주의 사항**: 필터 함수는 반드시 문자열을 반환해야 합니다. 반환된 텍스트는 결제 버튼에 표시됩니다.
- **관련 훅**: `cosmosfarm_members_subscription_pay_success_url`, `cosmosfarm_members_subscription_m_redirect_url`
