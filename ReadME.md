RestfulAPI 와 GraphicQL 비교
=

### 참고

[Hwasurr's Devlog](https://hwasurr.io/api/rest-graphql-differences/) \
[APOLLO BLOG](https://www.apollographql.com/blog/graphql/basics/graphql-vs-rest/) \
[holaxprogramming.com](https://www.holaxprogramming.com/2018/01/20/graphql-vs-restful-api/) \
[devSoo](https://velog.io/@djaxornwkd12/REST-API-vs-GraphQL-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)


Restful API 란
-

> REST 는 REpresentational State Transfer 의 줄임말 입니다.\
> 모든 Resource (자료, User, …) 들을 하나의 Endpoint 에 연결해놓고, 각 Endpoint 는 그 Resource 와 관련된 내용만 관리하게 하자는 방법론 입니다.\
> HTTP URI 를 통해 자원을 명시하고 , HTTP Method(post,get,put,delete)를 통해 해당자원에 대한 CRUD Operation 을 적용하는 것을 의미합니다.

### URI 예시

> 글 관련 API = /posts\
> 글 작성 = POST /posts\
> 글 수정 = PATCH /posts/{postid}\
> 글 삭제 = DELETE /posts/{postid}\
>
> 댓글 관련 API = /posts/{postid}/comments\
> 댓글 작성 = POST /posts/{postid}/comments\
> 댓글 수정 = PATCH /posts/{postid}/comments/{commentid}\
> 댓글 삭제 = DELETE /posts/{postid}/comments/{commentid}

### 결과 예시

> GET /books/1

```json
{
  "title": "Romance of the Three Kingdoms",
  "author": {
    "firstName": "Luo",
    "lastName": "Guanzhong"
  }
}
```

### 장점

- REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
- HTTP 프로토콜을 사용하므로 REST API 사용을 위한 인프라를 구축할 필요가 없다.
- HTTP 표준프로토콜을 따르는 모든 플랫폼에서 호환된다. (범용성)
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

### 단점

- 표준이 존재하지 않는다.
- 사용할수 있는 메소드가 4가지 밖에 없다.
- 구형의 브라우저가 아직 지원하지 못하는 부분이 존재한다.

GraphicQL 이란
-

> GraphQL 은 Graph Query Language 의 줄임말 입니다. \
> RESTful API 로는 다양한 기종에서 필요한 정보들을 일일히 구현하는 것이 힘들었으며\
> 이 때문에 정보를 사용하는 측에서 원하는 대로 정보를 가져올 수 있고, 보다 편하게 정보를 수정할 수 있도록 하는 표준화된 Query language 를 만들게 되었습니다.

### 결과 예시

> Book과 Author라는 타입을 정의해야 합니다.
> 이후 Book과 Author에 접근할 수 있도록, 우리는 Query라는 타입이 필요합니다

```
type Book
{
    id: ID
    title: String
    author: Author
}
type Author
{
    id: ID
    firstName: String
    lastName: String
    books: [Book]
}

type Query {
    book(id: ID!): Book
    author(id: ID!): Author
}
```

> /graphql?query={ book(id: "1") { title, author { firstName } } }

```json
{
  "title": "Black Hole Blues",
  "author": {
    "firstName": "Janna"
  }
}
```