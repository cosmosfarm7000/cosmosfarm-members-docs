# cosmosfarm_members_exists_check_result

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:5212`
- **실행 시점**: AJAX를 통해 메타 정보 존재 여부를 확인한 후 결과를 필터링합니다. 사용자 등록 시 중복 확인 결과에 대한 추가 검증이나 메시지 커스터마이징을 수행할 수 있습니다.
- **인자 정보**:
  - `$result (array)`: 존재 여부 확인 결과 배열. 다음과 같은 키를 포함합니다: 'exists'(boolean - 값이 존재하면 true, 아니면 false), 'meta_key'(string - 확인한 메타 키), 'meta_value'(string - 확인한 메타 값), 'message'(string - 사용자에게 표시할 메시지). 이 배열을 수정하여 확인 결과를 변경하거나 메시지를 커스터마이징할 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_exists_check_result', 'my_custom_exists_check_result', 10, 1);
  function my_custom_exists_check_result($result) {
      // 이메일 중복 확인 시 추가 검증
      if ($result['meta_key'] === 'user_email' && !$result['exists']) {
          // 도메인 제한
          $allowed_domains = ['company.com', 'gmail.com'];
          $email_domain = substr(strrchr($result['meta_value'], "@"), 1);
          
          if (!in_array($email_domain, $allowed_domains)) {
              $result['exists'] = true;
              $result['message'] = '허용되지 않는 이메일 도메인입니다.';
          }
      }
      
      // 사용자명 중복 시 친화적 메시지
      if ($result['meta_key'] === 'user_login' && $result['exists']) {
          $result['message'] = '이미 사용 중인 아이디입니다. 다른 아이디를 선택해주세요.';
      }
      
      return $result;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 결과 배열을 반환해야 합니다. 존재 여부 확인 로직을 변경할 때는 보안과 사용자 경험을 고려해야 합니다.
- **관련 훅**: 없음
