# One_day_Project
## :o:O/X 분류 모델 설계 및 학습:x:
### 목차
#### 1. 데이터셋 준비 및 전처리
#### 2. 특징 추출 
#### 3. CNN 모델 설계 및 하이퍼파라미터 튜닝 
#### 4. CNN 모델 학습
#### 5. CNN 모델 추론
---
### 1. 데이터셋 준비 및 전처리
* 데이터셋 크기 **600장**
  * 웹 다운로드 및 손글씨
* 128x128 Resize 및 Grayscale 변환
* 훈련용 : 테스트용 = 8: 2
* 이미지 라벨링
  * **'O' 클래스: 0**
  * **'X' 클래스: 1**
    <div align=center> 
      <img src="https://github.com/user-attachments/assets/2a344dcb-d9d0-40e7-8314-21154c31ba1f" width ="500">
  </div>
---

### 2. SIFT 특징 추출
**Q. 'O' 이미지와 'X' 이미지간 어떤 특징을 보고 CNN 모델이 분류를 하는 것일까?**
#### 2.1 각 class 별 feature point 확인
* 'X' 이미지 feature point 확인
  * 기호 **양 끝단** 중점적으로 분포
  * 막대 선 따라 **직선형** 분포
  <div align=center> 
      <br/>
      <img src="https://github.com/user-attachments/assets/304b2f8e-1d9b-432c-a671-789b2b305e81" width ="600">
  </div>

* 'O' 이미지 feature point 확인
  * **원 둘레** 따라 분포
  * **원점**에 대한 keypoint 검출
  <div align=center> 
      <br/>
      <img src="https://github.com/user-attachments/assets/f6c73843-5b29-4f9b-bec0-bf3667c56724" width ="600">
  </div>
---

### 3. CNN 모델 설계 및 하이퍼파라미터 튜닝 
#### 3.1 CNN모델 설계
* 2-classes CNN 분류 모델
  * 3개 Layer 층 + 2개 FC 층
* 입력 데이터 크기: (128, 128, 1) -> **(290, 128, 1)**
* 총 파라미터 수: 1,662,914 -> **18,931,650**
* Optimizer: Adam
* Loss Function: Sparse_Categorical_Crossentropy
#### 3.2 하이퍼파라미터 튜닝
* 최적 하이퍼파라미터 조합 찾기
  * Image Size: [128, 64, 32, 28]
  * Epoch: [10, 20]
  * Learning Rate: 'ReduceLROnPlateau' 콜백함수
  <div align=center> 
      <br/>
      <img src="https://github.com/user-attachments/assets/dbe4a260-4eda-4278-885b-bf2b592d3fee" width ="600">
  </div>
---

### 4. CNN 모델 학습
* 하이퍼파라미터 최적조합
  * epoch: **20** & learning rate: **0.001**
* 최적 성능 지표
  * Training accuracy: 0.93
  * Training loss: 0.177
  * Validation accuracy: **0.87**
  * Validation loss: **0.44**

  <div align=center> 
      <br/>
      <img src="https://github.com/user-attachments/assets/ab57963b-88cc-4cf5-87fb-563d827dfe4f" width ="600">
  </div>
---

### 5. CNN 모델 추론
* 최적 가중치 조합 사용
* 손글씨 Test 이미지 데이터 클래스별 50장
  * Confuision Matrix
    <div align=center> 
      <img src="https://github.com/user-attachments/assets/1c0343db-f841-4443-bedc-07132c1d3e97" width ="500">
    </div>
  * 추론 결과
    <div align=center> 
      <br/>
      <img src="https://github.com/user-attachments/assets/b1419887-5469-4da5-9aa5-aa317c13e901" width ="500">
    </div>
