---
title:  "github.io 사이트 설정"
categories: cse web
head:
    teaser: /assets/images/page-icon.png
---

사이트를 처음으로 설정하려는데 뭔가 어렵다.

그리고 뭔가 문제들이 몇 가지 보이는데 해결 방법을 몰라서 7시간 동안 삽질만 했다.

### 현재 해결해야할 문제들

- Category 별로 포스트를 보여주지만, 포스트의 개수가 많아질 경우 스압 발생.
- 상단 메뉴 선택시 해당 토픽의 최근 포스트를 보여줄 때 포스트 개수 제한 없이 모두 보여주어 스압 발생. (paginator 적용 안되어 있음)
- 이 페이지를 검색하려고 검색에서 `사이트` 로 검색했는데 결과가 없음.
- `collection` 을 어떻게 사용하는지 잘 모르겠다.
   - `collection` 을 사용해서 (Math/CSE/Life) 로 대분류를 나눠보려 했는데, 나누면 메인 화면의 최근 포스트에 다른 대분류가 잡히지 않음.
- ~~모바일에서 수식이 지나치게 긴 경우 수식만 튀어나오는 문제~~ (`overflow-x` property 로 해결)
- Preview Images 설정

[Minimal Mistakes Documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) 은 잘 되어있는 것 같은데, 그냥 내가 theme 을 잘못 고른건가 싶다.

### 지원되는 기능

일단 마크다운이기 때문에 기본적으로 될 것들은 다 되고... 그냥 심심하니 몇개 적어본다.

1. Syntax Highlighting

```c++
#include <stdio.h>
using namespace std;

int main() {
    printf("Hello, github.io!");
}
```

```python
print("Hello, github.io!");
```

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, github.io!");
    }
}
```

2. 수식 입력

$$
\vec{\nabla} \times \vec{F} =
            \left( \frac{\partial F_z}{\partial y} - \frac{\partial F_y}{\partial z} \right) \mathbf{i}
          + \left( \frac{\partial F_x}{\partial z} - \frac{\partial F_z}{\partial x} \right) \mathbf{j}
          + \left( \frac{\partial F_y}{\partial x} - \frac{\partial F_x}{\partial y} \right) \mathbf{k} 
$$

깔끔해서 마음이 편안해진다.

정리하자면 전체적으로 괜찮은 것 같긴 한데, **스압**이 가장 걱정된다. 느려지는 건 정말 원하지 않는다. (+ 모바일 데이터 폭탄 ~~무제한 쓰세요~~)

스압만 해결하면 적당히 쓸만한 사이트가 되지 않을까 싶다. 스압을 해결하려면 결국엔 이 테마에서 정의된 `layout` 들을 분석해야 할 것 같은데 Jekyll 로 되어있으니 Documentation 도 읽고 등등... 삽질 좀 더 해야 하나보다.

**더 편하게 코딩하자고 하는 삽질인데 그 과정이 무척 고통스러운 건 CSE 특징인 것 같다 ...**

남은 문제들은 미래의 나에게 맡긴다.