https://aifactory.space/competition/detail/1434

keras 기본 제공 데이터 이용
모든 모델 tensorflow keras 라이브러리 사용


<baseline_CNN>

    학습속도 빠름
    
    정확도 약 0.90
    
    
    

<VGG16>

    VGG16의 input인 244,244 사이즈를 맞추기 위해
    cv2 resize 방법은 알아냈지만, 이미지 한장당 resize 방법만 알아냈고,
    60000만장 전체를 resize하는 방법을 찾느라 오래걸림
    -> for문으로 new array 에 resize 할당으로 해결
    -> but 메모리 초과
    -> conv_layer 수를 줄이고 input_size = (28,28)
    
    정확도 약 0.92
   
   
<VGG16 ( Transfer Learning )>

    input으로 (28, 28) 들어가지 않음
    
    
    

<EfficienNet ( Transfer Learning ) ( 32, 32, 3 )>

    train 10000개 추출해서
    최소 input_size인 (32, 32, 3) 으로 학습
    학습속도 빠름
    --> epoch를 늘리면 정확도를 높아질 것으로 예측
    
    정확도 약 0.77


<EfficienNet ( Transfer Learning ) ( 300, 300, 3 )>

    train을 2000개만 추출해서
    input_size = (300, 300, 3)
    --> 정확도 매우 낮음 & 속도 느림
    --> Transfer Learning 이기에 초반부 높은 loss 값으로 시작
    --> 더 많은 epoch가 필요할 것이라고 예상됨
 
    정확도 약 0.10
    train 정확도에 비해 test 정확도가 매우 낮음!!!
    --> 사이즈를 키우는 과정이 잘못됐나?
    --> 모델 학습량이 부족했나?
    --> train data의 양이 부족했나?




<전체적으로>

    epoch = 10, batch_size = 64 로 고정
    --> hyperparameter tuning 진행하면 정확도 높아질 것으로 예측
    
    validation set 사용 x
    --> cross validation 사용 시 정확도 높아질 것으로 예측







데이터 불균형 확인 안했음!

불균형한 데이터에서는 -> 정확도로 모델을 판단하는 것이 안좋을 수 있음.
따라서 혼동 행렬을 봐야함


model.compile 의 metrics를 사용자 정의 함수를 사용함을 통해
Precision, recall, f1 score 등등을
return값으로 받아올 수 있다
(근데 이게 모델 학습 전에 미리 선언해놓아야 하는 것 같다.)







<<<<<<오류>>>>>>>>
Creating variables on a non-first call to a function decorated with tf.function.
해결 : jupyter 재시작
