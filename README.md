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
