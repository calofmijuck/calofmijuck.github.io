---
title: "github.io 사이트 설정 - 2"
categories: cse web
---

새해를 기념하여 글을 좀 더 열심히 작성하자는 생각에 이 사이트를 다시 방문했다.  
지난번에 남겨둔 해결해야 할 문제들을 다시 살펴보았고, 해결 할 수 있는 부분은 해결을 시도했다.

### 검색 결과가 발생하지 않는 문제
- 이 페이지를 검색하려고 검색에서 `사이트` 로 검색했는데 결과가 없음.

왠지 모르겠는데 다시 해보니까 아무 문제 없이 된다.
그런데 footer 쪽에 있는 related posts 에 들어있는 텍스트도 (즉, 해당 포스트에는 직접적으로 포함되지 않는 내용) 감지 되어 검색 결과에 같이 등장한다. 이게 뭐지?

### 상단 메뉴 별 pagination 적용 문제
- 상단 메뉴 선택시 해당 토픽의 최근 포스트를 보여줄 때 포스트 개수 제한 없이 모두 보여주어 스압 발생. (paginator 적용 안되어 있음)

사용하는 `plugin` 중 `jekyll-paginate` 를 더 이상 사용하지 않기로 하고, [`jekyll-paginate-v2`](https://github.com/sverrirs/jekyll-paginate-v2) 를 사용하기로 했다.

`_config.yml` 에 다음과 같은 내용을 추가했다.

```yml
plugins:
    - jekyll-paginate-v2

pagination:
    enabled: true
    per_page: 5     # 5개씩 보여주기
    limit: 0
    sort_field: "date"
    sort_reverse: true
    title: ':title'     # 타이틀 형식
```

그리고 `Gemfile` 에는 다음 내용을 추가했다.

```ruby
group :jekyll_plugins do
    gem "jekyll-paginate-v2"
```

당연히 `bundle install` 명령어를 한 번 입력해 줘야 하고, `index.html` 을 다음과 같이 변경했다.

```html
---
layout: home
author_profile: true
pagination:
    enabled: true
    per_page: 5
---
{% raw %}

{% for post in paginator.posts %}
  {% include archive-single.html %}
{% endfor %}

{% if paginator.total_pages > 1 %}
    <div class="pagination">
        {% if paginator.previous_page %}
            <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&laquo; Prev</a>
        {% else %}
            <span>&laquo; Prev</span>
        {% endif %}

        {% for page in (1..paginator.total_pages) %}
            {% if page == paginator.page %}
                <em>{{ page }}</em>

            {% elsif page == 1 %} 
                <a href="{{ '/index.html' | prepend: site.baseurl }}">{{ page }}</a>
            {% else %}
                <a href="{{ site.paginate_path | prepend: '/' | prepend: site.baseurl | replace: '//', '/' | replace: ':num', page }}">{{ page }}</a>     
            {% endif %}
        {% endfor %}

        {% if paginator.next_page %}
            <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Next &raquo;</a>
        {% else %}
            <span>Next &raquo;</span>
        {% endif %}
    </div>
{% endif %}
{% endraw %}
```

일단 당장은 디자인이 좀 구리다 (...)  
Bootstrap 이라도 이용해서 다시 고칠 생각을 하고 있다.

위와 같은 방식을 이용해서 category 별로 저 부분을 다 작성해서 넣어주면 pagination 이 잘 될 것이라고 기대하고 있다.

또 다른 문제를 하나 발견했는데...

### Category 가 많아지면 url 이 길어지는 문제
인지하지 못하고 있었는데, category 를 막 집어넣었더니 카테고리들이 `/` 로 분리되어 **전부** url 에 포함되는 것을 확인할 수 있었다. 일단은 임시 방편으로, permalink 를 `:path` 로만 해두었다.

```yml
permalink: /:path/
```

원하는 것은, `/대분류/:title/` 인데, collection 을 사용하면 될 것 같지만, 아직도 collection 은 잘 모르겠다.

아니면 태그를 잘 활용하는 것도 방법이 되지 않을까 고민하고 있다.


### TODO

- 상단의 Category 탭에서는 paginator 를 어떻게 적용해야 할지 전혀 모르겠다. 차라리 tag 를 도입해서 tag 가 같은 문서 끼리만 볼 수 있도록 구현을 하는 것이 방법일 것 같다.
- `_includes`, `_layouts` 에 뭐가 굉장히 많다. `liquid` syntax 를 익히고, template 들을 분석해서 사이트를 보다 더 다채롭게 사용할 수 있으면 좋겠다.


### 추가 내용

변경 사항들을 repo 에 모두 push 했는데, pagination 이 작동하지 않는다. 전체 recent post, CSE 카테고리 recent post 가 전부 보이지 않는다.