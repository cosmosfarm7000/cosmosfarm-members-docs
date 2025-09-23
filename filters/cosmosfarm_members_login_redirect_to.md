# cosmosfarm_members_login_redirect_to

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php`
- **실행 시점**: 사용자가 로그인 폼을 통해 로그인한 후, 리다이렉트될 URL을 결정할 때 실행됩니다. 로그인 성공 후 사용자를 보낼 목적지를 커스터마이징할 수 있습니다.
- **인자 정보**:
  - `$redirect_to (string)`: 로그인 후 리다이렉트될 URL. 기본적으로 로그인 페이지의 referrer URL이나 홈페이지 URL입니다.
- **예제 코드**:

```php
add_filter('cosmosfarm_members_login_redirect_to', 'my_custom_login_redirect');
function my_custom_login_redirect($redirect_to) {
    return home_url('/dashboard/');
}
```

- **주의 사항**: 필터 함수는 반드시 유효한 URL 문자열을 반환해야 합니다. 반환된 URL은 로그인 성공 후 사용자를 리다이렉트하는 데 사용됩니다.
- **관련 훅**: `cosmosfarm_members_social_login_redirect_to`
