다른 모델의 repository
- https://github.com/hyunwook990/vision_model_practice.git
---
# AlexNet 구현

- 문제 1: x1, x2로 병렬처리를 따라한 것은 구현, 그러나 세번째 레이어에서 두 output을 모두 input으로 받는 것을 어떻게 구현해야할 지 모르겠다...
- 해결법: 병렬처리로 하는 x1, x2 그리고 병렬처리를 하지 않는 x도 가져가야한다.
- 궁금증: conv_layer를 통과할때 항상 같은 특징을 가져가는 것인가?

### 변경점
- 2025.04.14
    - 병렬 GPU를 구현하고 싶었으나 3번째 conv_layer에서 교차로 각각의 GPU에 들어갈 때 다른 가중치를 연산하여 들어가는 것이 아니라 같은 가중치로 연산하여 각각의 input으로 들어가서 torch에서는 alexnet의 구현이 어렵다고 한다. (현재의 나의 실력으로 부족하다는 것 같다.)
    - 따라서 alexnet은 코드로 구현하는 방법을 익히는 것에 집중하기로 했다.

### 문제점
- 2025-04-14
    1. softmax를 언제 사용해야 하는지, 3번째 fc_layer를 어떻게 구현해야 하는지
    2. drop_out을 1, 2번째 fc_layer에 적용해야 하는데 어느 지점에 넣어줘야 하는지
    3. drop_out을 하게되면 output의 개수에도 영향이 가서 다음 layer의 input을 조정해줘야하는지
    4.  x = nn.Flatten(x)
        x = x.flatten()
        x = x.view(-1, 6*6*256)
        이 세가지가 모두 같은 기능을 하는지, 차이점이 있다면 무엇인지

### 수정
- 2025-04-14
    - 정규화 후에 ReLU를 거쳐야하는데 반대로 진행하여 수정함.

---
# Custom Model
### 2025-04-16
- AlexNet 구현을 시도했으나 아직 모델 구현에 대한 이해도가 부족하여 custom model을 구현하며 모델 구조의 이해도를 높이기위해 custom model 구현을 시작
