# cosmosfarm_members_mail_send

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Mail.class.php:24`
- **실행 시점**: 플러그인의 메일 발송 래퍼(`Cosmosfarm_Members_Mail::send()`)가 제목·본문·CTA 정보를 구성하고 `wp_mail()`을 호출하기 직전에 실행됩니다.
- **인자 정보**:
  - `$args (array)`: 메일 발송에 사용될 인자 배열. `to`, `subject`, `message`, `headers`, `call_to_actions` 등이 포함됩니다.
  - `$mail (Cosmosfarm_Members_Mail)`: 메일 클래스 인스턴스. 템플릿 렌더링 시 참조되는 `call_to_actions` 속성을 조정할 수 있습니다.
- **예제 코드**:
  ```php
  // 메일 발송 전에 CTA 버튼을 동적으로 추가한다.
  add_action('cosmosfarm_members_mail_send', function ($args, $mail) {
      $mail->call_to_actions[] = array(
          'name' => __('Manage Subscription', 'textdomain'),
          'url'  => home_url('/membership/manage')
      );

      add_filter('wp_mail', function ($mail_args) {
          $mail_args['headers'][] = 'Bcc: audit@example.com';
          remove_filter('wp_mail', __FUNCTION__);
          return $mail_args;
      });
  }, 10, 2);
  ```
- **주의 사항**:
  - `$args`는 값으로 전달되므로 직접 수정해도 `wp_mail()`에 반영되지 않습니다. 헤더나 수신자를 바꾸려면 `wp_mail` 필터를 추가하거나 `$mail` 인스턴스 설정을 조정하세요.
  - HTML 템플릿을 교체하려면 테마의 `cosmosfarm-members/email/template.php` 파일을 오버라이드하는 것이 추천됩니다.
  - 발송 실패 처리를 위해서는 `wp_mail_failed` 훅을 함께 활용하세요.
- **관련 훅**: `cosmosfarm_members_send_message`, `cosmosfarm_members_send_notification`
