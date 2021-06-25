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

### 개발 예시

```typescript
app.get('/books/:id', function (req, res) {
    const {id} = req.params;

    const result = {
        title: "Romance of the Three Kingdoms",
        author: {
            firstName: "Luo",
            lastName: "Guanzhong"
        }
    };

    res.send(result);
})
```

### 결과 예시

#### 요청

> GET /books/1

#### 응답

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

- REST 는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일이다.
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

### 개발 예시

```typescript
const resolvers = {
    Query: {
        book: (parent, args) => {
            const result = {
                title: "Romance of the Three Kingdoms",
            };
            return result;
        },
        author: (parent, args) => ({firstName: "Luo", lastName: "Guanzhong"})
    }
}
```

### 결과 예시

#### 요청

```
query {
  book(id: "1") {
    title
    author {
      firstName
      lastName
    }
  }
}
```

#### 응답

```json
{
  "title": "Romance of the Three Kingdoms",
  "author": {
    "firstName": "Luo",
    "lastName": "Guanzhong"
  }
}
```

#### 요청 2

```
query {
  book(id: "1") {
    title
    author {
      firstName
    }
  }
}
```

#### 응답 2

```json
{
  "title": "Romance of the Three Kingdoms",
  "author": {
    "firstName": "Luo"
  }
}
```

### 장점

- HTTP 요청의 횟수를 줄일 수 있다.
  - RESTful 은 각 Resource 종류 별로 요청을 해야하고, 따라서 요청 횟수가 필요한 Resource 의 종류에 비례한다.
  - 반면 GraphQL 은 원하는 정보를 하나의 Query 에 모두 담아 요청하는 것이 가능하다.
- HTTP 응답의 Size 를 줄일 수 있다.
  - RESTful 은 응답의 형태가 정해져있고, 따라서 필요한 정보만 부분적으로 요청하는 것이 힘들다.
  - 반면 GraphQL 은 원하는 대로 정보를 요청하는 것이 가능하다.

### 단점

- File 전송 등 Text 만으로 하기 힘든 내용들을 처리하기 복잡하다.
- 고정된 요청과 응답만 필요할 경우에는 Query 로 인해 요청의 크기가 RESTful API 의 경우보다 더 커진다.
- 재귀적인 Query 가 불가능하다. (결과에 따라 응답의 깊이가 얼마든지 깊어질 수 있는 API 를 만들 수 없다)

![img.png](./img.png)