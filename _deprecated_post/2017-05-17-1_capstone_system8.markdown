---

layout: post
title: "(캡스톤) 캡스톤[5.17]"
category: PYTHON

---

### 오늘 할일(5월 17일)
> 오늘의 목표다. 두가지 질문에 답을 해야한다.
* Cosine similarity를 비교할 때 다차원에서 차원을 통일할 필요가 없는가?
* 만약 내가 평가 하지 않은 값과 상대가 평가한 값에대해 Cosine similarity를 구할 때 내 값을 0으로 두는게 맞는 것인가

<br/>
2. 만약 내가 평가 하지 않은 값과 상대가 평가한 값에대해 Cosine similarity를 구할 때 내 값을 0으로 두는게 맞는 것인가?
> A라는 사람이 a - 2.0 / b - 3.0 을 주었다. B라는 사람은 c - 2.0 / a - 3.0 을 주었다. 이때 Cosine similarity를 구할때 A사람이 c에 0점, B사람이 b에 0점을 주고 계산하는 것이 맞는것일까?

* 사실 이 고민은 이전에 Datamining 자료를 볼 때 공부했던 부분이다.[http://guidetodatamining.com/assets/guideChapters/DataMining-ch2.pdf](http://guidetodatamining.com/assets/guideChapters/DataMining-ch2.pdf)의 41페이지를 보면 이와 같은 고민을 한다.
* 수업시간에 내가 그냥 잘못알아서 잘못 대답한 것이었다. 0이 들어간 값은 cosine similarity를 구할 때 자동으로 걸러준다.
* 이 0으로 해줄 때 문제가 생기는 것은 Distance 형태의 similarity를 구해줄 때 문제가 된다. 하 대답을 잘못했다.

```python
def get_cosine_similarity(rating1, rating2):
    x = 0
    y = 0
    xy = 0
    for key in rating1:
        x += rating1[key] * rating1[key]
        if key in rating2:
            xy += rating2[key] * rating1[key]   # key가 하나라도 0이라면 반영이 안될 것.
    for key in rating2:
        y += rating2[key] * rating2[key]
    similarity = xy / (sqrt(x) * sqrt(y))
    return similarity
```

1. Cosine similarity를 구할 때 다차원에서 dimension을 통일할 필요가 있는가?
* 먼저 생각 해 볼만한것은 만약 통일을 시킨다고 했을 때다. 가장 많은 평가를 한 dimension으로 통일을 한다 치면 결국엔 0과 0을 계산하는 꼴이 된다.(의미가 없지)
* 어떻게 보면 0과 0을 계산하여 여러 similarity를 맞춰준다고 생각할 수도 있겠다.
* 그렇다면 가장 낮은 차원으로 낮춘다고 보자. 그게 의미가 있을까...
* 이걸 교수님에게 어떻게 설명할까, 예시를 들어보자


<br/><br/>
