[[bioinformatics]] [[Topics/Bioinformatics/Single cell analysis|Single cell analysis]]


single cell analysis 분석을 위한 R 패키지



---
# Seurat 5.2.0 주요 명령어 정리

## 기본 Seurat 워크플로우

```R
pbmc <- NormalizeData(pbmc)
pbmc <- FindVariableFeatures(pbmc)
pbmc <- ScaleData(pbmc)
pbmc <- RunPCA(pbmc)
pbmc <- FindNeighbors(pbmc, dims = 1:30)
pbmc <- FindClusters(pbmc)
pbmc <- RunUMAP(pbmc, dims = 1:30)
DimPlot(pbmc, reduction = "umap")
```

## SCTransform 버전

```R
pbmc <- SCTransform(pbmc) %>%
  RunPCA() %>%
  FindNeighbors(dims = 1:30) %>%
  FindClusters() %>%
  RunUMAP(dims = 1:30)
DimPlot(pbmc, reduction = "umap")
```

## Seurat 객체 데이터 접근

### 셀, 유전자, 레이어 이름

- 셀 이름: `colnames(pbmc)` 또는 `Cells(pbmc)`
- 유전자 이름: `Features(pbmc)` 또는 `rownames(pbmc)`
- 셀과 유전자 수: `ncol(pbmc)`, `nrow(pbmc)`
- 레이어 목록: `Layers(pbmc)`
- 멀티모달 데이터 접근 예시:
    
    ```R
    Assays(cbmc)
    Features(cbmc[["RNA"]])
    Features(cbmc[["ADT"]])
    ```
    
- 변동 유전자 관리:
    
    ```R
    VariableFeatures(pbmc)
    VariableFeatures(cbmc) <- var.gene.names
    ```
    

### Identity 클래스 관리

- identity 클래스 설정/조회:
    
    ```R
    Idents(pbmc) <- "seurat_annotations"
    table(Idents(pbmc))
    ```
    
- 특정 셀 그룹 identity 설정:
    
    ```R
    Idents(pbmc, cells = Cells(pbmc)[1:10]) <- "CD4 T cells"
    ```
    
- metadata에 identity 저장:
    
    ```R
    pbmc <- StashIdent(pbmc, save.name = "old.ident")
    ```
    
- identity 클래스 이름 변경:
    
    ```R
    pbmc <- RenameIdents(pbmc, `CD4 T cells` = "T Helper cells")
    ```
    

### 메타데이터 관리

```R
pbmc[[]]
pbmc$nCount_RNA
pbmc[[c("percent.mito", "nFeature_RNA")]]
pbmc$groups <- sample(c("g1", "g2"), size = ncol(pbmc), replace = TRUE)
```

## 발현 데이터 접근 및 설정

```R
pbmc[["RNA"]]$counts
LayerData(pbmc, assay = "RNA", layer = "counts")
GetAssayData(pbmc, assay = "RNA", slot = "counts")

# 데이터 설정
pbmc[["RNA"]]$counts <- new.data
LayerData(pbmc, assay = "RNA", layer = "counts") <- new.data
pbmc <- SetAssayData(pbmc, slot = "counts", new.data = new.data)
```

## 차원 축소 데이터

```R
Embeddings(pbmc, reduction = "pca")
Loadings(pbmc, reduction = "pca")

# 차원 축소 객체 생성
pbmc[["custom_pca"]] <- CreateDimReducObject(embeddings = new.embeddings, loadings = new.loadings, key = "custom_pca")
```

## 데이터 가져오기(FetchData)

```R
FetchData(pbmc, vars = c("PC_1", "nFeature_RNA", "MS4A1"), layer = "counts")
```

## 객체 Subset 및 병합

### 객체 Subset

```R
subset(pbmc, idents = "B")
subset(pbmc, subset = MS4A1 > 2.5 & PC_1 > 5)
subset(pbmc, downsample = 100)
```

### 레이어 분할/병합

```R
ifnb[["RNA"]] <- split(ifnb[["RNA"]], f = ifnb$stim)
ifnb <- JoinLayers(ifnb)
```

### 객체 병합

```R
merged_obj <- merge(ifnb_list$CTRL, ifnb_list$STIM)
merged_obj[["RNA"]] <- JoinLayers(merged_obj)
```

## 의사벌크 분석 (Pseudobulk)

```R
bulk <- AggregateExpression(ifnb, group.by = c("stim", "seurat_annotations"), return.seurat = TRUE)
```

## 시각화

Seurat는 ggplot2 기반이며 다양한 커스터마이징 가능.

```R
DimPlot(pbmc, reduction = "pca")
FeaturePlot(pbmc, features = "MS4A1")
VlnPlot(pbmc, features = c("LYZ", "CCL5"))
DoHeatmap(pbmc, features = heatmap_markers)
```

테마 및 추가 기능 제공: `DarkTheme()`, `NoLegend()`, `HoverLocator()`, `LabelPoints()` 등

## 멀티어세이 기능

여러 Assay를 쉽게 관리하고 전환 가능

```R
cbmc[["ADT"]] <- CreateAssayObject(counts = cbmc.adt)
NormalizeData(cbmc, assay = "ADT", method = "CLR")
DefaultAssay(cbmc) <- "ADT"
FeatureScatter(cbmc, feature1 = "rna_CD3E", feature2 = "adt_CD3")
```

추가 리소스:

- SeuratObject 매뉴얼
- Seurat v5 Assay5 소개