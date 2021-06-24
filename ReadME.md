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

### 예시
> 글 관련 API = /posts\
> 글 작성 = POST /posts\
> 글 수정 = PATCH /posts/[postid]\
> 글 삭제 = DELETE /posts/[postid]\
> 댓글 관련 API = /posts/[postid]/comments\
> 댓글 작성 = POST /posts/[postid]/comments\
> 댓글 수정 = PATCH /posts/[postid]/comments/[commentid]\
> 댓글 삭제 = DELETE /posts/[postid]/comments/[commentid]

### 장점
- REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
- HTTP 프로토콜을 사용하므로 REST API 사용을 위한 인프라를 구축할 필요가 없다.
- HTTP 표준프로토콜을 따르는 모든 플랫폼에서 호환된다. (범용성)
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.