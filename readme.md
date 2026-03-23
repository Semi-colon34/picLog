# Piclog Diary

**Piclog Diary**는 사용자별 일기를 작성·조회·수정·삭제할 수 있는 Spring Boot 기반 애플리케이션입니다.  
사용자는 계정을 생성하고 로그인 후 자신만의 일기를 관리할 수 있습니다.

---

## 주요 기능
- **회원 관리**
    - 회원가입, 로그인, 프로필 수정
- **일기 관리 (CRUD)**
    - 일기 작성, 조회, 수정, 삭제 기능 완성
- **입력값 검증**
    - Validation을 통해 올바른 데이터 처리 및 안정성 확보
- **향후 기능**
    - 다이어리 페이지에서 그림을 그려 첨부할 수 있는 기능 개발 예정
    - JWT 인증 및 권한 관리로 보안 강화 예정

---

## 기술 스택
- **Backend**: Java 21, Spring Boot 4.0.4
- **Build Tool**: Gradle (Groovy DSL)
- **Libraries**: Spring Web, Spring Data JPA, Lombok, Validation
- **Database**: MySQL

---

## 특징
- Spring Data JPA를 활용한 ORM 기반 CRUD 구현
- Validation을 활용한 안정적인 사용자 입력 처리
- 향후 그림 첨부 및 JWT 인증으로 기능 확장 계획