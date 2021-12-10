2021년 상반기 진행
* 기본적인 적용 내용
  * 이용된 데이터는 2D 이미지로 학습 내용에서는 Covolution 2D를 적용
  * 커널 함수의 activation에서는 학습 결과가 우수한 Relu 함수를 기본으로 적용
  * 출력 함수의 activation에서는 stable한 결과를 얻기 위해 softmax 함수 적용
  
# CNN_Restaurant_Project

## 대학교 4학년 당시, "BigData Programing" 과목을 통한 프로젝트

### 1.	분야 및 분석 동기
일상에서 사람의 눈이 할 수 있는 부분을 AI에 적용하고자 했습니다. 조그만 범위부터 학습을 통해 AI 적용할 수 있는 모델을 만들려고 생각했습니다. 일상에서 식당 내부와 외부 및 메뉴판을 구분하는 것은 당연한 부분이며, 인공지능 또한 이를 구분할 수 있도록 하는것이 당연하다고 생각했습니다.
식당의 내부와 외부를 구분하고, 메뉴판 또한 따로 구분할 수 있도록 만들고자 해당 프로젝트를 진행했습니다. CNN을 이용한 이미지 분류 정확도와 손실 정도를 측정하였습니다. 학습을 통해서 식당 정보를 구분할 수 있다면 AI의 실생활 적용에도 이점이 있을 것이라 생각하며 이러한 주제를 생각하였습니다.

### 2.	데이터 수집
활용한 데이터는 이미지 데이터로써 JPEG 이미지를 사용하였습니다. 데이터의 출처는 “공공데이터포털”에서 직접 받아와서 사용하였습니다.
-	menupan (메뉴판 데이터 수): 1139개
-	restaurant_in (식당 내부 데이터 수): 582개
-	restaurant_out (식당 외부 데이터 수): 542개
-	총 데이터 수: 2263개
- 출처: [공공데이터포털1](https://www.data.go.kr/data/15076758/fileData.do), [공공데이터포털2](https://www.data.go.kr/data/15076653/fileData.do)

### 3.	분석 결과의 정확도 분석
#### ①	데이터 수집 당시, 첫 링크의 데이터만을 활용하였지만 유효한 정확도를 뽑아내지 못하였습니다. 때문에 두 번째 링크의 데이터를 추가로 수집하여 유효한 정확도와 결과를 얻고자 데이터 수를 추가로 늘렸습니다.
![00](https://user-images.githubusercontent.com/86669008/145525444-1228d9df-cf85-4b3a-9380-42bdb5229655.jpg)
#### ②	보다 높은 정확도를 얻기 위한 분석 결과를 위해 batch 에 따른 분석 정확도가 달라짐을 확인하였습니다. 이에 따라 가장 높은 정확도가 확인되는 batch 를 찾았습니다.
**∴ training_accuracy, test_accuracy 모두 ‘batch=10’일 때 가장 높으므로, ‘batch=10’으로 선택하였습니다.**
-	Condition: train_size=0.7, batch=60, epochs=10

![01](https://user-images.githubusercontent.com/86669008/145526285-d5a5ad4b-cee3-4df6-806b-ec9fab334a12.jpg)
-	Condition: train_size=0.7, batch=30, epochs=10

![02](https://user-images.githubusercontent.com/86669008/145526288-e9bcd659-0f0d-4c68-8cf8-0b01f9b20654.jpg)
-	Condition: train_size=0.7, batch=15, epochs=10

![03](https://user-images.githubusercontent.com/86669008/145526289-b510191a-d653-4ef0-a15e-fbb33dffef96.jpg)
-	Condition: train_size=0.7, batch=10, epochs=10

![04](https://user-images.githubusercontent.com/86669008/145526290-207039e0-9f69-45bf-bb0c-1ceb9518fd5b.jpg)
-	Condition: train_size=0.7, batch=5, epochs=10

![05](https://user-images.githubusercontent.com/86669008/145526293-32875ce1-869f-4fee-9a42-91df07c61677.jpg)
#### ③	train_size 에 따른 분석 정확도의 변화를 확인하였습니다. 이에 따라 정확도 도출이 가장 효과적일 것으로 판단되는 train_size 를 찾았습니다.
**∴ training_accuracy ( train_size=0.7 > train_size=0.6 > train_size=0.8 ) , test_accuracy ( train_size=0.8 > train_size=0.7 > train_size=0.6 ) 인 것을 확인하였습니다. 정확도에 대한 차이가 미미하여, training_accuracy 와 test_accuracy 가 가장 높은 ‘train_size=0.8’과 ‘train_size=0.8’을 고려하였습니다. test_loss 값의 결과로, loss 값이 더 작은 ‘train_size=0.8’을 선택하였습니다.**
-	Condition: train_size=0.6, batch=10, epochs=10

![06](https://user-images.githubusercontent.com/86669008/145526294-fa6a9bb7-8add-4587-8c4e-96a691223d16.jpg)
-	Condition: train_size=0.7, batch=10, epochs=10

![07](https://user-images.githubusercontent.com/86669008/145526298-37748838-8b85-45c6-8c73-60bed545200d.jpg)
-	Condition: train_size=0.8, batch=10, epochs=10

![08](https://user-images.githubusercontent.com/86669008/145526299-86bc9024-6518-4ec4-9238-c77fd1c963c6.jpg)
#### ④	loss 값이 가장 작으면서 accuracy 값이 가장 큰 경우를 찾기 위해 epochs 값에 변화를 주며 결과 값을 확인하였습니다. 이에 따라 가장 높은 정확도가 확인되는 epochs 를 찾았습니다.
**∴ training_accuracy, test_accuracy 모두 높고, training_loss, test_loss 모두 낮은 결과를 보여준 ‘epochs=58’을 선택하여 마무리 분석 결과를 얻었습니다.**
-	Condition: train_size=0.8, batch=10, epochs=30

![09](https://user-images.githubusercontent.com/86669008/145526302-5bd744eb-a622-4786-84d6-59310e61b514.jpg)
-	Condition: train_size=0.8, batch=10, epochs=29

![10](https://user-images.githubusercontent.com/86669008/145526303-14e94eaf-0d69-425d-be31-d85088102e74.jpg)
-	Condition: train_size=0.8, batch=10, epochs=58

![11](https://user-images.githubusercontent.com/86669008/145526304-59af3fa3-59fa-4d88-b65c-a1cf4b3ddca2.jpg)
### 4.	결과의 시사점 및 결론
![12](https://user-images.githubusercontent.com/86669008/145526305-48517678-ace1-4b7f-ae16-f2172a3748f9.jpg)

![13](https://user-images.githubusercontent.com/86669008/145526307-da4e2ccb-1f8b-4345-b078-80f75f929451.jpg)

![14](https://user-images.githubusercontent.com/86669008/145526308-e144afcc-16a8-4a8c-b71c-5552e7e8a2f7.jpg)
-	**‘train_size=0.8, batch=10, epochs=58’의 조건일때**, 해당 이미지 데이터를 분류하여 높은 정확도를 찾을 수 있었습니다.
-	실제로 높은 **‘training_accuracy=0.9987, test_accuracy=0.9956’ 와 낮은 ‘training_loss=0.0060, test_loss=0.0071’** 을 확인할 수 있었습니다.
-	위 결과들에 따라 해당 프로젝트 결과는 활용에 적합하다고 할 수 있습니다.
