# Grad-CAM 알고리즘을 통한 반도체 웨이퍼 불량 분석 및 원인 분석

##### 코드 정리 및 향후 업로드

- Grad-CAM 알고리즘을 통해 반도체 웨이퍼의 불량 패턴의 원인이 되는 주요 위치를 파악하여 주요 픽셀들만 남기고, 나머지 픽셀들을 제거하는 새로운 반도체 웨이퍼 빈 맵 디노이징 기법
- `Grad-CAM` : 설명 가능한 인공지능인 XAI 기법 중 하나로 AI의 이미지 분류 과정에서 가중치를 주어 근거가 되는 픽셀을 선정하고, 이를 히트맵으로 표현할 수 있게 해주는 알고리즘
![image](https://user-images.githubusercontent.com/79157951/230638767-b30de38c-e934-4074-b55c-84914d56bf92.png)
![image](https://user-images.githubusercontent.com/79157951/230638821-3af43681-c75b-4e1b-9123-6f8ff4c16710.png)

# Data
- Kaggle에서 제공하는 실제 제조 현장 46,393개의 lots에서 수집된 811,457개의 반도체 웨이퍼 맵 이미지 데이터셋(WM-811K) 활용 [Link](https://www.kaggle.com/datasets/qingyi/wm811k-wafer-map)
![image](https://user-images.githubusercontent.com/79157951/230638960-ec976d20-d258-4c58-ae21-1d6bc60b103e.png)

# Data Preprocessing
- Labeling이 없는 데이터 삭제
- Grad-CAM 알고리즘을 통해 주요 불량 위치를 파악할 의미가 없는 Failure Type 제거 -> `Random`, `Near-full`, `None`

# Model Training
- `VGGNet` `ResNet` `EfficientNet` 모델을 통해 5 epoch로 훈련 수행
- 모델 학습 결과
![image](https://user-images.githubusercontent.com/79157951/230639518-f1899bd8-e2a7-40ed-af70-acf87a3e3566.png)

# Grad-CAM
- AI의 Image Classification을 수행하는 데에 있어 높은 가중치를 주어 분류한 픽셀들을 선정하는 과정
- 반도체 웨이퍼 맵 불량 패턴을 Classification하는 과정에서 근거가 되는 픽셀들을 확인
- 특정 불량이 빈번하게 나타나는 위치를 파악

![image](https://user-images.githubusercontent.com/79157951/230639799-04bd6ea0-5eac-4d43-9526-fe2d242ff670.png)
![image](https://user-images.githubusercontent.com/79157951/230639805-615ee843-d35d-4a3e-833b-bbcd985126de.png)

# Denoising
- `Denoising` : 이미지 데이터 내에 존재하는 Noise를 제거하는 작업으로, 이미지 기반 인공지능 학습에 있어 중요한 전처리 기법
- 이미지 내에 존재하는 불량 패턴을 강조할 수 있으며 이를 통해 새로운 불량 패턴 정의가 가능하고, 보다 높은 학습 효율
- 기존 Image Denoising

![image](https://user-images.githubusercontent.com/79157951/230640009-b60469c7-552f-4812-ad4f-f6f190406495.png)

- 개선 Image Denoising

![image](https://user-images.githubusercontent.com/79157951/230640054-7f6859c1-9a44-4d3d-872e-0eb8130812be.png)
