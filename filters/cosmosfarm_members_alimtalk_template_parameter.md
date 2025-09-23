# cosmosfarm_members_alimtalk_template_parameter

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Sms_Nhn.class.php`class/Cosmosfarm_Members_Sms_Nhn.class.php`, `class/Cosmosfarm_Members_Sms_Solapi.php``
- **실행 시점**: 알림톡 템플릿 파라미터를 필터링합니다.
- **인자 정보**:
  - `$template_parameter (array)`: 알림톡 템플릿에 사용할 변수들의 배열. 키는 변수명(예: "이름", "주소"), 값은 실제 치환될 값입니다. 기본적으로 템플릿에서 정의된 변수들을 포함합니다.
  - `$template_code (string)`: 사용될 알림톡 템플릿의 코드. 템플릿을 식별하는 고유한 문자열입니다.
- **예제 코드**:

  ```php
add_filter('cosmosfarm_members_alimtalk_template_parameter', 'my_custom_alimtalk_template_param', 10, 2);
function my_custom_alimtalk_template_param($template_parameter, $template_code) {
    $template_parameter['custom_key'] = 'custom_value';
    return $template_parameter;
}
  ```

- **주의 사항**: 필터 함수는 반드시 값을 반환해야 합니다.
- **관련 훅**: 없음
