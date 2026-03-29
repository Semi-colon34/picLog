# PicLog Diary - API 설계 문서

## 1. 개요
- **서비스 이름:** PicLog Diary
- **설계 목적:** 사용자, 일기, 그림 데이터를 관리하기 위한 RESTful API 정의
- **주요 기능:**
    - 사용자 로그인/회원가입
    - 일기 작성/조회/수정/삭제
    - Canvas 그림 저장/조회/삭제 (덮어쓰기 방식)

---

## 2. 리소스 & 엔드포인트

### 2.1 User
| Method | Endpoint | Description | Request Body | Response |
|--------|---------|------------|-------------|---------|
| POST | /users/register | 회원가입 | `{ mail, pwd }` | `{ id, mail }` |
| POST | /users/login | 로그인 | `{ mail, pwd }` | `{ token, userId }` |
| GET | /users/:id | 사용자 정보 조회 | - | `{ id, mail }` |

---

### 2.2 Diary
| Method | Endpoint | Description | Request Body | Response |
|--------|---------|------------|-------------|---------|
| POST | /diaries | 새 일기 작성 | `{ userId, diaryDate, title, content }` | `{ diaryKey, ... }` |
| GET | /diaries/:diaryKey | 특정 일기 조회 | - | `{ diaryKey, title, content, diaryDate }` |
| GET | /users/:userId/diaries | 사용자 일기 목록 조회 | - | `[ { diaryKey, title, diaryDate } ]` |
| PUT | /diaries/:diaryKey | 일기 수정 | `{ title?, content? }` | `{ diaryKey, ... }` |
| DELETE | /diaries/:diaryKey | 일기 삭제 | - | `{ success: true }` |

---

### 2.3 Picture
| Method | Endpoint | Description | Request Body | Response |
|--------|---------|------------|-------------|---------|
| POST | /pictures | Diary 그림 업로드 | `{ diaryKey, path }` | `{ diaryKey, path }` |
| GET | /pictures/:diaryKey | Diary 그림 조회 | - | `{ diaryKey, path }` |
| DELETE | /pictures/:diaryKey | 그림 삭제 | - | `{ success: true }` |

> 💡 덮어쓰기 방식 적용: 그림을 수정할 때 기존 path에 덮어쓰기 때문에 PUT(수정) API는 불필요

---

## 3. 설계 팁
- DiaryKey 기반 조회 → Diary와 Picture 모두 연결 가능
- JWT 토큰 인증 → User 인증 후 Diary/Picture 접근
- Validation → 날짜 중복, 그림 1:1 제약 체크