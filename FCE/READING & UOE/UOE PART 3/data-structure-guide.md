# Hướng dẫn cấu trúc JSON

## File 1: students.json
Lưu ở GitHub repo của bạn, ví dụ:
https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/students.json

```json
{
  "students": [
    {
      "id": "RS2024001",
      "name": "Nguyen Thi Lan",
      "class": "7A1"
    },
    {
      "id": "RS2024002",
      "name": "Tran Van Minh",
      "class": "7A2"
    }
  ]
}
```

---

## File 2: grade10.json
Câu hỏi Word Form cho Tuyển sinh 10
https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/grade10.json

```json
{
  "questions": [
    {
      "id": "g10_001",
      "sentence": "The ___ of this project depends on everyone's cooperation. (SUCCESS)",
      "rootWord": "SUCCESS",
      "answer": "SUCCESS",
      "explanation": "'Success' là danh từ, đứng sau mạo từ 'The' và trước giới từ 'of', nên dùng danh từ. SUCCESS (n) = sự thành công."
    },
    {
      "id": "g10_002",
      "sentence": "She gave a very ___ speech at the ceremony. (POWER)",
      "rootWord": "POWER",
      "answer": "POWERFUL",
      "explanation": "'Powerful' là tính từ, bổ nghĩa cho danh từ 'speech'. POWER (n) → POWERFUL (adj) = mạnh mẽ, hùng hồn."
    },
    {
      "id": "g10_003",
      "sentence": "The students showed great ___ during the exam. (PATIENT)",
      "rootWord": "PATIENT",
      "answer": "PATIENCE",
      "explanation": "'Patience' là danh từ trừu tượng, đứng sau tính từ 'great'. PATIENT (adj) → PATIENCE (n) = sự kiên nhẫn."
    }
  ]
}
```

---

## File 3: fce.json
Bài đọc Word Form cho FCE Use of English Part 3
https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/fce.json

```json
{
  "passages": [
    {
      "id": "fce_001",
      "title": "The Science of Sleep",
      "text": "Getting enough sleep is (0) ESSENTIAL for good health. Many people, however, are (1) ___ of the damage that sleep deprivation causes. Without proper rest, our (2) ___ to concentrate drops significantly. Research shows that even slight (3) ___ in sleep quality can affect our mood the following day. Scientists remain (4) ___ about the exact mechanisms involved, though most agree that the brain's (5) ___ process during sleep is crucial. A good night's sleep improves both physical and (6) ___ wellbeing. For many students, developing (7) ___ sleep habits is one of the most (8) ___ changes they can make to their academic performance.",
      "example": {
        "number": 0,
        "rootWord": "ESSENCE",
        "answer": "ESSENTIAL",
        "explanation": "Ví dụ mẫu: ESSENCE (n) → ESSENTIAL (adj) = thiết yếu."
      },
      "questions": [
        {
          "number": 1,
          "rootWord": "AWARE",
          "answer": "UNAWARE",
          "explanation": "Cần tính từ phủ định. AWARE (adj) → UNAWARE (adj) = không nhận thức được. Tiền tố UN- tạo nghĩa phủ định."
        },
        {
          "number": 2,
          "rootWord": "ABLE",
          "answer": "ABILITY",
          "explanation": "Sau sở hữu cách 'our' cần danh từ. ABLE (adj) → ABILITY (n) = khả năng."
        },
        {
          "number": 3,
          "rootWord": "REDUCE",
          "answer": "REDUCTIONS",
          "explanation": "Cần danh từ số nhiều sau 'slight'. REDUCE (v) → REDUCTION (n) → REDUCTIONS (n, plural) = sự sụt giảm."
        },
        {
          "number": 4,
          "rootWord": "CERTAIN",
          "answer": "UNCERTAIN",
          "explanation": "Cần tính từ phủ định sau 'remain'. CERTAIN (adj) → UNCERTAIN (adj) = không chắc chắn."
        },
        {
          "number": 5,
          "rootWord": "RESTORE",
          "answer": "RESTORATION",
          "explanation": "Sau sở hữu cách 'brain's' cần danh từ. RESTORE (v) → RESTORATION (n) = quá trình phục hồi."
        },
        {
          "number": 6,
          "rootWord": "MENTAL",
          "answer": "MENTAL",
          "explanation": "Cần tính từ song song với 'physical'. MENTAL (adj) = thuộc về tinh thần. Từ không đổi dạng."
        },
        {
          "number": 7,
          "rootWord": "HEALTH",
          "answer": "HEALTHY",
          "explanation": "Cần tính từ trước danh từ 'sleep habits'. HEALTH (n) → HEALTHY (adj) = lành mạnh."
        },
        {
          "number": 8,
          "rootWord": "BENEFIT",
          "answer": "BENEFICIAL",
          "explanation": "Cần tính từ sau 'most'. BENEFIT (n/v) → BENEFICIAL (adj) = có lợi, mang lại lợi ích."
        }
      ]
    }
  ]
}
```

---

## Ghi chú quan trọng khi tạo data

### Với Grade 10:
- Viết câu có chỗ trống rõ ràng bằng ___
- Luôn in hoa từ gốc trong ngoặc: (SUCCESS)
- Đáp án luôn IN HOA
- Giải thích bằng tiếng Việt, ngắn gọn, nêu rõ lý do chọn dạng từ đó

### Với FCE:
- Câu (0) là ví dụ mẫu đã cho sẵn, không tính điểm
- Đánh số từ 1-8
- Đáp án luôn IN HOA
- Giải thích nêu rõ: cần loại từ gì → vì sao → cách biến đổi
