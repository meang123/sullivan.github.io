---
layout: single
title:  "Basic concept of DL"
categories: Deep learning,MLP,perception,cnn,CNN
tag : [Deep learning,CNN,backprophagation,MLP,perception,DL,gradient descent]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
typora-root-url: ../



---





## Computer vision 분야가 어려운이유 

 

- 빛
- 관점에 따라 사물이 달라보인다 viewpoint
- 착시 효과 - 인지와 측정된 값은 다르다
- Motion
- 그림에서 여러 개 보이는 영상(멀리서 보면 인지 할 수 있는 객체들)
  - 이런건 local feature를 보고 판단할수가 없다 
- 한 사물에 대해서도 다양한 버전이 있다 (의자가 다 같은 의자 모양이 아니다)





# DL concept정리 



가중치와 편향을 학습하여 결과를 내는 것이다.  즉 파라미터를 최적화 하는 문제로 볼수도 있다. 물리나 수학 영역에서는 어떤 현상에 대한 모델 정의를 먼저 하고 나서 조정하는 과정이라면 신경망에서는 모델 정의를 신경망에서 할수있도록 파라미터 값을 계속 조정해 주는것이다. 



**batch,iteration,epoch**

예 ) 2000개의 dataset epoch=20, batch size = 500이면 

1 epoch마다 bath size 500만큼이니까 총 iteration은 4번이다 



**supervised learning**

정답 label이 존재하는 dataset



**Unsupervised learning**

정답 label이 없는 dataset -> data의 구조를 학습한다 



* clustering algorithms 

* Audoencoder

  * encoder network에 input data 넣고 decode network를 통해 reconstructe한다 결과를 input data와의 차이로 loss function을 계산한다 그래서 목표는 input data와 reconstucted output결과의 loss가 최소화가 되는것이다

  * encoder에서 데이터를 압축하여(SVD) decoder에서 다시 복원 하는 결과물의 차이를 loss로 잡고 학습 시키는것이다 

    결국 train할때는 (x_train,x_train)으로 들어간다

    

**semi-supervised learning**











---



### Activation function 



일반적으로 신경망은 입력 값과 가중치의 곱 + 편향으로 이루어진 선형식을 기반으로 가정한다 h(x) = w1 * x1 + w2 * x2….

선형식을 여러개의 은닉층을 거치고 나와도 결국 선형식일뿐이다 선형 변환만 수행이 된다 -> Activation function이 등장한 이유  



non-linear transformation인 activation function을 해줌으로써 입력값으로 이루어진 선형 식을 더 복잡하게 표현 할수가 있다. 

비선형성이 그러면 어디서 확보가 되는가? 여러 층에서 거쳐나온 활성화 함수의 결과를 조합하는 과정에서 비선형성이 확보가 된다 

MLP를 사용해서 손글시를 분류 한다고 하면, weight는 pattern을 이미지에서 찾는다 bias는 해당 이미지에서 반드시 이 패턴이 있어야 함을 의미 한다 

activation function을 거치면서 weight&bias를 통해 패턴을 찾아간다 hidden layer거칠수록(NN더 들어갈수록) 찾은 패턴을 더 정교한 패턴으로 전환해 간다(찾은 패턴 조합)

마지막 layer에서는 최종 패턴을 통해 이미지를 구별하기 위한 패턴을 파악해서 확률을 매긴다 

즉 활성화 함수를 통해 찾은 패턴들을 조합하여서 더 정교한 패턴으로 전환하여 마지막 최종 패턴을 통해 이미지를 구별하여 확률을 매긴다는것이다. 



-----

### Gradient descent 

정의한 loss function에 대해서 최소를 찾아야하는 optimizer가 필요하다 그 방법중 하나가 gradient descent이다 

GD는 어떤 방향으로 가야 하는지 알려준다 최소를 찾아야 하기 때문에 수식에서 (-)가 있는것이다. 또한 local minimal만 보장한다 global minimal은 보장하지 않는다 

파라미터가 많아서 gaussian newton방식은 계산 복잡도가 높다 그래서 GD를 사용한다 



Dataset이 큰 경우 GD계산을 하는건 느리니까 mini batch로 나눠서 GD계산하는것이 빠르다  이 방식이 SGD이다 

mini batch 별로 GD를 계산하면 sampling한것 마다 GD 방향이 다르게 나올것이다. 하지만 전체를 평균을 내면 결국 하나의 방향을 얻을수있다.  전체 데이터를 보는것이 아니다 일종의 approximate of real gradient이다.  



보통 SGD라고 하면  mini batch SGD를 의미 한다 전체 데이터를 batch만큼 나눠서 학습 하는것이다. 예를 들어서 2000개의 데이터 셋에 batch가 500이면 500개씩 총 4번의 iteration을 거치는것이다. 그러면 1 epoch당 4번 GD를 계산하는것이다. 





---

### Back propagation 

신경망의 노드는 여러 가중치 변수들의 행렬곱으로 이루어져 있다. 문제는 이러한 신경망 구조에서(복잡한 노드로 이루어져있다) GD계산을 어떻게 계산할수있는지가 문제이다. 이때 사용하는 방법이 back propagation알고리듬이다. backpropagation은 chain rule로 가중치의 각 변수들의 GD를 계산하는 방식이다



> 만약 가중치 (2*3) 출력 노드 3개가 있을때 9(3 * 3)개의 행렬 2개가 출력으로 나온다 
>
> 



![image-20240417133712783](/images/2024-03-03-Deel_learning/image-20240417133712783.png)





loss함수에서 backpropagation해서 w1에 적용하는 과정이다 w1은 위에 처럼 2*2행렬(w00~w11)로 이루어져 있다 결국 계산 결과로 나온 [4,-4,1,-1]의 의미는 w00이 변할때 4배만큼 변한다는 의미고 w01변할때 -4만큼, w10변할때 1만큼 ,w11변할때 -1만큼 변한다는 의미 이다 그래서 gradient이용할때 변화량(미분값)만큼 변화 시켜서 최적값 찾는것이다 









**backpropagation, gradient에 대한 내용은 lecture 5, 6 ipynb파일 보면 도움 될것 같다 **





---

# cross entropy



![entropy_image]({{site.url}}/images/2024-03-03-Deel_learning/IMG_KEEP_1671103896.jpg)



-log함수의 모양으로 확률이 높을수록 정보량이 낮고 확률이 낮을수록 정보량이 높다 즉 0에 수렴할수록 정보량은 무한대가 되고 1에 수렴할수록 0에 수렴한다 

기대값 공식 처럼 엔트로피 공식도 같은 결이다. 정보값에 확률값을 곱한것에 합이 엔트로피이다. 





binary classification(0과 1을 구분하는 신경망)의 경우를 예를 들면 신경망에서 나온 결과를 확률값 0-1사이로 정규화를 해주고(sigmoid함수를 이용해서 정규화 해도됨) 정규화 한 값을 기준으로 loss function을 계산해야 한다 (문제 정의마다 loss function은 달라진다)

binary classification의 경우 loss function으로 BCE loss를 사용한다 0인 확률과 1인 확률의 합이 최소가 되어야 하기 때문이다 -(y1 logp + (1-y) log(1-p) )



보통 다중 분류 문제에서 loss function으로 사용된다 위에서 binary classification에서는 sigmoid함수를 이용해서 0-1사이로 정규화 했다면 다중 분류 문제에서는 softmax를 통해 0-1확률값으로 정규화 한다 softmax에서 확률값 구한것에 one hot encoding한 행렬 곱하면 해당 label에 대해서만 활성화 되는 효과가 있다. 



cross entropy 입력으로는 softmax의 값과 , one hot 정답 label이 들어간다 즉 예측값과 정답값이 들어간다 



**cross entropy보다 더 좋은 성능을 내는 Focal loss, Asymmetric loss가 있다. **





----

### one hot encoding 

multi classification에서 주로 사용하는 방법이다. 분류하고자 하는 label을 one hot encoding을 해줌으로써 labe domain을 표현 한것이다. 








----



# Batch normalization



vanishing gradient를 해결해주기 위해 사용한다. 말그대로 batch 단위로 정규화 해주는것이다. 

총 4가지 변수가 있다 평균,분산, 감마(scale),베타(shift)이다. BN에 대한 직관은 흩어진 모래알을 모래성처럼 모았다가(평균과 분산 이용해서 정규화) 다시 흩뿌린다(감마와 분산만큼) vansighing gradient가 발생하는 이유는 예를 들어 시그모이드 활성화 함수라고 하면 데이터가 1주변에 몰려있거나 음수주변에 몰려 있기 때문이다 이러면 변화량이 0이라서 업데이트가 되지 않는다 그래서 BN을 통해 정규화를 해주면(가우시안분포 모양) 1과 음수주변에 모여있던 데이터가 0인 원점으로 모이면서 vanishing gradient가 예방이 된다. 하지만 이때 정규분포의 모양이 모두 같다면 들어오는 입력에 따라 모두 같은 정규화를 가지게 되므로 감마와베타가 등장한다. 감마는 정규분포의 크기를 조절하는것을 의미하고 베타는 정규분포의 shift를 의미한다. 그래서 train일때는 loss가 줄어드는 방향으로 감마와 베타가 학습을 한다. 또한 정규화가 되기 때문에 기존에 bias를 broadcast하는게 의미 없다 그래서 bias=False로 설정을 해야 한다. 

Train할때는 batch 단위로 평균과 분산을 구해서 정규화 할수있었는데 Test할때는 어떤데이터가 들어올지 모른다 그래서 train 시간에 moving average(전체 데이터를 몰라도 평균을 구할수있다)를 통해 평균과 분산을 학습한다 즉 train 때 평균과 분산은 moving avg를 통해 학습되고 감마와 베타는 backpropagation을 통해 학습이 된다 



덕분에 초반에 가중치 초기화가 중요했는데 batch normalization나오고 나서 그 중요도가 많이 떨어질수있었다. 



비슷하게 layer normalization이 있다 이건 batch 단위가 아니라 layer단위로 정규화를 하는것이다 단위만 다르고 개념은 같다 



-----

### Drop out, Early stopping,weight decay

overfitting을 방지하는 용도이다.  뉴런을 랜덤하게 끄는 역할이다 매번 랜덤하게 뉴런이 꺼지면 매번 다른 신경망을 학습하는 효과를 얻을수있다.  랜덤으로 꺼진 뉴런의 정보를 보상하기 위해 안꺼진 다른 뉴런에서 보상한다 단 train할때만 사용한다 

이외에도 batch, batch norm, early stopping, weight decay등의 방법도 있다 그러나 가장 강력한 정규화 방법은 데이터 확보이다. 



###### Regularization 

정규화는 모델 파라미터에 제약을 줌으로써 overfitting을 막는 개념이다. L2 regularization(Ridge regression)



weight decay는 너무큰 가중치 값에 대해서 제약을 줘서 정규성을 확보한다는 개념이다



**가중치 초기화** : weight값 작아야 하고 backprophagation가능해야 하고 unit 다양해야한다 

ex) xavier (unit개수에 맞춰서 초기화) , He 초기값 (Relu함수사용시)

그러나 GD의 특성때문에 local minimal 문제는 해결 할수가 없다. 









----

### optimizer 



SGD,Adam,Adamw, RMsprop등의 optimizer가 있다 



momentum(local minimum 벗어나서 global minimum찾을수있다)이라는 개념과 adaptive learning(각 weight파라미터에 대해 다른 learning rate를 적용한다는 의미이다)이라는 개념이 나온다. adaptive learning ragte는 각 가중치에 대해서 Gradient의 제곱을 계산하여서 루트 분모로 나타낸다 

앞서 batch normailzation할때도 moving average 개념이 나왔는데 이전 데이터와 현재 데이터의 비율을 보겠다는 개념이다. 

그래서 momentum개념과 adaptive learning개념이 같이 고려하는 **Adam optimizer**를 보면 

moving average를 통해 momentum계산하고 gradient descent의 제곱을 통해 각 가중치에 대한 학습률을 구할수있다. adaptive learning에도 moving average가 포함 되어있다. 



[Adam — PyTorch 2.2 documentation](https://pytorch.org/docs/stable/generated/torch.optim.Adam.html)

다음 링크에서 Adam의 수식을 확인할수가 있는데 모멘텀의 계산은 이전에 계산한 GD결과의 비율과 현재 계산된 GD결과의 비율을 줘서 momentum계산을 한다 즉 moving average가 적용된 momentum

Adaptive learning rate또한 moving average가 적용되어있는데 각 파라미터 변수의 GD^2의값을 계산하는 방식이다. 



##### RMSprop optimizer 

Adagrad 계산을 moving average사용하여 과거의 값 대신 현재의 값을 반영하는 방식이다. 



##### AdamW optimizer 



Adam에 적용하는 L2 regularization이 SGD보다 효과적이지 않다고 주장하며 제안된 개념이다 



**L2 regularization != Weight Decay**



기존  Adam에서는 L2 normalization한 것도 같이 미분해서 GD계산 했다면 AdamW에서는 L2에 대한 계산은 빼고 Loss만 고려 하는것이다. 







---------------



# CNN 및 기본 Network 



아래 pdf자료 정리 한 내용





[meang123/ModernConvNets: Revisions and implementations of modern Convolutional Neural Networks architectures in TensorFlow and Keras (github.com)](https://github.com/meang123/ModernConvNets)







-----



## Vision Transformer 



CNN으로 분류 하는 대신 transformer Encoder아키텍쳐를 이용해서 이미지 분류 하는 모델을 만든것이다 

(단, 데이터가 많을때 VIT성능이 좋다 데이터 양이 적으면 오히려 CNN보다 성능이 안좋게 나온다)



**colab link :** [vision_transformer.ipynb의 사본 - Colaboratory (google.com)](https://colab.research.google.com/drive/1KEF2iYiKGc0RIem68Sl7c-51fkC88VNa#scrollTo=KVVWmPso4eGf)





image data를 patch로 나눠서 transformer에 넣은 것이다 

m*m으로 patch를 나눈다 즉 input data로 BCHW를 정한 patch 사이즈 만큼 flatten하여서 넣는다 

위에 colab링크에서 그림 참고 하면 이해가 된다 



1. patch embedding
2. positional embedding
3. Add pos embedding + patch
4. Attention -> layer norm -> residual



### Swin Trnasformer 



VIT에서 patch크기는 16*16인데 이렇게 하면 작은 물체에 대해서 인식률이 낮다 

swin transformer는 patch사이즈를 줄인것이다 





hierarchical feature map : 

local attention 



[미완 아직 이해를 못했]



-----



### ConvNet

how do design decisions in Transformers impact Conv Net performance?

resnet 50을 tunning하면 VIT나 swin transformer보다 준하거나 높은 성능을 보여 줄수 있다는 내용이다 (adam w, more epoch ,Gelu,data augmentatioin...etc)

즉 다양하게 튜닝하는 방법에 대하여 소개 한것이다.

**MAE(masked autoencoders)**, **FCMAE**



[미완]









