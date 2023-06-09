# 1. MLP란?

  MLP 란 여러 개의 퍼셉트론 뉴런을 여러 층으로 쌓은 다층신경망 구조

입력층과 출력층 사이에 하나 이상의 은닉층을 가지고 있는 신경망이다.

인접한 두 층의 뉴런간에는 완전 연결 => fully connected 된다.

# 2. MLP의 필요성?

  복잡한 패턴 분류를 위해서는 입출력 간의 복잡한 변환 구조가 필요하다. 사용하는 뉴런의 수를 늘리고 층을 추가하여 복잡한 구조의 의사결정 경계를 생성할 수 있다. 단일뉴런 ( 퍼셉트론)으로는 선형분리 가능한 경계선만 생성가능하다. 

두개의 뉴런을 결합함으로써 XOR 과 같은 비선형 분리가 가능한 결정선을 생성할 수 있다. 뉴런을 추가함으로써 다각형 모양의 경계선을 생성할 수 있다. => 복잡한 데이터의 분류가 가능해진다!  , 일반적으로 다층 신경망은 (MLP 는) 2-3 개 계층으로 구성된다. 

# 3. MLP의 구조 : 입력층(데이터셋), 은닉층(하나이상), 출력층(결과)의 전방향 신경망이다.

검정색이나 희색 이미지을 이용해서 강아지나 고양이를 분류하는 케이스를 생각해보자. (다중분류)

이미지에 무엇이 있는지 알아내기 위해서는 입력과 출력 간의 매우 복잡한 관계와 이를 위해서는 패턴이 많은 특성(feature)들 사이의 관계를 통해서 특정 지어지는 가능성을 고려해야한다. 이런 경우에는, 선형 모델의 정확도는 낮을 것이다. 모든 입력값과 레이블의 관계가 꼭 선형적일 수 없기 때문이다.

우리는 한 개 이상의 은닉층(hidden layer)을 함께 사용해서 더 일반적인 함수들을 이용한 모델을 만들 수 있다. 이를 구현하는 가장 쉬운 방법은 각 층 위에 다른 층들을 쌓는 것이다.

각 층의 결과는 그 위의 층의 입력으로 연결되는데, 이는 마지막 출력층까지 반복된다. 이런 아키텍쳐는 일반적으로 “다층 퍼셉트론(multilayer perceptron)”이라고 불린다. 즉, MLP는 여러 층를 연속해서 쌓아올린다.

입력이 4개, 출력이 3개, 중간의 은닉층(hidden layer)은 5개의 은닉 유닛(hidden unit)이 있는 다층 퍼셉트론(multilayer perceptron) 를 생각해보자.

입력층은 어떤 연산을 수행하지 않기 때문에, 이 다층 퍼셉트론(multilayer perceptron)은 총 2개의 층(layer)을 갖는다고 말한다. 은닉층(hidden layer)의 뉴런(neuron)들은 입력층의 입력들과 모두 연결되어 있다. 출력층(output layer)의 뉴런과 은닉층의 뉴런들도 모두 연결되어 있다. 따라서, 이 다층 퍼셉트론의 은닉층과 출력층은 모두 완전 연결층(fully connected layer)이다.

모든층에 비선형함수σ를 추가함으로써 MLP로 만들 수 있다. 이 과정이 빠지면 층끼리 합쳐져서 단일 퍼셉트론으로 표현되어버린다. 모든층에 σ를 추가하는 것이 층을 쌓을 수 있게 하고 여러 은닉층을 쌓는 것을 가능하게 한다. -> 선형에서 비선형으로의 변환

h=σ(W1x+b1)

o=W2h+b2

y-hat=softmax(o)

# 4. 활성화 함수란?

  퍼셉트론에서는 step 함수 (계단 함수) 를 활성화 함수로 사용, MLP 에는 다양한 비선형 함수들을 활성화 함수로 사용한다.

인공 신경망을 통과해 온 값을 최종적으로 어떤 값으로 만들지 결정하는 함수라고 볼 수 있다.

1) step function : 임계값을 미리 설정하고 (threshold value) 임계값 보다 크면 1, 아니면 0

2) Sigmoid fuction : [0,1] 사이의 값

3) Linear function : y =x 

4) tanh function : [-1, 1] 사이의 값

5) ReLu function : 양수이면 그대로 , 음수이면 0 

6) Leaky ReLU 

7) ELU

# 5. 손실 함수 : 전체 오차는 목표 출력값에서 실제 출력값을 빼서 제곱한 값을 모든 출력 노드에 대하여 합한 값이다 => 평균제곱법(MSE) 

# 6. 역전파 알고리즘 (EBP : Error BackPropagation) : 입력이 주어지면 순방향으로 계산하여 출력을 계산한 후에 실제 출력과 우리가 원하는 출력 간의 오차를 계산한다. 오차를 역방향으로 전파하면서 오차를 줄이는 방향으로 가중치를 변경한다. 

역전파(back propagation)는 뉴럴 네트워크의 파라미터들에 대한 그래디언트(gradient)를 계산하는 방법을 의미한다.

일반적으로는 역전파(back propagation)은 뉴럴 네트워크의 각 층과 관련된 목적 함수(objective function)의 중간 변수들과 파라미터들의 그래디언트(gradient)를 출력층에서 입력층 순으로 계산하고 저장한다. 이는 미적분의 ’체인룰(chain rule)’을 따르기 때문이다.

임의의 모양을 갖는 입력과 출력 텐서(tensor) X,Y,Z 들을 이용해서 함수 Y=f(X) 와 Z=g(Y)=g∘f(X) 를 정의했다고 가정하고, 체인룰(chain rule)을 사용하면, X 에 대한 Z 의 미분은 다음과 같이 정의된다.

∂Z∂X=prod(∂Z∂Y,∂Y∂X).

하나의 은닉층(hidden layer)를 갖는 간단한 네트워크의 파라매터는 W(1)와 W(2) 이고, 역전파(back propagation)는 미분값 ∂J/∂W(1)와 ∂J/∂W(2) 를 계산하는 것이다.

이를 위해서 우리는 체인룰(chain rule)을 적용해서 각 중간 변수와 파라미터에 대한 그래디언트(gradient)를 계산한다. 연산 그래프의 결과로부터 시작해서 파라미터들에 대한 그래디언트(gradient)를 계산해야하기 때문에, 순전파(forward propagation)와는 반대 방향으로 연산을 수행한다. 

 

# 7. 구현방법 

Activation function = 활성화 함수는 ReLU(x)=max(x,0)를 사용하고 만족스럽지 않으면 LeakyReLU, ELU 를 사용한다.

 

그래도 만족스럽지 않다면 tanh 를 사용 , Deep learning 에서 Sigmoid 는 사용하지 말자 (Sigmoid 는 MLP 까지만!) 

실무적으로는 ReLU 를 가장 많이 사용한다. ReLU를 사용하는 이유는 값이 사라지거나 그대로 전달하게 하는 식으로 미분이 아주 잘 작동하기 때문이다. 이러한 특징으로 인해 최적화가 더 잘 되고,  vanishing gradient 문제를 줄여주게된다. LeakyReLU/ELU 도 괜찮다. 

텐서플로우를 이용한 신경망 모델 구성방법 세가지

Sequential Model : 주로 이걸로 코딩할 것이다. 아주 쉽고, 1개입력과 1개출력으로 계속 처리한다. 70%의 경우 적용이 가능하다. 입력층에서 부터 차곡차곡 쌓기가 가능한하다. 사용법 : tf.keas.Sequential 
Functional API : 다중입력 , 다중출력 등으로 처리 , 95% 의 경우에 적용 가능 , 사용방법 : model=tf.keras.Input, Model 
Model 서브클래스: 가장 유연하게 사용할 수 있지만 어렵고 복잡하다.
