
huggingface 모델

AIDO.Cell-100M은 50백만 개의 세포로부터 다양한 인간 조직과 기관을 포함하는 대규모 데이터로 학습된 최신(SOTA) 세포 기저(Foundation) 모델입니다.  
AIDO.Cell 모델들은 인간의 전사체(Transcriptome) 전 범위를 입력으로 처리할 수 있도록 설계되어, 세포 전체 전사적 맥락에 대한 정확하고 범용적인 표현(Representation)을 학습합니다.  
AIDO.Cell은 제로샷(Zero-Shot) 클러스터링, 세포 유형 분류(Cell-Type Classification), 약물 처리(perturbation) 모델링 등의 작업에서 최신(SOTA) 성능을 달성합니다.

## 모델 구조적 세부사항

AIDO.Cell은 연속적인 유전자 발현 값을 자동으로 이산화(Auto-Discretization)하여 인코딩하며, BERT 스타일의 양방향 Transformer 인코더를 기반 구조로 사용합니다.  
의미론적으로 풍부한 표현을 학습하기 위해서 인코더 전용(Encoder-Only) Dense Transformer 구조를 사용하였으며, SwiGLU와 LayerNorm 등의 현재 최신 기법을 반영하여 아키텍처를 약간 수정했습니다.  
아래 표는 모델 아키텍처에 대한 상세 정보입니다:

|모델|레이어 수(Layers)|히든 크기(Hidden)|헤드 수(Heads)|인터미디어트 히든 크기(Intermediate Hidden Size)|
|---|:-:|---|---|---|
|3M|6|128|4|320|
|10M|8|256|8|640|
|100M|18|650|20|1664|
|650M|32|1280|20|3392|

## AIDO.Cell 사전학습 개요

아래에서는 AIDO.Cell의 사전학습 방법을 간단히 소개합니다. 자세한 내용은 [논문](https://www.biorxiv.org/content/10.1101/2024.11.28.625303v1) 을 참고하세요.  
AIDO.Cell은 Read Depth-Aware(RDA) 사전학습 목표를 사용합니다. 이 방법은 한 세포의 발현 값을 낮은 읽힘 깊이(Read Depth)로 다운샘플링하여 모델이 마스킹된 유전자들의 더 높은 읽힘 깊이에서의 발현 값을 예측하도록 학습합니다.

### 데이터

AIDO.Cell은 50백만 개 이상의 세포로 이루어진, 100가지 이상의 조직 데이터로부터 다양하게 수집된 데이터셋으로 사전학습되었습니다.  
scFoundation에서 부록으로 정리한 리스트를 참고하였으며, 여기에는 GEO(Gene Expression Omnibus), DISCO(Deeply Integrated human Single-Cell Omnics), hECA(human ensemble cell atlas), Single Cell Portal 등의 데이터가 포함됩니다.  
전처리 및 품질 관리 후, 최종적으로 약 50백만 개의 세포와 9630억 개의 유전자 토큰으로 구성된 데이터셋이 구축되었습니다. 이 중 100,000개의 세포를 검증(Validation)용으로 분할하여 따로 설정하였습니다.

### 학습 세부사항

모델 학습은 bfloat-16 정밀도(Precision)로 진행하여 메모리와 속도를 최적화했습니다.  
100M 모델은 256개의 H100 GPU를 사용하여 3일 동안 학습하였으며, 650M 모델은 같은 방식으로 8일 동안 학습을 진행했습니다.

## AIDO.Cell 평가

AIDO.Cell은 단일 세포 유전체 분석 분야에서 제로샷(Zero-Shot) 평가와 파인튜닝(Fine-Tuned) 평가를 모두 수행하였으며, 다양한 작업에서 탁월한 성능을 보였습니다. 자세한 내용은 [논문](https://www.biorxiv.org/content/10.1101/2024.11.28.625303v1) 을 참고하세요.

## 사용 방법

자세한 내용은 [Model Generator](https://github.com/genbio-ai/modelgenerator)를 참고하세요.  
`experiments/AIDO.Cell` 폴더 내 예시를 확인하실 수 있습니다.

## 인용 방법

AIDO.Cell 모델을 사용하실 때는 아래 BibTeX 코드를 인용해주세요:

```
@inproceedings{ho_scaling_2024,
	title = {Scaling Dense Representations for Single Cell with Transcriptome-Scale Context},
	url = {https://www.biorxiv.org/content/10.1101/2024.11.28.625303v1},
	doi = {10.1101/2024.11.28.625303},
	publisher = {bioRxiv},
	author = {Ho, Nicholas and Ellington, Caleb N. and Hou, Jinyu and Addagudi, Sohan and Mo, Shentong and Tao, Tianhua and Li, Dian and Zhuang, Yonghao and Wang, Hongyi and Cheng, Xingyi and Song, Le and Xing, Eric P.},
	year = {2024},
    booktitle={NeurIPS 2024 Workshop on AI for New Drug Modalities},
}
```