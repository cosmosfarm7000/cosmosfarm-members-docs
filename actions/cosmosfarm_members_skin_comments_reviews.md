# cosmosfarm_members_skin_comments_reviews

- **분류**: Action
- **정의 위치**: `class/Cosmosfarm_Members_Skin.class.php:1465`
- **실행 시점**: 스킨에서 댓글/리뷰 영역을 출력하는 지점에서 호출됩니다.
- **인자 정보**:
  - `$skin (Cosmosfarm_Members_Skin)`
- **예제 코드**:

  ```php
  add_action('cosmosfarm_members_skin_comments_reviews', function ($skin) {
      echo '<div class="my-reviews">' . esc_html__('Custom reviews block', 'textdomain') . '</div>';
  }, 10, 1);
  ```

- **주의 사항**:
  - 코멘트 템플릿과 중첩되지 않도록 출력 위치를 최소화하세요.
- **관련 훅**: `comments_template`
