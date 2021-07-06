## [📔 L2_Supervised multi-task learning, transfer learning]
✓ [lecture video](https://youtu.be/6stKGH6zI8g)


#### Multi-task classification vs. Multi-label learning
> '**Task**' Definition: <img src="https://user-images.githubusercontent.com/33504288/124423334-dfd8d480-dd9f-11eb-862b-45f6ef9d8db6.png" width="200" height="30">
> > **p(x)**: input의 distribution, **p(y|x)**: x의 label distribution, **L**: loss
> 
> - **Multi-task classification**: 모든 task의 loss function(**L**)이 같음 (e.g. per-language handwriting recognition)
> - **Multi-label learning**: 모든 task의 loss function(**L**)과 input data(**p(x)**)가 같음 (e.g. scene understanding)

> 그럼 loss function이 같은 경우는?
> <br>: 이산/연속 label이 섞여있을 때, 다른 task보다 특정 task 하나에 더 집중할 때

<br>

#### Basic Structure & Task Descriptor
 <img src="https://user-images.githubusercontent.com/33504288/124550449-9e156000-de6b-11eb-8f9c-d46bb4e73b0e.png" width="480" height="220"> <img src="https://user-images.githubusercontent.com/33504288/124551325-eaad6b00-de6c-11eb-87a9-2fe201f71e0d.png" width="200" height="60">


> - Basic structure: input x와 **task descriptor인 Zi**가 같이 주어짐
> > **task descriptor**란?<br>
> > : 단순히 task index를 one-hot encoding한 것<br>
> > : 또는! **meta data**를 제공하는 것 (e.g. personalization(user features/attributes), language description of the task, formal specifications of the task)
> <br>
> 💡 자, 그럼 Multi-task learning에서 우리의 목표는 두 가지!<br>
> Q1. task descriptor Zi를 어떻게 conditioning 할 것인가?<br>
> Q2. objective를 어떻게 optimize할 것인가?

<br>

#### Conditioning
> 'How to condition on Zi'  ==  'How & Where to share parameters'
> 전체 parameter(θ)를 shared parameter(θsh)와 task-specific parameter(θi)로 나누자!<br>
> objective: <img src="https://user-images.githubusercontent.com/33504288/124554096-88566980-de70-11eb-8c45-725e91adb10d.png" width="200" height="60">
> > **shared parameter**: network에서 task descriptor 바로 뒤에 오는 parameter

> - **Conditioning 종류** <br>
> *여기서 task descriptor는 one-hot encoding vector* <br>
> <img src="https://user-images.githubusercontent.com/33504288/124559853-1df4f780-de77-11eb-8b71-9dc315f96585.png" width="750" height="150"> <br>
> > But, 두 방법은 사실 같다는 점...! <br>
> > <img src="https://user-images.githubusercontent.com/33504288/124558210-51368700-de75-11eb-8aa7-0b8d320bcc3c.png" width="320" height="150"> <br>
> 
> <img src="https://user-images.githubusercontent.com/33504288/124560095-66acb080-de77-11eb-838c-8103401a8410.png" width="650" height="180"> <br>
> 
> 안타깝게도 이런 방법들은 **problem dependent**하고, 문제에 대한 **intuition이나 지식**에 largely guided 됨

<br>

#### Challenges in Multi-task learning
> - **Negative transfer**: independent network가 성능이 더 좋은 경우
> > '**optimization challenges**' & '**limited representational capacity**'때문! <br>
> > : 한 task에 대한 gradient가 다른 task의 gradient 때문에 변한다거나, 각 task가 다른 비율(속도)로 학습하는 경우
> 
> negative transfer가 발생했을 때, task 간의 **share를 줄이자**! <br>
> <img src="https://user-images.githubusercontent.com/33504288/124566083-ad9da480-de7d-11eb-9dbe-5e30c817b693.png" width="240" height="70"> <br>
> 'soft parameter sharing' term: 서로 다른 task의 task-specific parameter를 비슷하게 만들어줌 
> > 👍🏻 결과적으로 더 많은 양의 parameter sharing이 가능해짐! <br>
> > 👎🏻 이건 또 다른 design decisions/hyperparameter이 됨... <br>

> - **Overffiting**
> > 덜 share해서 발생 => **더 share**하면 됨!

<br>

#### + Case study: [Make recommendations for YouTube](https://dl.acm.org/doi/pdf/10.1145/3298689.3346997?casa_token=5I-bu7KVMXkAAAAA:rZiBs9D3FrXAUzL3E11jcegSnScsc_lGLb8m9WSIiNLDqZ7kBrhw5ILECWQJ-zPxZmRhlqtgpZN1)
______
#### Meta-Learning
> - **Mechanistic** view
> > : network 모델이 전체 dataset 읽고, training에 meta-dataset(각기 다른 task에 대한 여러 dataset으로 구성) 사용 <br>
> > 🌟 이 관점은 meta-learning algo를 수월하게 실험하도록 함!
> 
> - **Probabilistic** view
> > : set of task에서 사전정보를 추출하고, 이 사전정보와 (small) training set을 사용해서 사후 parameter 추론 <br>
> > 🌟 이 관점은 meta-learning algo를 수월하게 이해하도록 함!

<br>

#### Problem definition
  <img src="https://user-images.githubusercontent.com/33504288/124573939-f60c9080-de84-11eb-982b-b0269c369fed.png" width="550" height="200">

> 💡 이 때, dataset이 작다면...? **additional data**를(meta-train data) 추가할 순 없을까? <br>
> <img src="https://user-images.githubusercontent.com/33504288/124576012-dd9d7580-de86-11eb-917d-b7f2013159c1.png" width="480" height="240">

> 근데, new task를 학습할 때마다 prior information을 쓰고 싶진 않은데... <br>
> 💡 그럼 meta-train data를 **meta-parameter**로 바꾸자!
> <img src="https://user-images.githubusercontent.com/33504288/124577646-6d8fef00-de88-11eb-972e-95d313ea54de.png" width="700" height="180"> <br>
> - meta-training data로 meta-parameter를 구하고, data와 meta-parameter로 task-parameter를 예측함
> > 이 때, task-parameter와 meta-train data는 조건부 독립, meta-parameter 기반
>
> 위 식은 (아주 대략적인 근사치지만)<img src="https://user-images.githubusercontent.com/33504288/124602391-c15c0180-dea3-11eb-9138-0ef24025b2a5.png" width="210" height="20">로 표현 가능
> > 오른쪽 term: **meta-training**과 대응(주어진 meta-training data에서 set of meta-parameters를 학습하는 것이 목표) <br>
> > 왼쪽 term: **adaptation**과 대응(새 task의 data와 meta-parameter가 주어졌을 때, 새 task를 위한 새 parameter를 학습하는 것이 목표)


> 이해를 위한 simple example <br>
> <img src="https://user-images.githubusercontent.com/33504288/124606137-8d82db00-dea7-11eb-9b29-4e3ba1400df7.png" width="550" height="250"> <br>
> - **test**: test datapoint에 대한 prediction을 위해 Φ* 를 예측
> > 이 걸 meta-training에서도 똑같이 하고 싶으시다는 거지~ (위의 RNN을 train시켜서) <br>
> > adaptation: (meta)test-time으로 볼 수 있음(meta-train이 선행된다면)
> 
> - 그럼 (meta)training-time 때 쓰이는 **test datapoints**들은 어디서 오는 거...?
> > training/test set은 meta-training dataset에서! <br>
> > 그리고 meta test-time에는 새 task를 받겠죠!(meta-test set으로 train하기 시렁)
>
> ♨️ 여기서의 key idea(principal rule of mata-learning)<br>
> : **test and train conditions must match**
> > test 때 학습할 수 있게 하려면, meta-learning 중에 학습할 수 있게 해야 한다는 말!(**learning how to learn**)

❤️ 결론: θ(meta-parameter)가 task들에 걸쳐 shared된 prior information이다! parameter θ* 를 가진 model을 학습해서 여러 task들을 해결하자!
