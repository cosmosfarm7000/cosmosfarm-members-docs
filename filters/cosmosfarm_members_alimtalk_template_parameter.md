# cosmosfarm_members_alimtalk_template_parameter

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Sms_Nhn.class.php:23`
- **실행 시점**: 알림톡 메시지를 전송하기 전에 템플릿 파라미터를 필터링합니다. SMS 발송 과정에서 템플릿 변수들을 동적으로 수정하거나 추가할 수 있습니다.
- **인자 정보**:
  - `$template_parameter (array)`: 알림톡 템플릿에 사용할 변수들의 연관 배열. 키는 템플릿에서 정의된 변수명(예: "이름", "주소", "주문번호"), 값은 실제 치환될 문자열 값입니다. 빈 배열일 수 있으며, 필터에서 새로운 변수를 추가하거나 기존 값을 수정할 수 있습니다.
  - `$template_code (string)`: 사용될 알림톡 템플릿의 고유 코드. 템플릿을 식별하는 문자열로, 특정 템플릿에 맞는 파라미터를 설정할 때 사용할 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_alimtalk_template_parameter', 'my_custom_alimtalk_template_param', 10, 2);
  function my_custom_alimtalk_template_param($template_parameter, $template_code) {
      // 특정 템플릿에만 적용
      if ($template_code === 'ORDER_CONFIRM') {
          $template_parameter['주문상태'] = '확인됨';
      }
      
      // 공통 변수 추가
      $template_parameter['사이트명'] = get_bloginfo('name');
      
      return $template_parameter;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 $template_parameter 배열을 반환해야 합니다. 이 필터를 통해 알림톡 템플릿의 동적 콘텐츠를 제어할 수 있습니다.
- **관련 훅**: `cosmosfarm_members_messages_subnotify_alimtalk_args`
