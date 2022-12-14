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
