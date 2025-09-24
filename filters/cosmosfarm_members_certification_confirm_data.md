# cosmosfarm_members_certification_confirm_data

- **분류**: Filter
- **정의 위치**: `class/Cosmosfarm_Members_Controller.class.php:3242`
- **실행 시점**: 본인인증 확인 후 인증 데이터를 필터링합니다. 아임포트 인증 API로부터 받은 사용자 인증 정보를 추가 처리하거나 수정할 수 있습니다.
- **인자 정보**:
  - `$certification (object)`: 아임포트 인증 API에서 반환된 인증 데이터 객체. 인증 성공/실패 상태, 사용자 정보(이름, 생년월일, 휴대폰번호 등), 인증 번호, 그리고 기타 인증 관련 메타데이터를 포함합니다. 이 객체는 아임포트 API의 응답 구조를 따르며, 인증 결과를 확인하고 추가 처리를 위해 사용됩니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_certification_confirm_data', 'my_custom_certification_data', 10, 1);
  function my_custom_certification_data($certification) {
      // 인증 성공 시 추가 로깅
      if (isset($certification->success) && $certification->success) {
          error_log('본인인증 성공: ' . $certification->name);
          
          // 추가 데이터 저장
          $certification->verified_at = current_time('mysql');
      }
      
      // 민감한 정보 마스킹
      if (isset($certification->phone)) {
          $certification->phone_masked = substr($certification->phone, 0, 3) . '****' . substr($certification->phone, -4);
      }
      
      return $certification;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 $certification 객체를 반환해야 합니다. 인증 데이터를 변경할 때는 보안과 개인정보 보호를 고려해야 합니다.
- **관련 훅**: 없음
