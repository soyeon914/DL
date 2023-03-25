# TinyML: Tensorflow lite for microcontroller

[![Yes24](./images/tinyML_bookcover_kor.jpg)](https://www.yes24.com/Product/Goods/91879171)

<!--
[![Oreilly](./images/tinyML_bookcover_eng.jpg)](https://learning.oreilly.com/library/view/tinyml/9781492052036/)
-->

TinyML 번역서의 한국 독자들을 위한 한글 소스코드 저장소를 개설하게 되었습니다. 책에서도 명시하고 있지만, 텐서플로우 프로젝트는 업데이트가 활발히 진행되고 있는 프로젝트입니다. 가장 최신 코드는 아래의 영어 원문 코드를 참조하시기 바랍니다.

- TinyML(Tensorflow Lite) <https://oreil.ly/TQ4CC>

## 실습소스코드

### Google Colab 통한 실습
아래의 Jupyter Notebook 파일은 Google Colab과 연결되도록 만들어두었습니다. 이를 통해 책의 주요 딥러닝 모델 학습 코드를 간편하게 실행해 볼 수 있습니다.

- __Ch04: 사인파 예측하는 모델 만들기__ [create_sine_model_ko.ipynb ](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/tensorflow/lite/micro/examples/hello_world/create_sine_model_ko.ipynb)

    ![](./images/sinewave.png)

- __Ch08: 음성 인식 모델 만들기__ [train_speech_model.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/tensorflow/lite/micro/examples/micro_speech/train_speech_model_ko.ipynb)

    ![](./images/training_audio.gif)
    ![](./images/cross_entropy.gif)

- __Ch12: 마술 지팡이 제스쳐 인식하기__ [train_magic_wand_model.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/tensorflow/lite/micro/examples/magic_wand/train/train_magic_wand_model_kor.ipynb)

    ![](./images/training.gif)
    ![](./images/tensorboard.gif)


### 마이크로컨트롤러 기기를 통한 실습  
기기에서 동작하게 될 소스코드는 본 소스코드 저장소를 직접 다운로드 받은 후 압축을 푼 뒤 아두이노와 같은 마이크로컨트롤러 기기에 업로드 하여 사용할 수 있습니다. 자세한 실습 방법은 책 혹은 아래의 공식개발문서를 참고하세요.

- __소스코드 저장소 다운받기__ [tensorflow-lite-kor-master.zip](https://github.com/yunho0130/tensorflow-lite/archive/master.zip)

    ![](./images/microcontroller.png)

### 마이크로컨트롤러용 텐서플로우 라이트 (TensorFlow Lite for Microcontrollers)

`마이크로 컨트롤러용 텐서플로우 라이트 (TensorFlow Lite for Microcontrollers)`는 아주 작은 메모리(KB)를 사용하는 기기에서 머신러닝모델을 실행하도록 텐서플로우 라이트(TensorFlow Lite)를 이식한 프레임워크입니다.
- 이 프레임워크에 대해 더 자세히 배우고 싶다면 공식개발문서를 확인하세요. [tensorflow.org/lite/microcontrollers](https://www.tensorflow.org/lite/microcontrollers).

### 자주묻는질문 FAQ
- [Issue #84](https://github.com/yunho0130/tensorflow-lite/issues/84) -  Makefile 관련 clang: error: linker command failed with exit code 1 에러
- [하드웨어 구매시 주의할 점](http://blog.naver.com/eonnow/222101071611) - eonnow님 리뷰 감사합니다. 

### Project Showcase

아래의 프로젝트들은 Tensorflow Lite를 활용하여 진행되었습니다. Tensorflow Lite를 활용한 프로젝트라면 자유롭게 Pull Request를 보내주시면 검토 후 추가하도록 하겠습니다. 

### Watch Out - 딥러닝 기반 음성인식 알림 서비스 (모바일 & 애플워치)
Watch Out은 Tensorflow Lite 모델을 이용해 위험한 소리를 대신 인식 해주는 iOS & WatchOS 프로젝트입니다. 

![./images/watchout.gif](./images/watchout.gif)

청각장애인이 사용할 경우를 생각하여 모델 커스텀 트레이닝을 통해 이름을 인식할 수 있도록 트레이닝 가이드를 추가하였습니다. 전반적인 아키텍처는 다음과 같습니다. 

![./images/systemArchitecture.png](./images/systemArchitecture.png)

- __모델 학습으로 바로가기__ [train_speech_model_ios_ko.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/mobile_team_project/model_training/train_speech_model_ios_ko.ipynb)

- 이 프로젝트에 대한 더 자세한 정보는 [여기](https://github.com/yoonseok312/watch-out)를 참고해주세요.


### Watch Ya - 딥러닝 기반 비전인식 디바이스 (라즈베리파이 & Coral)

![./images/watchya.gif](./images/watchya.gif)

Watch Ya는 전동킥보드 탑승자의 헬멧 착용 여부를 탐지하고, 착용하지 않은 경우 경고 알람을 내보내는 Tiny ML 디바이스를 만드는 프로젝트입니다.   

![./images/systemArchitecture_watchya.png](./images/systemArchitecture_watchya.png)


- __모델 학습으로 바로가기__ 
    - (Step1) 헬멧 데이터 전처리 [kaggle-data-processing.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/usecase_watchya_mobility/Step1_helmet_data_processing/kaggle-data-processing.ipynb)
    - (Step2) 모델 학습 및 텐서플로우 라이트 모델 변환 
        - [helmet_classification_for_tinyMLproject_part1.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/usecase_watchya_mobility/Step2_Model_training_and_tflite_convert/helmet_classification_for_tinyMLproject_part1.ipynb)
        - [helmet_classification_for_tinyMLproject_part2.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/usecase_watchya_mobility/Step2_Model_training_and_tflite_convert/helmet_classification_for_tinyMLproject_part2.ipynb)
        - [helmet_classification_for_tinyMLproject_part3.ipynb](https://colab.research.google.com/github/yunho0130/tensorflow-lite/blob/master/usecase_watchya_mobility/Step2_Model_training_and_tflite_convert/helmet_classification_for_tinyMLproject_part3.ipynb)
    - (Step3) 라즈베리파이(Raspberry Pi)에 이식하기  [가이드 살펴보기](https://github.com/yunho0130/tensorflow-lite/tree/master/usecase_watchya_mobility/Step3_Raspberry_Pi_Porting)  
        
- 보다 자세한 내용은 [여기](https://github.com/yunho0130/tensorflow-lite/tree/master/usecase_watchya_mobility)를 참고해주세요.

### Collaborators

> yunho0130(맹윤호), harheem(김하림), prograsshopper(서미지), 0ys(공예슬), yoonseok312(양윤석), dlqh406(이보성), Karmantez(김창윤), kyunghwanleethebest(이경환), new-w(최예진), su-minn(전수민), ProtossDragoon(이장후), yammayamm(김도연), ufo8945(송보영), pmcsh04(조승현), sanghunkang(강상훈)


* TinyML: Tensorflow lite for microcontroller   컨트리뷰션은 아래의 `Github 가이드라인`을 따릅니다.
    - Github 공식 오픈소스 컨트리뷰션 가이드라인 <https://opensource.guide/ko/how-to-contribute/>

### 인용 Citation
본 레파지토리나 <초소형 머신러닝 TinyML>의 내용을 인용하실 때에는 아래의 인용정보를 사용하시면 편리합니다.
```
@book{TinyML-Machine-Learning-with-TensorFlow-Lite,
  title={초소형 머신러닝 TinyML: 모델 최적화부터 에지 컴퓨팅까지 작고 빠른 딥러닝을 위한 텐서플로 라이트},
  author={피트 워든, 대니얼 시투나야케， 맹윤호(역), 임지순(역)},
  isbn={9791162243411},
  url={https://www.hanbit.co.kr/media/books/book_view.html?p_code=B3963656224},
  year={2020},
  publisher={한빛미디어}
}
```
