# cosmosfarm_members_skin_subscription_checkout_field

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 구독 결제 페이지에서 각 입력 필드를 렌더링할 때 실행됩니다. 결제 폼의 필드 속성(플레이스홀더, 클래스 등)을 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$field (object)`: 결제 필드 객체. name, type, placeholder, value 등의 속성을 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_skin_subscription_checkout_field', 'my_custom_skin_checkout_field');
function my_custom_skin_checkout_field($field) {
    // 필드 속성 변경
    if ($field->name === 'billing_phone') {
        $field->placeholder = '휴대폰 번호를 입력하세요';
    }
    return $field;
}
```

- **주의 사항**: 필터 함수는 반드시 필드 객체를 반환해야 합니다. 필드 객체의 속성을 수정하여 결제 폼의 동작을 변경할 수 있습니다.
- **관련 훅**: `cosmosfarm_members_template_subscription_checkout_fields`
