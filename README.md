# 군집 주행

> 두 대 이상의 트럭이 하나로 연결된 호송대를 구성해 운행하는 기술로 자율주행 기술과 함께 차량 연결 기술이 복합적으로 적용된 주행방법

- 군집 주행으로 트럭의 연비가 증가, 배출 가스가 감소, 도로 정체가 해소, 운전 인력 대체 효과

![8499_12973_3652](https://user-images.githubusercontent.com/81899557/206140450-86746584-f7c0-4044-9902-0d6c30f2c605.jpg)

## 팀원

- 20197120 이병규
- 20197118 강지훈
- 20197124 하상욱

## 직진 및 정지

![KakaoTalk_20221207_172759268](https://user-images.githubusercontent.com/81899557/206127508-f0c9ba91-8f95-4d52-8535-e49d1224c590.gif)

## 커브

![KakaoTalk_20221207_173438398](https://user-images.githubusercontent.com/81899557/206128837-08821e96-3982-45dc-8cb3-6ab592df5983.gif)

## 코드 사용, 업데이트 내용

- 사용할 모델 불러오기

```python
from jetbot import ObjectDetector

model = ObjectDetector('ssd_mobilenet_v2_coco.engine')
```

- 자동차 label로 변경, speed와 turn_gain값을 변경해서 객체 탐지 후 따라가게 설정

```python
from jetbot import bgr8_to_jpeg

blocked_widget = widgets.FloatSlider(min=0.0, max=1.0, value=0.0, description='blocked')
image_widget = widgets.Image(format='jpeg', width=300, height=300)
label_widget = widgets.IntText(value=1, description='tracked label')
speed_widget = widgets.FloatSlider(value=0.4, min=0.0, max=1.0, description='speed')
turn_gain_widget = widgets.FloatSlider(value=0.8, min=0.0, max=2.0, description='turn gain')

display(widgets.VBox([
    widgets.HBox([image_widget, blocked_widget]),
    label_widget,
    speed_widget,
    turn_gain_widget
]))

```

![KakaoTalk_20221207_175717784](https://user-images.githubusercontent.com/81899557/206133960-1353716f-4e31-457a-a563-69e842c2f4c1.gif)

###### - 초록색 바운딩 박스 탐지 시 속도 업데이트
###### - 탐지 실패 속도 0으로 업데이트

- forward 0으로 수정해 자동차 label이 아닌 객체가 탐지되면 스피드를 0으로 바뀌며 멈춤

```python
# otherwise go forward if no target detected
    if det is None:
        robot.forward(0)
```
