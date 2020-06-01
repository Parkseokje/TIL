# GraphQL Intro

GraphQL와 REST API와의 차이점에 대해 간략히 소개합니다.

## GraphQL은

- SQL(Structured Query Language) 쿼리와 동일한 목적의 쿼리 언어이다.
- GraphQL 문장은 주로 클라이언트에서 작성한다.
- 특정 데이터베이스 또는 플랫폼에 종속적이지 않다.

## REST API와의 차이점

- GraphQL은 앤드포인트가 하나다.
- REST API의 경우 앤드포인트마다 SQL 쿼리가 달라지는 반면, GraphQL의 타입에 따라 SQL 쿼리가 달라진다.
- 단일 요청으로 여러 리소스를 동시에 가져올 수 있다.

  요청 예시: hero의 이름과 친구들의 이름을 가져와.

  ```graphql
  {
    hero {
      name
      friends {
        name
      }
    }
  }
  ```

  응답 예시

  ```json
  {
    "hero": {
      "name": "seokje",
      "friends": [{ "name": "sam" }, { "name": "christ" }]
    }
  }
  ```

## GraphQL이 해결해주는 문제들

- Over-Fetching: 클라이언트가 필요하지 않은 정보도 함께 내려주는 문제
- Under-Fetching: 어떤 하나의 정보를 완성하기 위해 여러 요청을 보내야 하는 경우

## GraphQL Schema

- 받거나 줄 데이터를 정의하는 GraphQL의 구성 요소
- Query(질의): 데이터를 받고자할 때 사용
- Mutation(변형): 데이터를 변경하고자할 때 사용
- Resolver: 데이터를 가져오는 구체적인 과정을 기술

## Query

데이터를 받고자할 때 사용. 데이터를 유저 리스트라고 가정했을 때,
아래 문법은 모든 사용자의 name을 반환한다.

```graphql
query {
  name
}
```

아래 문법은 id가 1인 사용자를 반환한다. (단, `user`라는 resolver를 정의했을 경우)

```graphql
query {
  user(id: 1) {
    name
  }
}
```

편리한 점은 여러 resolver(REST API의 경우 endpoint와 동일한 개념)를 한번에 호출할 수 있다는 점이다. 만약 영화목록과 추천 영화 목록을 한꺼번에 조회하고 싶다면 아래와 같이 작성할 수 있다.

```graphql
{
  movies(limit: 1) {
    id
    title
    rating
    summary
    small_cover_image
  }
  suggestion(id: 7893) {
    title
  }
}
```

실행 결과 `movies`와 `suggestion` 하나의 JSON으로 반환된다.

```json
{
  "data": {
    "movies": [
      {
        "id": 17937,
        "title": "The Haunting of Molly Bannister",
        "rating": 0,
      }
    ],
    "suggestion": [
      {
        "title": "Berserk: The Golden Age Arc III - The Advent"
      }
    ]
  }
}
```

## Mutation

데이터를 변경하고자할 때 사용. 아래 문법은 사용자를 추가하는 구문 (단, `addUser`라는 resolver를 정의했을 경우)

```graphql
mutation {
  addUser(name: "Seokje", age: 40, gender: "male) {
    name
  }
}
```

## Resolver

데이터를 가져오는 구체적인 과정을 기술. 아래는 query에서 보았던 `user` resolver의 구문이다.

```javascript
const resolvers = {
  Query: {
    user: (_, { id }) => getUser(id), // getUser에서 id를 받아 데이터를 가져온다.
  },
};
```

아래는 mutation에서 보았던 `addUser` resolver의 구문이다. Mutation이란 속성으로 정의되어 있는 것을 알 수 있다.

```javascript
const resolvers = {
  Mutation: {
    addUser: (_, { name, age, gender }) => addUser(name, age, gender),
  },
};
```

## Reference sites/docs

- [GraphQL 공식 사이트](https://graphql.org/)
- [GraphQL 한국 공식 사이트](https://graphql-kr.github.io//)
- [GraphQL 개념잡기](https://tech.kakao.com/2019/08/01/graphql-basic/)
- [The Fullstack Tutorial for GraphQL](https://www.howtographql.com/)
