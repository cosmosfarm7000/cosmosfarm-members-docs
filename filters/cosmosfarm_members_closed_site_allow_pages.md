# cosmosfarm_members_closed_site_allow_pages

- **분류**: Filter
- **정의 위치**: `..\class\Cosmosfarm_Members_Security.class.php:412`
- **실행 시점**: 폐쇄된 사이트에서 페이지 접근을 확인할 때 허용 페이지 목록을 필터링합니다. 사이트 폐쇄 모드에서 특정 페이지에 대한 접근을 추가로 허용할 수 있습니다.
- **인자 정보**:
  - `$allow_pages (array)`: 폐쇄된 사이트에서 접근 가능한 페이지들의 ID 배열. 기본적으로 로그인 페이지($option->login_page_id), 회원가입 페이지($option->register_page_id), 계정 페이지($option->account_page_id)의 ID가 포함되며, 추가로 접근을 허용할 페이지 ID를 배열에 추가할 수 있습니다.
- **예제 코드**:

  ```php
  add_filter('cosmosfarm_members_closed_site_allow_pages', 'my_custom_closed_site_allow_pages', 10, 1);
  function my_custom_closed_site_allow_pages($allow_pages) {
      // 유지보수 안내 페이지 추가 (페이지 ID로 추가)
      $maintenance_page_id = 123; // 유지보수 페이지의 ID
      $allow_pages[] = $maintenance_page_id;
      
      // 약관 페이지 추가
      $terms_page_id = 456; // 약관 페이지의 ID
      $allow_pages[] = $terms_page_id;
      
      return $allow_pages;
  }
  ```

- **주의 사항**: 필터 함수는 반드시 수정된 페이지 ID 배열을 반환해야 합니다. 페이지 ID는 WordPress 포스트 ID여야 합니다.
- **관련 훅**: `cosmosfarm_members_page_restriction`
