
논문에서 다양한 종류의 종양 연관 대식세포(Tumor-Associated Macrophages, TAMs)를 분석한 내용을 한국어 표로 정리해드리겠습니다.

reference: # Macrophage diversity in cancer revisited in the era of single-cell omics

[Ruo-Yu Ma](https://www.cell.com/trends/immunology/fulltext/S1471-4906\(22\)00094-1#)1 ∙ [Annabel Black](https://www.cell.com/trends/immunology/fulltext/S1471-4906\(22\)00094-1#)2 ∙ [Bin-Zhi Qian](https://www.cell.com/trends/immunology/fulltext/S1471-4906\(22\)00094-1#)1,2,3 [Binzhi.Qian@ed.ac.uk](mailto:Binzhi.Qian@ed.ac.uk "Send email to Bin-Zhi Qian")


## 종양 연관 대식세포(TAMs)

| 분류 | 특징 마커 | 주요 기능 | 발견된 암 종류 |
|------|----------|----------|-------------|
| IFN-TAMs (인터페론 프라임 TAMs) | CXCL9/10/11, ISG15, PDL1, CD274, CASP1/4, IDO1 | • 면역억제 작용• T세포 소진 유도• 인터페론 반응 유도• 조절 T세포 유입 촉진 | 유방암, 대장암, 교모세포종, 간세포암, 두경부암, 림프종, 폐암, 췌장암 등 |
| Reg-TAMs (면역조절 TAMs) | ARG1, MRC1, CX3CR1, TREM2, IL-10 | • T세포 억제• 항원 제시 기능• 면역관문 조절 | 유방암, 방광암, 대장암, 위암, 간암, 림프종, 흑색종, 폐암 등 |
| Inflam-TAMs (염증성 TAMs) | IL1B, CXCL1/2/3/8, CCL3, CCL3L1, S100A8/A9 | • 면역세포 모집 및 조절• 염증 촉진• 호중구 유입 유도 | 대장암, 위암, 골육종, 척추 상의세포종 |
| LA-TAMs (지질 연관 TAMs) | APOC1, APOE, ACP5, FABP5, CD163, TREM2 | • 식균작용• 종양세포 EMT 촉진• 지질 대사 촉진• 면역억제 | 유방암, 대장암, 교모세포종, 위암, 간암, 두경부암, 폐암, 췌장암 |
| Angio-TAMs (혈관신생 TAMs) | VEGFA, SPP1, VCAN, FCN1, THBS1, HIF1A | • 혈관신생 촉진• CAF 상호작용• 종양세포 EMT 촉진• HIF 경로 활성화 | 유방암, 대장암, 폐암, 비인두암, 난소암, 췌장암, 갑상선암 등 |
| RTM-TAMs (조직 상주 대식세포 유사 TAMs) | LYVE1, HES1, FOLR2, 위치 특이적 마커(간: VSIG4, 폐: MARCO) | • 조직 특이적 기능• 정상 대식세포와 유사• 종양 침습성 촉진• 조절 T세포 모집 | 간암, 대장암 전이, 폐암, 교모세포종 등 |
| Prolif-TAMs (증식성 TAMs) | MKI67, CDK1, CDC45, HMGB1 | • 증식 활성 높음• 세포 주기 활성화• 염증성 기능 | 위암, 대장암, 섬유육종, 전립선암, 폐암, 난소암, CNS 종양 |

## 추가 관련 세포 유형

| 세포 유형 | 특징 |
|----------|------|
| 종양 침윤 단핵구(TIMs) | CD14+, S100A8/9, FCN1 발현, 고전적 단핵구와 유사하나 염증 마커와 성장 조절자 발현 증가 |
| 비고전적 단핵구 | CD16+, CX3CR1, FCGR3A/B 발현, 정상 인접 조직에 풍부 |
| 중간 단핵구 | CD14+CD16+, CX3CR1, ISG15/20 발현, 인접 정상 조직에 풍부 |



---
M1 macrophages 

- Overexpress CD80, CD86, and CD16/32
- Express HLA-DR and CD197
- Secrete pro-inflammatory cytokines
- Genetic markers include IL1a, IL1b, IL6, NOS2, TLR2, and TLR4

M2 macrophages

- Express arginase-1 (Arg-1), mannose receptor (CD206), anti-inflammatory factor (IL-10) and chemokines CCL17 and CCL22 

- Express CD163, CD209, and CD206 

- Activated through cytokines including IL4, IL10, and IL13


## 단일세포 UMAP 분석의 주요 세포 마커 설명표

PDF 파일에 제시된 UMAP 시각화에서 볼 수 있는 주요 세포 마커에 대한 설명 표를 작성했습니다.

| 마커     | 세포 유형                               | 특징                                  | UMAP에서의 위치          |
| ------ | ----------------------------------- | ----------------------------------- | ------------------- |
| KRT14  | Epithelial cell (기저층)               | 기저 각질세포 마커로 피부, 유방 등의 기저층 상피세포에서 발현 | 상단 중앙 클러스터에 강하게 발현  |
| COL1A1 | Fibroblasts                         | 제1형 콜라겐 생성, 결합조직과 세포외기질 형성에 관여      | 우측 하단 클러스터에 발현      |
| RGS5   | Pericytes                           | 혈관 평활근 세포 및 혈관주위세포 마커               | 우측 중간-하단 영역에 약하게 발현 |
| PMEL   | Melanocytes                         | 멜라닌 생성과 관련된 멜라닌세포 특이 마커             | 좌측 하단 영역에 발현        |
| KRT7   | Epithelial cells (ductal/glandular) | 단순 및 이행 상피의 마커로 관상/선상 상피세포에서 발현     | 전체적으로 약하게 분포        |
| SELE   | Vascular endothelial cells          | E-셀렉틴으로 염증 부위의 혈관내피세포에서 발현          | 좌측 중앙-상단 영역에 발현     |
| CD68   | Macrophages                         | 대식세포와 단핵구 계열의 세포 마커                 | 중앙 우측 영역에 분포        |
| CD3D   | T lymphocytes                       | T 세포 수용체 복합체의 일부로 T 림프구의 특이 마커      | 우측 상단 영역에 강하게 발현    |

