### [📔 L1_Coures_Introduction]

#### robot(agents)가 real world의 skill을 배우게 하자!
> _Q. 왜 하필 robot?_ 
> <br>_A. Robots can teach us things about intelligence!_
> - faced with the __real world__
> - robot must __generalize__ across tasks, objects, environments, etc
> - need some __common sense understanding__ to do well
> - __supervision__ can't be taken for granted

> ⚠️ BUT! 하나의 task에 대해 하나의 environment에서 reinforcement learning을 하는 것은,
> > ==> __detail한 supervision과 guidance에 의존__ 
> <br>(machine translation, speech recognition, object detection에도 해당되는 문제...)
> <br> 이 경우를 **specialists**라고 부름(<-> Human은 **generalists**)

<br>

#### 왜 deep multi-task & meta learning을 배워야 하죠?
> 그 전에, deep learning의 benefit을 보자면,
> - domain knowledge가 적고, hand-engineering feature가 없어도 unstructured input을 처리할 수 있고
> - 성능도 좋아요~!
> <br>😥 단, large/diverse data가 있을 때만...!

> 그럼 **적은 data**만 있다면...?
> <br>prior experience로 new data를 빠르게 학습해보자! (e.g. few-shot learning)

<br>

#### multi-task learning, 이럴 때 사용하세요!
> - AI system이 더 **general-purpose** 하면 좋겠다
> - dataset이 **적다**
> - data가 **long tail**이다
> - **빨리 new data를 학습**하고 싶다

<br>

#### multi-task가 뭔데요?
> **'task'**: dataset과 loss function이 주어졌을 때, model을 optimize 하는 것
> <br>이 때 objects, people, objectives, lighting conditions, words, languages에 따라 different task가 다양해질 수 있음
> > ==> 일반적으로 우리가 생각하는 **task**뿐만 아니라 결과에 영향을 미치는 다른 요소(task)들이 많다!

> 하지만 여기엔 **critical assumption**이 존재하는데...
> > 🙅🏻‍♀️ [Bad News]
> > <br>: 이러한 알고리즘의 benefit을 받으려면, 각기 다른 task들이 some structure를 share 해야 함ㅠ
> > <br><br>🙆🏻‍♀️ [Good News]
> > <br>:  다행히도 꽤 많은 task들이 shared structure를 가지고 있음! (e.g. 잼 뚜껑 돌리기, 물병 뚜껑 돌리기, etc)

<br>

#### Problem Definition(informal ver.)
> ☑ **[Multi-task learning problem]**
> <br>: 모든 task들을 각각 학습하는 것보다 더 빠르고 능숙하게 학습하자!
> <br><br>☑ **[Meta learning problem]**
> <br>: previous task에 대한 data/experience를 바탕으로, new task를 더 빠르고 능숙하게 학습하자!(learning to learn)

<br>

#### 그럼 Multi-task learning을 Single-task로 볼 수 있지 않나요?
> 네! (모든 dataset들을 하나의 dataset으로 보고, 모든 loss function들을 하나의 loss function으로 본다면)
> <br>이 때 data가 각기 다른 tasks에서 왔다는 것을 알고, 이 사실을 이용하는 것이 성능을 더 좋게 한답니다~!

<br>

#### 자, 그럼 지금 Multi-task & Meta learning을 배워야 하는 이유는?
> 사실 Multi-task & Meta learning에 대해서는 오래 전부터 연구가 진행되어 왔으나...
> - **powerful한 neural network function approximator**가 출현한 이 시점에서는 더 중요!(+ computing power)
> - 통계적으로, machine learning research에 있어 이러한 알고리즘들이 점점 더 많은 역할을 함
> > 이전에 deep learning이 크게 발전함! 단, **실현 불가능한 정도의 광범위한 setting**에서... (e.g. 1.2백만 image와 label들, 40.8백만 paired sentences, etc)
> > <br><br>🌟 medical image처럼 **data가 적은 domain**에서도 **deep learning이 성공적으로 적용**되기 위해서는 Multi-task & Meta learning이 아주 중요하다!
> > <br>e.g.
> > - 간질 치료에서의 reinforcement learning: 1시간이 채 되지 않는 data
> > - robotic manipulation: 15분 이하의 data
> - 그리고, 아직 이 분야의 풀리지 않은 문제가 많기 때문에 재밌을 것(?)이다~
