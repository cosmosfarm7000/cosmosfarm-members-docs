# cosmosfarm_members_register_form_policy_fields

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members.class.php`
- **실행 시점**: 회원가입 폼에서 표시될 정책 동의 필드들을 설정할 때 실행됩니다. 이용약관, 개인정보처리방침 등의 정책 필드를 추가하거나 제거할 수 있습니다.
- **인자 정보**:
  - `$fields (array)`: 정책 필드들의 배열. 기본적으로 'policy_service', 'policy_privacy' 등의 필드 키를 포함합니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_register_form_policy_fields', 'my_custom_policy_fields');
function my_custom_policy_fields($fields) {
    // 'policy_privacy' 필드를 제거
    if (($key = array_search('policy_privacy', $fields)) !== false) {
        unset($fields[$key]);
    }
    // 새로운 정책 필드 추가
    $fields[] = 'my_custom_policy';
    return $fields;
}
```

- **주의 사항**: 필터 함수는 반드시 필드 배열을 반환해야 합니다. 반환된 필드들은 회원가입 폼에 정책 동의 체크박스로 표시됩니다.
- **관련 훅**: `cosmosfarm_members_template_social_buttons`
