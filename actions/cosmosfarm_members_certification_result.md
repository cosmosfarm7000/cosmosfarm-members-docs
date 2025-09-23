# cosmosfarm_members_certification_result

- **분류**: Action
- **정의 위치**: `class/api/Cosmosfarm_Members_API_Iamport.class.php`
- **실행 시점**: 본인 인증 결과가 처리될 때 호출됩니다. 인증 성공/실패 후 후속 작업에 사용됩니다.
- **인자 정보**:
  - `$result (object)`: 인증 결과 객체. `$result->success`로 성공 여부를 확인할 수 있습니다.
  - `$response (object)`: 인증 응답 데이터. 이름, 전화번호 등 포함.
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_certification_result', 'my_custom_certification_result', 10, 2);
  function my_custom_certification_result($result, $response) {
      // 본인 인증 결과에 따른 추가 로직
      if ($result->success) {
          error_log('본인 인증 성공: ' . $response->name);
      } else {
          error_log('본인 인증 실패: ' . $response->error_msg);
      }
  }
  ```

- **주의 사항**: 민감한 개인정보 처리 시 보안에 유의하세요.
- **관련 훅**: 없음
