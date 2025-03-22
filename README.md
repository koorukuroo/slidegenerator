# Slide generator


# 📘 JSON 기반 슬라이드 작성 가이드

이 문서는 `build_slides_from_json()` 함수로 자동 슬라이드를 생성하기 위한 JSON 포맷을 안내합니다. 각 슬라이드는 Python dict로 정의되며, 다음 필드를 포함할 수 있습니다:

---

## 🔑 공통 필드 (모든 타입 공통)
| 필드명           | 설명 |
|------------------|------|
| `type`           | 슬라이드 타입 (`title`, `chapter`, `section`, `topic`, `content`, `code`, `table`) |
| `slide_number`   | 슬라이드 번호 (슬라이드 순서를 나타냄, 확장성을 위해 유지) |
| `title`          | 슬라이드 타이틀 |
| `speaker_note`   | 발표자 노트 (발표자가 참고할 설명) |
| `logo_path`      | 개별 슬라이드에만 적용할 로고 경로 또는 텍스트 |
| `logo_size`      | 로고 크기 (인치 단위) |

---

## 🎬 1. `title` 슬라이드
강의 제목과 발표자 정보를 담은 표지 슬라이드

| 필드명             | 설명 |
|--------------------|------|
| `subtitle`         | 부제목 |
| `lecture_number`   | 강의 번호 (예: `Lecture 4`) |
| `presenter_name`   | 발표자 이름 |
| `presenter_email`  | 발표자 이메일 |

**예시**:
```json
{
  "type": "title",
  "slide_number": 1,
  "title": "Web Scraping with Python",
  "subtitle": "BeautifulSoup & Selenium",
  "lecture_number": "Lecture 4",
  "presenter_name": "Kyunghoon Kim",
  "presenter_email": "kyunghoon@core.today"
}
```

---

## 📚 2. `chapter` 슬라이드
강의의 주요 챕터 구분용 슬라이드 (어두운 배경, 강조 효과)

| 필드명       | 설명 |
|--------------|------|
| `subtitle`   | 챕터 설명 or 소제목 |

**예시**:
```json
{
  "type": "chapter",
  "slide_number": 2,
  "title": "Chapter 1: Basics",
  "subtitle": "Fundamentals of Web Scraping"
}
```

---

## 🧩 3. `section` 슬라이드
챕터 내부의 중간 파트 구분 (연한 파랑 배경, 세련된 구간 전환)

| 필드명       | 설명 |
|--------------|------|
| `section_subtitle` | 선택적으로 부제목 표시 |

**예시**:
```json
{
  "type": "section",
  "slide_number": 5,
  "title": "Part 2: Parsing HTML",
  "section_subtitle": "BeautifulSoup in Action"
}
```

---

## 🪧 4. `topic` 슬라이드
하위 주제 전환을 나타내는 간결한 전환 슬라이드 (화이트 배경, 중앙 정렬 텍스트)

**예시**:
```json
{
  "type": "topic",
  "slide_number": 6,
  "title": "Advanced CSS Selectors"
}
```

---

## 📝 5. `content` 슬라이드
일반적인 본문 슬라이드 (여러 줄 텍스트, 마크다운 일부 지원)

| 필드명    | 설명 |
|-----------|------|
| `content` | 본문 내용 (`\n`으로 줄 바꿈, `**bold**`, `*italic*`, `` `code` `` 지원) |

**예시**:
```json
{
  "type": "content",
  "slide_number": 3,
  "title": "What is Web Scraping?",
  "content": "✅ Definition: Automated process\n- HTML\n- HTTP\n- Parser"
}
```

---

## 🧾 6. `table` 슬라이드
비교표나 데이터 테이블을 나타내는 슬라이드

| 필드명   | 설명 |
|----------|------|
| `headers` | 열 제목 리스트 |
| `rows`    | 행 데이터 2차원 리스트 |

**예시**:
```json
{
  "type": "table",
  "slide_number": 5,
  "title": "Scraping vs API",
  "headers": ["Feature", "Web Scraping", "API"],
  "rows": [
    ["Availability", "Any public webpage", "Only if provided"],
    ["Ease of Use", "Can be tricky", "Usually simpler"]
  ]
}
```

---

## 💻 7. `code` 슬라이드
Python 코드 하이라이팅이 포함된 슬라이드

| 필드명    | 설명 |
|-----------|------|
| `content` | 코드 문자열 (Pygments로 Python 문법 하이라이팅됨) |

**예시**:
```json
{
  "type": "code",
  "slide_number": 8,
  "title": "Basic Scraping Example",
  "content": "import requests\nresponse = requests.get('https://example.com')"
}
```

---

## 🗒 발표자 노트 (`speaker_note`)
모든 슬라이드에 선택적으로 `speaker_note`를 넣을 수 있습니다. 이는 발표자가 발표할 때 참고하는 텍스트입니다.

---

## 🖼 로고 삽입
- 슬라이드 전체에 공통 로고를 적용하려면 `build_slides_from_json(..., default_logo_path, default_logo_size)` 인자를 사용하세요.
- 개별 슬라이드에는 `logo_path`와 `logo_size`를 지정할 수 있습니다.

---

## ✅ 요약
| 슬라이드 타입 | 용도 |
|---------------|------|
| `title`       | 강의 표지 |
| `chapter`     | 대단원 구분 |
| `section`     | 중간 구간 구분 |
| `topic`       | 소주제 전환 |
| `content`     | 일반 본문 설명 |
| `table`       | 데이터/비교표 |
| `code`        | 코드 설명 |

---
