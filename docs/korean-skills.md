# Codex 한국어 글쓰기 스킬

[DaleSeo/korean-skills](https://github.com/DaleSeo/korean-skills)의 스킬 3개를 이 프로젝트의 `.agents/skills/`에 설치했다. `references/`와 `examples/`도 함께 포함한다. 전역 설치나 Claude 플러그인 설치는 수행하지 않았다.

## 사용 예시

```text
$humanizer 이 자기소개서의 사실과 기술 수준은 유지하고 번역투만 자연스럽게 다듬어줘.
$grammar-checker 이 문서의 맞춤법과 띄어쓰기만 검사해줘.
$style-guide 이 포트폴리오의 용어와 말투를 통일해줘.
```

일반 문장으로 “한국어 글쓰기 스킬로 이 문서를 검토해줘”라고 요청해도 된다. 실제 스킬 목록에 나타나는지 확인한 뒤 사용하며, 새 스킬이 보이지 않으면 새 대화를 시작하거나 Codex를 재시작한다.

프로젝트 적용 규칙의 원본은 [.claude/korean-writing.md](../.claude/korean-writing.md)다. 지원서의 사실 검증과 기존 취업 절차는 그대로 적용한다. 코드·영어 문서·일반 대화에 세 스킬을 무조건 실행하는 설정은 아니다.

설치한 정확한 커밋과 라이선스는 [설치 기록](../.agents/skills/KOREAN_SKILLS_SOURCE.md)을 확인한다. 파일 설치와 문서 연결을 검증했으며, 별도 Codex 세션에서의 자동 스킬 선택은 다음 사용 시 확인한다.
