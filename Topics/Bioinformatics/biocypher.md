[[cypher]]
# BioCypher: 생물학 지식 그래프 구축을 위한 프레임워크

BioCypher는 생물학적 데이터를 지식 그래프로 변환하는 프레임워크로, 복잡한 생물학적 데이터를 구조화된 방식으로 표현하여 기계 판독 가능하고 생물학 연구자들에게 접근 가능하게 만듭니다.


### 온톨로지 유연성

BioCypher는 온톨로지 선택에 있어 유연한 접근법을 취합니다:

- 기본적으로 Biolink 모델을 사용하지만, 다른 온톨로지도 사용 가능합니다.
- 여러 온톨로지를 혼합(하이브리드화)하여 특정 도메인에 맞게 확장할 수 있습니다.
- OWL(.owl), RDF(.rdf), TTL(.ttl) 형식의 온톨로지 파일을 지원합니다.

### 모델 확장 방법

BioCypher는 기본 온톨로지 모델을 여러 방식으로 확장할 수 있습니다:

1. **명시적 상속**: `is_a` 필드를 사용하여 새로운 클래스를 기존 온톨로지의 하위 클래스로 정의
    
    ```yaml
    protein isoform:
      is_a: protein
      represented_as: node
    ```
    
2. **암시적 상속**: 여러 입력 라벨과 선호 식별자를 통해 자동으로 하위 클래스 생성
    
    ```yaml
    pathway:
      represented_as: node
      preferred_id: [reactome, wikipathways]
      input_label: [react, wiki]
    ```
    
3. **동의어**: 기존 온톨로지 클래스에 더 적합한 이름 부여
    
    ```yaml
    complex:
      synonym_for: macromolecular complex
      represented_as: node
    ```
    
4. **온톨로지 하이브리드화**: 특정 분야에 특화된 온톨로지를 기본 온톨로지와 결합
    
    ```yaml
    tail_ontologies:
      so:
        url: data/so.owl
        head_join_node: sequence variant
        tail_join_node: sequence_variant
    ```
    

### 시각화 도구

BioCypher는 온톨로지 계층 구조를 시각화하는 도구를 제공합니다:

- `show_ontology_structure()`: 사용된 온톨로지 부분만 표시
- `show_ontology_structure(full=True)`: 전체 온톨로지 표시
- `show_ontology_structure(to_disk="/path/to/file")`: 복잡한 온톨로지를 GraphML 파일로 저장

## 활용 사례

BioCypher는 다음과 같은 생물학적 데이터 통합 작업에 적합합니다:

- 단백질 상호작용 네트워크 구축
- 다양한 경로(pathway) 데이터베이스 통합
- 유전자-질병 관계 매핑
- 복잡한 생물학적 시스템의 계층적 표현



---
# BioCypher 기초

BioCypher는 생물학적 데이터를 그래프 데이터베이스(주로 Neo4j)에 효율적으로 변환하고 저장하기 위한 파이썬 프레임워크입니다. 생물학 지식 그래프를 쉽게 구축할 수 있도록 도와주는 도구로, 온톨로지를 활용해 생물학 데이터의 의미론적 일관성을 유지합니다.

## 기본 구조 및 개념

### 1. 핵심 구성 요소

- **BioCypher 객체**: 모든 작업의 중심이 되는 메인 인터페이스
- **어댑터(Adapter)**: 데이터 소스와 BioCypher 간의 연결을 담당
- **스키마 설정**: 데이터 구조를 정의하는 YAML 파일
- **온톨로지**: 생물학적 개념의 계층 구조를 정의

### 2. 설정 파일

BioCypher는 두 가지 주요 설정 파일을 사용합니다:

1. **biocypher_config.yaml**: 전반적인 설정 (온톨로지, 출력 형식 등)

```yaml
biocypher:
  head_ontology:
    url: https://github.com/biolink/biolink-model/raw/v3.2.1/biolink-model.owl.ttl
    root_node: entity
```

2. **schema_config.yaml**: 데이터 구조 정의

```yaml
protein:
  represented_as: node
  input_label: prot
  preferred_id: uniprot
```

## 기본 사용법

### 1. BioCypher 객체 초기화

```python
from biocypher import BioCypher

bc = BioCypher(
    schema_config_path="schema_config.yaml",
    biocypher_config_path="biocypher_config.yaml"
)
```

### 2. 노드 생성

```python
# 단백질 노드 데이터 예시
protein_data = [
    {
        "id": "P12345",
        "name": "Example Protein",
        "taxon": "9606"  # 인간
    }
]

# 노드 추가
for protein in protein_data:
    bc.add_node(
        node_id=protein["id"],
        node_label="protein",
        properties={
            "name": protein["name"],
            "taxon": protein["taxon"]
        }
    )
```

### 3. 관계 생성

```python
# 단백질-단백질 상호작용 데이터 예시
interaction_data = [
    {
        "source": "P12345",
        "target": "P67890",
        "score": 0.95
    }
]

# 관계 추가
for interaction in interaction_data:
    bc.add_edge(
        source_id=interaction["source"],
        target_id=interaction["target"],
        edge_label="protein protein interaction",
        properties={
            "score": interaction["score"]
        }
    )
```

### 4. 지식 그래프 생성

```python
# 그래프 데이터베이스 쓰기
bc.write_nodes()
bc.write_edges()

# 트랜잭션 완료
bc.summary()
```

## 온톨로지 활용

BioCypher는 온톨로지를 활용해 데이터 모델을 정의합니다:

### 1. 기본 Biolink 모델 사용

```yaml
protein:
  represented_as: node
  input_label: prot
```

### 2. 클래스 확장 (명시적 상속)

```yaml
protein isoform:
  is_a: protein
  represented_as: node
```

### 3. 온톨로지 시각화

```python
# 사용된 온톨로지 부분만 시각화
bc.show_ontology_structure()

# 전체 온톨로지 시각화
bc.show_ontology_structure(full=True)
```

## 데이터 출력 옵션

BioCypher는 다양한 출력 형식을 지원합니다:

1. **Neo4j 데이터베이스**: 실시간 그래프 데이터베이스 연결
2. **파일 시스템**: CSV, JSON, GraphML 등의 파일로 출력
3. **가상 그래프**: 메모리 내 그래프 작업을 위한 옵션

```python
# Neo4j 연결 예시
bc = BioCypher(
    driver="neo4j",
    uri="neo4j://localhost:7687",
    auth=("neo4j", "password")
)
```

BioCypher는 복잡한 생물학적 데이터를 구조화된 그래프로 변환하는 과정을 단순화하여, 생물학 연구자들이 데이터 통합과 분석에 집중할 수 있게 도와줍니다.