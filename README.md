# Yolo-Pytorch

분석 주제: 실시간 객체 검출(Object Detection)

실습 데이터 셋

1.얼굴 마스크 탐지

2.개/고양이 품종 탐지

3.라쿤 탐지

# 실습 가이드

1.Colab에서 구현

2.Jupyter lab에서 구현

# 데이터 저장소

3가지 dataset 모두 roboflow에서 제공하는 Dataset

1. https://public.roboflow.com/object-detection/mask-wearing/1/download

2. https://public.roboflow.com/object-detection/oxford-pets

3. https://public.roboflow.com/object-detection/raccoon

Format은 YOLO5-Pytorch로 설정하고 데이터 셋 다운로드

# 데이터 셋 경로 확인하기

data.yaml파일을 통해 데이터 셋의 환경 설정 파일을 수정.

data.yaml 파일에는 데이터셋의 경로 등 YOLO v5가 참고할 수 있는 환경 설정 정보가 포함됨.

![image](https://user-images.githubusercontent.com/104436260/207486983-672314ac-2ca8-4531-a3d0-20e489e42812.png)

![image](https://user-images.githubusercontent.com/104436260/207487043-754ca425-0041-466c-b2f7-a0b51d9105dd.png)

절대 경로 위와 같이 변경

# yaml 파일 파싱하여 환경 정보 파이썬 객체로 저장

![image](https://user-images.githubusercontent.com/104436260/207488030-9990c534-e123-409f-85c5-6f3972319c9b.png)

# Dataset EDA

![image](https://user-images.githubusercontent.com/104436260/207502911-e0a4f702-f31e-4c22-ab7a-5b6d23829d5d.png)

# 바운딩박스 만들기

![image](https://user-images.githubusercontent.com/104436260/207503093-93faca29-eaea-48e9-bca9-4aab52f4462a.png)

![image](https://user-images.githubusercontent.com/104436260/207503197-46fefdac-9c45-439b-9038-d5767610426f.png)

# YOLO 아미텍처 핵심정리

YOLO는 객체 탐지에 필요한 많은 구성요소를 하나의 네트워크로 통함함.

하나의 이미지에 대한 전체적인 특징을 추출한 후, 각 그리드에 대해서 예측 결과 구함


# YOLO1

YOLO1은 이미지를 받아 특징을 추출한 뒤에 7x7 그리드 셀마다 클래스를 예측함

출력 텐서의 크기=7X7X30(채널의길이)=7X7X(2개(바운딩 박스 개수))X5개(바운딩 박스 좌표와 confidence score)+20개(클래스 개수)->예시임

이후에 NMS을 이용해 하나의 객체에 대하여 가장 confidence score가 높은 바운딩 박스만 남김

input Size=448x448x3

448x448x3->112x112x192->56x56x256->28x28x512->14x14x1024->7x7x1024->fully connected->4096->output=7x7x30

# YOLO2

속도 측면에서 높은 이점이 있는 Darknet-19을 제안함

9000개의 클래스를 분류할 수 있는 YOLO 9000을 제안함

mAP(정확도)가 많이 향상됨

K-means 클러스터링을 이용해 ground-truth box(실제 이미지에서 해당 객체의 정보를 나타낸 것)와 유사한 anchor box 학습한 뒤에 사용함.

특정한 데이터 셋에 적합한 anchor box를 찿을 수 있기 때문에 성능이 많이 개선됨.

더 적은 개수의 anchor box를 사용해도, 고정된 anchor box보다 더 좋은 성능을 보임.

YOLO 2는 fully connected를 사용하지 않음

하나의 그리드 셀마다 5개의 anchor box를 통해 예측을 수행함

하나의 그리드 안에서 anchor box 별로 클래스 확률을 예측함

# YOLO 3

Darknet 53 아키텍처 사용

Residual block 사용

바운딩 박스 예측->logistic regression을 이용해 사물이 존재하는지 예측.

# YOLO 4

512x512 고해상도 이미지를 입력으로 받음

CSPNet에서 제안된 아이디어를 적용함

다양한 기술들을 YOLO 아키텍처에 적용하여 정확도를 높임

# 소스코드 다운하여 객체인식 진행하기

YOLO v5로 진행
Pytorch 기반 코드로 수행

YOLO v5 Samll

YOLO v5m Medium

YOLO v5l Large

YOLO v5x XLarge

# 샘플 데이터 객체인식 진행

![image](https://user-images.githubusercontent.com/104436260/208354880-449c3bc1-1670-47c4-a0ce-bbf4425975f0.png)

![image](https://user-images.githubusercontent.com/104436260/208354050-1d5a5888-d4f8-499a-a363-97b9d3de09d4.png)


# mask data training 진행

![image](https://user-images.githubusercontent.com/104436260/208358366-5208ecb6-2022-4649-8254-7f54940e970d.png)

# 학습결과

![image](https://user-images.githubusercontent.com/104436260/208359756-56ab8b36-8deb-49bb-9e05-c5d448a49b4c.png)

트레인 이미지 바운딩 박스 생성

모자이크 기법을 사용하기 때문에 하나의 이미지에 4개의 이미지가 섞여서 학습됨

![image](https://user-images.githubusercontent.com/104436260/208360299-63c841a2-74a4-4579-ac12-a70274cc6505.png)

# 테스트 예측 결과

![image](https://user-images.githubusercontent.com/104436260/208360639-f0e3b48a-1acf-4ef9-bfa9-db4d4f908ad1.png)

전반적으로 마스크를 착용 유무 detecting함

# Tensor board 시각화

![image](https://user-images.githubusercontent.com/104436260/208361784-ae7b2cc8-692b-4214-8d6f-833077a11488.png)

# Test 결과

![image](https://user-images.githubusercontent.com/104436260/208362282-80b6c4fe-b755-43b8-a517-946f87a8639f.png)



