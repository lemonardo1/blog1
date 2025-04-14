
(_Ballard et al., 2024, BioData Mining_)

---

### 🔍 **연구 배경**

- 생의학 분야에서는 다양한 오믹스(genomics, transcriptomics, proteomics 등) 및 이미지 데이터(radiomics, pathomics 등)를 통합하여 질병을 이해하고 예측하려는 시도가 증가하고 있음.
    
- 딥러닝은 이러한 이질적이고 고차원적인 데이터를 통합하고 분석하는 데 강력한 도구로 부각되고 있음.
    

---

### 🧠 **주요 내용 및 방법론 분류**

1. **비생성(Non-generative) 기반 딥러닝 모델**
    
    - **Feedforward Neural Networks (FNN)**: 단순 구조, 일부 생물학적 해석 가능성 존재. 대체로 결측치 처리 불가.
        
    - **Graph Convolutional Networks (GCN)**: 유사 환자 네트워크 또는 생물학적 네트워크(PPI 등)를 활용하여 해석 가능성 강화.
        
    - **Autoencoders (AE)**: 고차원 데이터를 저차원으로 압축하며, 공유/고유 정보 학습. 일부는 모달리티 간 합의(consensus)와 보완성(complementary)을 동시에 학습.
        
2. **생성(Generative) 기반 딥러닝 모델**
    
    - **Variational Autoencoders (VAE)**: 라벨 없이 잠재 공간을 구성하며, 결측 데이터 처리 및 생물학적 제약 조건 부여 가능.
        
    - **Generative Adversarial Networks (GAN)**: 두 모달리티 간 관계 학습 및 데이터 생성 가능. 예: omicsGAN, CLUE.
        
    - **Generative Pretrained Transformers (GPT)**: scGPT는 3천만 개 이상의 single-cell 데이터를 사전 학습하여 다양한 downstream task에 높은 성능 제공.
        

---

### 📌 **주요 기술적 통찰**

- **Integration 전략**:
    
    - _Early integration_: 데이터 결합 후 모델 적용
        
    - _Intermediate integration_: 각 모달리티는 개별적으로 처리되되, 중간에서 통합
        
    - _Late integration_: 모달리티 별 모델 후 예측을 결합
        
- **결측치(missingness) 처리 능력**:
    
    - _PoE(VAE 기반)_, _Cross-learning(GAN 기반)_, _unpaired 데이터 처리(GLUE, GLUER)_ 등을 통해 일부 모델은 모달리티 누락된 데이터도 활용 가능
        
- **이미지 데이터 통합**:
    
    - CNN, Pathomic Fusion, GAN 등으로 radiomics/pathomics와 오믹스 데이터의 통합 분석 사례 증가 중
        
- **시간 정보(시계열 데이터)**:
    
    - RNN, LSTM 등을 활용한 Alzheimer 예측 등에서 활용됨
        

---

### 📈 **미래 방향**

- **결측 데이터 처리 기술의 발전**
    
- **이미지와 오믹스 통합의 보편화**
    
- **대규모 사전학습 기반 모델(GPT류)의 활용 확산**
    
- **다중 모달리티 및 시계열 데이터를 포함한 정밀의학 모델 개발**
    

---

### 📝 **결론**

이 리뷰는 딥러닝을 활용한 multi-omics 통합 방법을 체계적으로 정리하며, 각각의 모델이 다루는 문제, 적용 가능한 데이터 형태, 장단점, 해석 가능성, 결측치 대응 능력 등을 비교 분석함. 복잡한 생물학적 정보의 통합 분석을 위한 딥러닝 접근법은 점점 더 다양화되고 있으며, 향후 정밀의학 실현에 핵심적인 역할을 할 것으로 기대됨.



---
## **딥러닝 기반 통합 방법 분류**

#### 🔹 A. **비생성(Non-generative) 모델**

|분류|설명|주요 예시|
|---|---|---|
|**FNN**|단순한 구조, 일부 생물학적 구조 반영 가능|MOLI, SALMON, DeepOmix|
|**GCN**|샘플 유사성 또는 생물학적 네트워크 활용|MOGONET, MoGCN, DeepMOCCA|
|**Autoencoder**|비선형 차원 축소, 공유/고유 정보 추출|MOCSS, DLSF, MAE|

---

#### 🔹 B. **생성(Generative) 모델**

|분류|설명|특징|주요 예시|
|---|---|---|---|
|**VAE**|잠재 공간의 확률 분포 학습|결측치 대응, 해석성|OmiVAE, GLUE, Multigrate|
|**GAN**|생성자-판별자 구조|합성 데이터 생성, 정합성 강화|omicsGAN, CLUE|
|**GPT (Transformer)**|대규모 사전학습 기반|다양한 downstream task 수행 가능|scGPT|

---

### 3. **데이터 통합 전략**

|전략|설명|
|---|---|
|**Early Integration**|모든 모달리티를 결합 후 입력|
|**Intermediate Integration**|모달리티별 처리 후 잠재 공간 통합|
|**Late Integration**|모달리티별 예측 결과를 나중에 통합|

---

### 4. **최근 발전 & 미래 방향**

- **결측 데이터 처리 방법론**: PoE, cross-encoder, attention 기반 보완 등
    
- **이미지 데이터 통합**: CNN, transformer 기반 융합 방법들
    
- **시계열 데이터 처리**: RNN, LSTM, longitudinal Siamese Network
    
- **GPT 기반 대형 모델의 확장**
    

---

### 5. **결론**

- 딥러닝은 multi-omics 통합 분석에 강력한 도구
    
- 각 모델 유형별 장단점, 적용 가능 데이터, 해석 가능성 다름
    
- 향후 결측 데이터 대응 및 multi-modal 통합의 발전 기대
    

---

필요하시면 각 모델에 대한 비교 표나 다이어그램도 그려드릴 수 있어요!