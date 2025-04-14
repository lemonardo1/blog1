[[seurat]]

# Seurat v5의 변경사항

Seurat v5가 CRAN에서 출시되어 이제 새로운 설치의 기본 버전이 되었습니다. Seurat v5는 Seurat v4와 호환되도록 설계되어 기존 코드가 계속 실행되지만, 사용자 결과에 영향을 미치는 소프트웨어 변경 사항이 있습니다. Seurat v4의 이전 워크플로우를 재현하려는 사용자는 설치 페이지의 지침에 따라 이 버전을 계속 설치할 수 있습니다.

특히 다음 사항이 변경되었습니다:

- **Seurat Object와 Assay 클래스:** Seurat v5는 이제 디스크 기반 행렬을 포함한 추가 assay 및 데이터 유형을 지원합니다. 이를 위해 업데이트된 Seurat v5 assay를 도입했습니다. 사용자는 [자세한 정보 비네트]를 확인할 수 있습니다. 간단히 말해, Seurat v5 assay는 데이터를 layer(이전에는 'slot'이라고 함)에 저장합니다. 예를 들어, 이러한 layer는 원시 카운트 `(layer='counts')`, 정규화된 데이터 `(layer='data')`, 또는 z-점수/분산 안정화 데이터 `(layer='scale.data')`를 저장할 수 있습니다. 데이터는 `$` 접근자(예: `obj[["RNA"]]$counts`) 또는 `LayerData` 함수(예: `LayerData(obj, assay="RNA", layer='counts')`)를 사용하여 접근할 수 있습니다. 이러한 업데이트는 사용자에게 최소한의 변경으로 설계되었습니다. v4의 기존 Seurat 함수와 워크플로우는 v5에서도 계속 작동합니다. 예를 들어, `GetAssayData(obj, assay="RNA", slot='counts')` 명령은 Seurat v4와 Seurat v5 모두에서 성공적으로 실행됩니다.
    
- **통합 워크플로우:** Seurat v5는 저차원 공간에서 통합을 수행하고 속도와 메모리 효율성을 향상시키는 간소화된 통합 및 데이터 전송 워크플로우를 도입합니다. 통합 결과는 두 워크플로우 간에 동일하지 않지만, 사용자는 원한다면 Seurat v5에서 v4 통합 워크플로우를 계속 실행할 수 있습니다. 이전 버전의 Seurat에서는 통합 워크플로우에 여러 Seurat 객체 목록이 입력으로 필요했습니다. Seurat v5에서는 모든 데이터를 단일 객체로 유지할 수 있지만, 통합 전에 사용자는 단순히 layer를 분할할 수 있습니다. 자세한 내용은 통합 소개 비네트를 참조하세요.
    
- **차등 발현:** Seurat v5는 이제 가능한 경우 차등 발현 분석을 수행하기 위해 presto 패키지(Korunsky 및 Raychaudhari 연구실에서 개발)를 사용합니다. presto를 사용하면 DE 테스트 속도를 크게 향상시킬 수 있으며, 사용자들이 이를 설치할 것을 권장합니다. 또한 Seurat v5에서는 세포 수준 대신 그룹 수준에서 pseudocount(log-FC 계산 시)를 구현합니다. 결과적으로 사용자는 v5에서 더 높은 logFC 추정치를 관찰하게 됩니다 - 그러나 이러한 추정치가 더 불안정할 수 있다는 점을 유의해야 합니다 - 특히 두 그룹 중 하나에서 매우 낮게 발현되는 유전자의 경우. 이 주제에 대해 McCarthy 및 Pachter 연구실의 피드백에 감사드립니다.
    
- **SCTransform v2:** Choudhary와 Satija, Genome Biology, 2022에서 sctransform의 업데이트된 버전 2를 구현했습니다. 이제 Seurat v5에서 `SCTransform`을 실행할 때 기본 버전입니다. 이전 워크플로우를 실행하려는 사용자는 `SCTransform` 함수에서 `vst.flavor = "v1"` 인수를 설정할 수 있습니다.
    
- **Pseudobulk 분석:** 단일 세포 데이터셋이 세포 하위 집단을 주석하도록 분석되면, pseudobulk 분석(즉, 주어진 하위 집단과 샘플 내에서 세포를 함께 집계)은 노이즈를 줄이고, 낮게 발현된 유전자의 정량화를 개선하며, 데이터 행렬의 크기를 줄일 수 있습니다. Seurat v5에서는 pseudobulk 분석을 수행하기 위해 `AggregateExpression` 함수 사용을 권장합니다. `AggregateExpression`을 사용하여 여러 다른 조건에서 scRNA-seq 데이터의 강력한 차등 발현을 수행하는 방법의 예는 차등 발현 비네트와 췌장/건강한 PBMC 비교를 확인하세요.
    