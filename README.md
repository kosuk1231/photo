# 40주년 사진전 심사표

서울특별시사회복지사협회 창립 40주년 기념 사진전 심사 시스템

## 배포 방법

### 1. GitHub에 올리기
```bash
git init
git add .
git commit -m "40주년 사진전 심사표"
git remote add origin https://github.com/your-username/photo-judging.git
git push -u origin main
```

### 2. Vercel 배포
1. [vercel.com](https://vercel.com) 접속 → GitHub 연동
2. Import Project → 이 저장소 선택
3. Deploy 클릭 → 완료!

### 3. Google Apps Script 설정
스프레드시트(ID: `1K3cr1Bg5boRLaG5aEcYmvpWppPkmoDtWBf69ky769SQ`)에서:

1. **확장 프로그램 → Apps Script** 열기
2. 아래 코드 붙여넣기:

```javascript
function doPost(e) {
  try {
    var data = JSON.parse(e.postData.contents);
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    if (sheet.getLastRow() === 0) {
      var h = ["제출시각", "심사자"];
      for (var i = 1; i <= 40; i++) h.push("사진" + i);
      h.push("총점", "평균", "서명");
      sheet.appendRow(h);
    }
    sheet.appendRow(data.row);
    return ContentService
      .createTextOutput(JSON.stringify({ result: "success" }))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (err) {
    return ContentService
      .createTextOutput(JSON.stringify({ error: err.message }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

3. **배포 → 새 배포 → 웹 앱 → 모든 사용자** → 배포

## 스프레드시트 구조

| 제출시각 | 심사자 | 사진1 | 사진2 | ... | 사진40 | 총점 | 평균 | 서명 |
|---------|--------|-------|-------|-----|--------|------|------|------|
| 2026.3.19 | 홍길동 | 8 | 7 | ... | 9 | 320 | 8.0 | 서명완료 |
