# ERICA 통합 학사안내 편람

한양대학교 ERICA 학사 관련 규정과 제도별 안내를 제공하는 웹 기반 학사편람입니다. 공개 화면은 `index.html` 하나로 구성되며 GitHub Pages에서 배포합니다.

## 마이크로전공 목록 연동

마이크로전공 이수기준 교과목은 아래 두 서비스와 연결되어 있습니다.

- 목록형 원본: [Google Sheets](https://docs.google.com/spreadsheets/d/11VciL-MMSVYezUiEmWmtGbjjVC4YTlApBwUOdQQfxe4/edit?gid=0#gid=0)
- 카드형 웹앱: [Google Apps Script](https://script.google.com/macros/s/AKfycbwCh98GK66k6Kc7W8h_g1j-LhN5kuvmXB9q-0Rsov9NR_GpCSdTVnnEal5ar3enzERK8Q/exec)

학사편람의 `목록형 보기`는 Google Sheets를 새 탭에서 엽니다. `카드형 보기`는 Apps Script 웹앱을 학사편람 내부 iframe으로 표시합니다. Apps Script의 `getMicroMajorData()`가 시트의 최신 내용을 읽으므로, 시트의 값만 수정한 경우에는 `index.html` 수정이나 GitHub 재배포가 필요하지 않습니다.

## 카드형 보기 동작

- 사용자가 마이크로전공 메뉴에 들어오면 숨겨진 iframe을 미리 로딩합니다.
- 카드형 보기 버튼을 누르면 이미 준비된 웹앱을 표시하여 첫 클릭 대기시간을 줄입니다.
- Apps Script 상단의 중복 제목과 보기 전환 버튼 영역은 학사편람에서 보이지 않도록 처리하고 검색창부터 표시합니다.
- 데스크톱에서는 Apps Script의 900px 반응형 기준보다 넓은 920px 레이아웃을 확보한 후 화면 폭에 맞게 축소하여 카드를 2열로 표시합니다.
- 모바일에서는 가독성을 위해 1열로 표시합니다.

## Google Sheets 내용 수정

1. Google Sheets에서 기존 열 구조를 유지한 채 내용을 수정합니다.
2. 시트 저장이 완료되면 Apps Script 웹앱을 새로고침하여 변경 내용을 확인합니다.
3. 학사편람에서는 브라우저를 새로고침한 뒤 카드형 보기를 확인합니다.

Google Sheets의 열 이름이나 표 구조를 변경하면 `getMicroMajorData()`도 함께 수정해야 합니다.

## Apps Script 코드 수정 및 배포

Apps Script 코드 자체를 수정한 경우에는 저장만으로 공개 웹앱에 반영되지 않을 수 있습니다.

1. Apps Script에서 코드를 저장합니다.
2. `배포 → 배포 관리`를 엽니다.
3. 기존 웹앱 배포의 수정 버튼을 누릅니다.
4. `새 버전`을 선택하여 다시 배포합니다.
5. 실행 사용자는 소유자, 액세스 권한은 모든 사용자로 유지합니다.
6. 기존 `/exec` 주소가 유지되는지 확인합니다.

iframe 삽입을 위해 `doGet()`의 반환값에는 다음 설정이 필요합니다.

```javascript
.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
```

## GitHub 배포

`index.html`의 구조·스타일·Apps Script 주소를 변경한 경우에는 변경사항을 검증한 뒤 `main` 브랜치에 푸시합니다. GitHub Pages 반영에는 수 분이 걸릴 수 있습니다.
