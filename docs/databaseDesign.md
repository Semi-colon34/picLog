# PicLog Diary - 데이터베이스 설계 문서

## 1. 개요
- **서비스 이름:** PicLog Diary
- **설계 목적:** 사용자, 일기, 그림 데이터를 효율적으로 관리하고, 안정적인 키 구조 기반으로 설계
- **주요 기능:**
    - 사용자 로그인
    - 일기 작성/조회/수정/삭제
    - 일기별 그림 저장 및 Canvas 툴 연동

---

## 2. 논리적 설계 (테이블 구조)

### 2.1 User 테이블
| 컬럼 | 데이터 타입 | 제약조건 | 설명 |
|------|------------|---------|------|
| id | INT | PK, AUTO_INCREMENT | 사용자 고유 ID |
| mail | VARCHAR(100) | NOT NULL, UNIQUE | 이메일 (로그인용) |
| pwd | VARCHAR(255) | NOT NULL | 비밀번호 |

---

### 2.2 Diary 테이블
| 컬럼 | 데이터 타입 | 제약조건 | 설명 |
|------|------------|---------|------|
| diaryKey | VARCHAR(20) | PK, NOT NULL | `userId + '_' + diaryDate` 문자열 키 |
| userId | INT | FK(User.id), NOT NULL | 작성자 ID |
| diaryDate | DATE | NOT NULL | 일기 작성일 |
| title | VARCHAR(200) | NOT NULL | 일기 제목 |
| content | TEXT | NOT NULL | 일기 내용 |

---

### 2.3 Picture 테이블
| 컬럼 | 데이터 타입 | 제약조건 | 설명 |
|------|------------|---------|------|
| diaryKey | VARCHAR(20) | PK, FK(Diary.diaryKey), NOT NULL | 연결된 Diary 키 |
| path | VARCHAR(255) | NOT NULL | 그림 파일 경로 |

---

## 3. 관계 및 제약 조건
- User ↔ Diary: 1:N (User.id ↔ Diary.userId)
- Diary ↔ Picture: 1:1 (Diary.diaryKey ↔ Picture.diaryKey)
- Diary 삭제 시 Picture도 Cascade 삭제

---

