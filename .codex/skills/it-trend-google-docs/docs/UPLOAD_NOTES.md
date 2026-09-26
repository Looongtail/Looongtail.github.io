# Google Docs 업로드 검수 메모

이 문서는 IT Trend 발행본을 Google Docs로 옮길 때 확인된 변환 특성과 재발 방지 절차다. 문서 작성 단계가 아니라, 배포가 끝난 Markdown 원고를 변경 없이 문서화하는 단계에서만 사용한다.

## 이번 작업에서 확인된 문제

### 원고 축약 위험

- Google Docs용으로 옮길 때도 게시 Markdown이 기준 원고다. 제목, 도입, 모든 소제목, 삼성SDS/SCP 등 기업별 맥락, 비교표, 그림 캡션, 결론, `## 출처`를 빠짐없이 대조한다.
- 문서로 옮기는 과정에서 표나 본문을 재요약하지 않는다. 이미지와 표가 누락되지 않았는지는 읽기 API로 별도 확인한다.

### 한글 글꼴과 로컬 렌더링

- Arial만 지정한 DOCX를 로컬 LibreOffice 계열 렌더러로 확인하면 한글 글리프가 공백 또는 점처럼 보일 수 있다. 이는 원문 손실이 아니라 로컬 렌더러의 한글 대체 글꼴 부재일 수 있다.
- DOCX에는 Arial과 함께 한글 지원 East Asian fallback font를 지정한다. 그래도 로컬 렌더 출력이 의심스러우면, 원문과 native Google Doc의 readback text를 대조해 한글 보존을 확인한다.
- 로컬 렌더에 문제가 있다는 사실만으로 이미지를 빼거나 원고를 다시 쓰지 않는다. native Google Doc 변환 후 텍스트·표·캡션을 확인한 결과를 우선한다.

### 페이지 형식

- 문서 생성 라이브러리의 기본 페이지 크기는 A4가 아닐 수 있다. 페이지 크기와 상하좌우 72pt 여백을 명시적으로 설정한다.

### 이미지 포함 방식

- 블로그 Markdown의 `/images/...` 경로는 Google Docs에서 표시되지 않는다. 대응하는 `codes/public/...` 실제 파일을 찾아 DOCX/HTML에 **인라인으로 삽입**해야 한다.
- SVG가 DOCX 삽입에 호환되지 않으면 임시 PNG로 변환해 삽입할 수 있다. 원본 SVG는 바꾸지 않고, 임시 변환 파일은 검수 후 정리한다.
- 이미지 수는 원고의 Markdown 이미지 수와 비교한다. 그림마다 캡션이 바로 뒤에 있고, `get_document`의 inline object 정보에서 이미지 객체가 모두 확인돼야 한다. 캡션만으로 이미지 삽입을 판단하지 않는다.

### 날짜와 native Google Docs 변환

- Drive에 단순 파일 업로드가 아니라 `native_google_docs` 변환을 사용한다. MIME type과 대상 parent folder ID를 반드시 확인한다.
- 날짜 메타데이터는 Google Docs date chip으로 넣는다. `DATE_FORMAT_YEAR_MONTH_DAY`는 이 환경의 API에서 유효하지 않아 실패했다. 지원되는 date format enum을 사용하고, 실패한 batch update가 문서를 바꾸지 않았는지 readback으로 확인한다.
- 날짜 칩은 text readback에서 일반 문자열처럼 표시되지 않을 수 있다. batch update 성공 응답과 문서 구조 readback을 함께 확인한다.

## 최소 검수 목록

- [ ] Drive 파일 제목이 `[yyyy-mm-dd] <기사 제목>` 형식이며, 날짜가 post `pubDate`와 일치함
- [ ] 제목과 `IT Trend  |  [작성일]` 메타 행
- [ ] 도입·모든 `##` 소제목·결론·`## 출처`
- [ ] 모든 표의 행·열과 핵심 셀 텍스트
- [ ] 원고의 모든 이미지가 인라인 삽입됐고 캡션이 존재함
- [ ] native Google Docs MIME type 및 Drive 폴더 ID
- [ ] 제목·본문·표·출처의 Google Docs readback 결과
- [ ] 생성 중인 임시 DOCX, PDF, 변환 이미지의 정리
