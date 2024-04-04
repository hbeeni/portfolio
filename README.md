# 박혜빈 포트폴리오
> 매일 조금씩 더 성장하고자 하는 개발자 :seedling:

</br>

## :pushpin: Intro
안녕하세요. 백엔드 개발자로서 더 성장하고 싶은 **박혜빈**입니다.

저는 Java와 Spring Boot를 활용하여 1개의 팀 프로젝트, 2개의 개인 프로젝트를 개발하였습니다.

프로젝트에서 데이터베이스 설계 및 쿼리 작성, REST API 설계 및 구현, Redis를 활용한 캐싱 등을 구현하였습니다.  
더불어 Google Cloud를 사용하여 프로젝트를 배포하는 과정도 익혔습니다.

팀 프로젝트에서는 팀원들과 커뮤니케이션하는 경험 또한 할 수 있었습니다.

이제까지의 경험을 바탕으로 더 배우고 성장하여, 백엔드 개발자로서의 역량을 지속적으로 향상시키겠습니다!

</br>

## :pushpin: Contact
- 이메일: hyebeen.dev@gmail.com
- 깃헙: https://github.com/hbeeni

</br>

## :pushpin: Projects

### 1. CATEGO
>YouTube 구독 채널 폴더링 서비스 (개인 프로젝트)  
>개발 기간: 2024.1.16 ~ 2024.3.23  
>서비스 링크: https://catego.kro.kr  
>  
>기술 스택:  
>Java 17 / Spring Boot 3.2.1 / Gradle 8.5  
>Spring Data JPA / MySQL / H2  
>Spring Security / OAuth2 Client / Spring Web / Spring Data Redis  
>Thymeleaf / YouTube Data API V3  
>  
>[프로젝트 상세 설명](https://github.com/hbeeni/catego) 참고

---

### 2. 온라인 쇼핑몰 API
>쇼핑몰 웹 사이트를 위한 REST API (개인 프로젝트)  
>개발 기간: 2023.11.1 ~ 2024.1.14  
>서비스 링크: http://onlinestoreapi.kro.kr  
>  
>기술 스택:  
>Java 17 / Spring Boot 2.7.17 / Gradle 8.3  
>Spring Data JPA / QueryDSL / MySQL / H2  
>Spring Security / Spring Web / Spring REST Docs / restdocs-api-apec  
>  
>[프로젝트 상세 설명](https://github.com/hbeeni/online-store) 참고

---

### 3. i:HealMe
>소아과 진료 접수 및 후기 작성 서비스 (팀 프로젝트)  
>개발 기간: 2023.4.24 ~ 2023.5.14  
>  
>기술 스택:  
>Java 11 / Spring Boot 2.7.11 / Gradle 7.6.1  
>Spring Data JPA / Oracle DB / Spring Web / Thymeleaf

- 담당: 커뮤니티 후기 게시글 관련 기능 구현
- 핵심 기능
  - JPA를 활용한 게시글 등록, 수정, 삭제, 조회
  - 게시글 조회 시 병원 이름, 제목, 작성자로 검색 가능
  - 게시글 조회수 보기, 신고하기
- 트러블 슈팅

  <details>
  <summary><code>PersistentObjectException: detached entity passed to persist</code></summary>
  <div markdown="1">
  
  - 문제: Post 저장 시 이미 저장된 User를 또 저장하기 때문에 문제가 발생함
  - 해결: `cascade = CascadeType.ALL` 설정을 삭제함
  
  </div>
  </details>

  <details>
  <summary><code>firstResult/maxResults specified with collection fetch; applying in memory!</code></summary>
  <div markdown="1">
  
  - 문제: `Post` 조회 시 `Comment` fetch join과 pagination을 같이 사용했음 -> 이 때 모든 데이터를 전부 가져와 메모리에서 걸러내서 문제가 발생함
  - 해결: Batch size를 설정함
    ```java
    public class Post {

        //...
    
        @OneToMany(mappedBy = "post", orphanRemoval = true, fetch = FetchType.LAZY)
        @BatchSize(size = 10) //추가
        private List<Comment> comments = new ArrayList<>();
    }
    ```
  - 해결: `distinct`를 추가함
  
  </div>
  </details>
