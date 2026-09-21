# AUTOMATION_OUTPUT_CONTRACT

## 목적

Scheduled Task가 학습자료를 생성할 때 임시 Python/Jupyter 파일 시스템에 의존하지 않고 GitHub 저장소를 영구 출력 저장소로 사용한다.

## 성공 조건

1. 해당 Day의 학습자료를 완성된 UTF-8 HTML 문자열로 생성한다.
2. 저장 경로는 `materials/YYYY-MM-DD_DayNN_주제.html`이다.
3. GitHub connector로 `NaturalHwang/cs-masters-study`의 기본 브랜치에 파일을 생성한다.
4. 같은 경로가 이미 있으면 먼저 현재 파일 SHA를 조회한 뒤 update_file로 개정한다.
5. 쓰기 성공 후 fetch_file로 파일을 다시 읽어 다음을 확인한다.
   - 올바른 Day 번호
   - 올바른 오늘의 주제
   - 15개 기본 섹션
   - 확인 질문/해설
6. 성공한 경우에만 생성 완료로 보고한다.

## 실패 조건

GitHub connector 접근, 파일 생성, 업데이트, 재조회 검증 중 어느 단계에서든 실패하면:
- 긴 학습 본문을 채팅에 출력하지 않는다.
- 실패한 Day/주제와 실패 단계, 확인 가능한 짧은 오류만 보고한다.
- 해당 Day를 생성/학습 완료로 처리하지 않는다.
- 다음 Day로 자동 건너뛰지 않는다.

## 파일 정책

- 자급형 HTML
- 외부 JS 금지
- UTF-8
- 모바일/인쇄 대응 CSS
- 목차
- `<details>` 기반 접이식 해설
- 실제 생성된 GitHub 파일만 링크한다.
