# Hướng dẫn tạo Google Apps Script để lưu điểm

## Bước 1: Tạo Google Sheet

1. Vào https://sheets.google.com → tạo sheet mới
2. Đặt tên: **Word Form Quiz Results**
3. Tạo 2 tab (sheet):
   - Tab 1: **Sessions** (lưu mỗi lần làm bài)
   - Tab 2: **WrongAnswers** (lưu câu sai để ôn lại)

### Tab Sessions - hàng đầu tiên (header):
```
Timestamp | StudentID | StudentName | Class | Mode | StartTime | EndTime | Duration | TotalQuestions | Correct | Wrong | Percentage
```

### Tab WrongAnswers - hàng đầu tiên (header):
```
Timestamp | StudentID | QuestionID | QuestionType | RootWord | StudentAnswer | CorrectAnswer | AttemptCount
```

---

## Bước 2: Tạo Apps Script

1. Trong Google Sheet → menu **Extensions** → **Apps Script**
2. Xóa hết code cũ, dán code sau vào:

```javascript
const SHEET_ID = 'YOUR_GOOGLE_SHEET_ID_HERE'; // Thay bằng ID sheet của bạn

function doPost(e) {
  try {
    const data = JSON.parse(e.postData.contents);
    const action = data.action;
    
    if (action === 'saveSession') {
      return saveSession(data);
    } else if (action === 'saveWrongAnswers') {
      return saveWrongAnswers(data);
    } else if (action === 'getWrongAnswers') {
      return getWrongAnswers(data);
    }
    
    return ContentService
      .createTextOutput(JSON.stringify({ status: 'error', message: 'Unknown action' }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch(err) {
    return ContentService
      .createTextOutput(JSON.stringify({ status: 'error', message: err.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  // Cho phép test từ browser
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'ok', message: 'Word Form Quiz API is running' }))
    .setMimeType(ContentService.MimeType.JSON);
}

function saveSession(data) {
  const ss = SpreadsheetApp.openById(SHEET_ID);
  const sheet = ss.getSheetByName('Sessions');
  
  sheet.appendRow([
    new Date().toISOString(),
    data.studentId,
    data.studentName,
    data.class,
    data.mode,
    data.startTime,
    data.endTime,
    data.duration,
    data.totalQuestions,
    data.correct,
    data.wrong,
    data.percentage
  ]);
  
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'success', message: 'Session saved' }))
    .setMimeType(ContentService.MimeType.JSON);
}

function saveWrongAnswers(data) {
  const ss = SpreadsheetApp.openById(SHEET_ID);
  const sheet = ss.getSheetByName('WrongAnswers');
  
  data.wrongAnswers.forEach(function(q) {
    sheet.appendRow([
      new Date().toISOString(),
      data.studentId,
      q.questionId,
      q.questionType,
      q.rootWord,
      q.studentAnswer,
      q.correctAnswer,
      q.attemptCount
    ]);
  });
  
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'success', message: 'Wrong answers saved' }))
    .setMimeType(ContentService.MimeType.JSON);
}

function getWrongAnswers(data) {
  const ss = SpreadsheetApp.openById(SHEET_ID);
  const sheet = ss.getSheetByName('WrongAnswers');
  const rows = sheet.getDataRange().getValues();
  
  const studentId = data.studentId;
  const wrongIds = [];
  
  // Bỏ hàng header (rows[0])
  for (let i = 1; i < rows.length; i++) {
    if (rows[i][1] === studentId) {
      wrongIds.push(rows[i][2]); // QuestionID
    }
  }
  
  // Lọc trùng
  const uniqueIds = [...new Set(wrongIds)];
  
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'success', wrongQuestionIds: uniqueIds }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

---

## Bước 3: Lấy Sheet ID

- Mở Google Sheet của bạn
- Nhìn vào URL: `https://docs.google.com/spreadsheets/d/`**`1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgVE2upms`**`/edit`
- Phần in đậm đó chính là Sheet ID
- Dán vào dòng `const SHEET_ID = '...'` trong code

---

## Bước 4: Deploy Apps Script

1. Nhấn nút **Deploy** (góc trên phải) → **New deployment**
2. Chọn loại: **Web app**
3. Cấu hình:
   - Description: Word Form Quiz API
   - Execute as: **Me**
   - Who has access: **Anyone** (quan trọng - phải chọn Anyone)
4. Nhấn **Deploy**
5. **Copy URL** hiện ra - đây là URL bạn sẽ dán vào app HTML

---

## Bước 5: Lần đầu chạy - cấp quyền

1. Sau khi Deploy, Google sẽ yêu cầu cấp quyền
2. Nhấn **Authorize access**
3. Chọn tài khoản Google của bạn
4. Nhấn **Advanced** → **Go to Word Form Quiz API (unsafe)** → **Allow**
5. Xong - URL của bạn đã hoạt động

---

## URL mẫu sau khi deploy:
```
https://script.google.com/macros/s/AKfycbxXXXXXXXXXXXXXX/exec
```

Dán URL này vào app HTML ở phần cấu hình.
