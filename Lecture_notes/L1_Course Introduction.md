### [📔 L1_Coures_Introduction]

#### robot(agents)가 real world의 skill을 배우게 하자!
> _Q. 왜 하필 robot?_ 
> <br>_A. Robots can teach us things about intelligence!_
> - faced with the __real world__
> - robot must __generalize__ across tasks, objects, environments, etc
> - need some __common sense understanding__ to do well
> - __supervision__ can't be taken for granted

> ⚠️ BUT! 하나의 task에 대해 하나의 environment에서 reinforcement learning 
> > ==> __detail한 supervision과 guidance에 의존__ 
> <br>(machine translation, speech recognition, object detection에도 해당되는 문제...)
> <br> 이 경우를 **specialists**라고 부름(<-> Human은 **generalists**)

<br>

#### 왜 deep multi-task & meta learning을 배워야 하죠?
> 그 전에, deep learning의 benefit을 보자면,
> - domain knowledge가 적고, hand-engineering feature가 없어도 unstructured input을 처리할 수 있고
> - 성능도 좋아요~!
> <br>😥 단, large/diverse data가 있을 때만...!

> 그럼 적은 data만 있다면...?
> <br>prior experience로 new data를 빠르게 학습해보자! (e.g. few-shot learning)

<br>

#### multi-task learning, 이럴 때 사용하세요!
> - AI system이 더 general-purpose 하면 좋겠다
> - dataset이 적다
> - data가 long tail이다
> - 빨리 new data를 학습하고 싶다

<br>

#### multi-task가 뭔데요?
> objects, people, objectives, lighting conditions, words,languages에 따라 different task가 다양해질 수 있음
> > ==> 일반적으로 우리가 생각하는 **task**뿐만 아니라 결과에 영향을 미치는 다른 요소(task)들이 많다!
> 
