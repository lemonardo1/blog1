# Cypher 기초

Cypher는 Neo4j 그래프 데이터베이스에서 사용되는 쿼리 언어로, 그래프 데이터를 직관적으로 조회하고 조작할 수 있게 설계되었습니다. 아래에서 Cypher의 기본 개념과 문법을 설명해 드리겠습니다.

## 기본 구조

Cypher는 패턴 매칭을 기반으로 하며, 노드와 관계를 시각적으로 표현합니다:

- 노드(Node): 원형 괄호 `()` 로 표현
- 관계(Relationship): 대시와 화살표 `-[]->` 로 표현
- 속성(Property): 중괄호 `{}` 안에 키-값 쌍으로 표현

## 주요 명령어

### 1. MATCH

그래프에서 특정 패턴을 찾는 데 사용됩니다.

```cypher
// 모든 Person 노드 찾기
MATCH (p:Person)
RETURN p

// 특정 속성을 가진 노드 찾기
MATCH (p:Person {name: 'John'})
RETURN p
```

### 2. CREATE

새로운 노드나 관계를 생성합니다.

```cypher
// 새 노드 생성
CREATE (p:Person {name: 'John', age: 30})

// 노드 간 관계 생성
MATCH (a:Person {name: 'John'}), (b:Person {name: 'Mary'})
CREATE (a)-[:FRIENDS_WITH]->(b)
```

### 3. RETURN

쿼리 결과를 반환합니다.

```cypher
MATCH (p:Person)
RETURN p.name, p.age
```

### 4. WHERE

조건을 지정합니다.

```cypher
MATCH (p:Person)
WHERE p.age > 25
RETURN p
```

### 5. DELETE

노드나 관계를 삭제합니다.

```cypher
// 관계 삭제
MATCH (a)-[r:FRIENDS_WITH]->(b)
DELETE r

// 노드 삭제 (연결된 모든 관계도 함께 삭제해야 함)
MATCH (p:Person {name: 'John'})
DETACH DELETE p
```

### 6. SET

속성을 설정하거나 업데이트합니다.

```cypher
MATCH (p:Person {name: 'John'})
SET p.age = 31, p.updated = true
```

## 복잡한 쿼리 예제

### 관계 탐색

```cypher
// John의 친구들 찾기
MATCH (p:Person {name: 'John'})-[:FRIENDS_WITH]->(friend)
RETURN friend.name

// John의 친구의 친구 찾기 (2단계 관계)
MATCH (p:Person {name: 'John'})-[:FRIENDS_WITH]->()-[:FRIENDS_WITH]->(fof)
RETURN DISTINCT fof.name
```

### 집계 함수

```cypher
// 각 사람의 친구 수 계산
MATCH (p:Person)-[:FRIENDS_WITH]->(friend)
RETURN p.name, COUNT(friend) AS friendCount
ORDER BY friendCount DESC
```

### 경로 찾기

```cypher
// 두 사람 간의 최단 경로 찾기
MATCH p = shortestPath((a:Person {name: 'John'})-[*]-(b:Person {name: 'Mary'}))
RETURN p
```

## 실행 계획 확인

쿼리 최적화를 위해 실행 계획을 확인할 수 있습니다.

```cypher
EXPLAIN MATCH (p:Person)-[:FRIENDS_WITH]->(friend)
RETURN p.name, COUNT(friend)
```

Cypher는 SQL과 유사한 구조를 가지고 있지만, 그래프 데이터 모델에 맞게 설계되어 복잡한 관계 패턴을 쉽게 표현할 수 있다는 점이 큰 장점입니다. 이러한 특징으로 인해 연결된 데이터를 다루는 작업에서 매우 효과적입니다.