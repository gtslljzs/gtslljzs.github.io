---
sidebar:
    nav: "category"
title: "깃허브(Github) 블로그 만들기 #3"
excerpt: "블로그 구조와 Layout이 적용되는 과정"
categories:
    - ETC
permalink: /posts/ETC/making-blog-3
tags: [jekyll, github, blog]
toc: true
toc_sticky: true
comments: true
share: true
last_modified_at: 2019-07-17T15:00:00-10:00
---

[깃허브 블로그 만들기 #1](/posts/ETC/making-blog-1)<br>
[깃허브 블로그 만들기 #2](/posts/ETC/making-blog-2)<br>
**[깃허브 블로그 만들기 #3](/posts/ETC/making-blog-3)**

<br>
깃허브 블로그 만들기 세 번째 포스팅입니다. 이 포스팅은 블로그에 적용된 테마가 어떻게 적용되는지 전체적인 구조에 대한 포스팅입니다. 혹시 구조적인 내용에 대해 궁금하지 않으신 분들은 가볍게 건너 뛰시면 됩니다.

그 동안 이런 저런 일이 있어 지난 포스팅과 텀이 길어졌네요. 지난 두 번째 포스팅에서는 블로그를 개설하고 테마를 적용하는 방법까지 알아보았습니다. 사실 세 번째 포스팅으로 적용된 기본 테마를 커스터마이징 하는 방법과 포스트를 작성하는 방법 두 가지 중에 고민을 했지만, 조금 더 난해할 수 있는 커스터마이징 방법에 대해 작성하기로 했습니다.

## 1. 각 폴더와 파일들의 역할
커스터마이징에 대해 어떻게 설명을 해야할지 고민을 하다가 코드 하나하나의 수정 사항을 보여드리기보다는 전체적인 구조를 아시는 것이 우선일 것 같다고 생각해서 먼저 커스터마이징에 필요한 폴더와 파일들의 역할에 대해 제가 아는 범위 내에서 설명드리도록 하겠습니다. 제가 언급하지 않는 폴더와 파일들은 저 또한 사용한 적이 없고 기능을 알 수 없는 것들이기 때문에 양해 부탁드릴게요.

지난 포스팅까지 잘 따라오셨다면 현재 local repostiroy의 파일들은 다음과 같을 거에요.

![home](/assets/images/etc/home1.png)

폴더와 파일의 정렬 순서는 상이할 수 있으니 참고하시기 바랍니다.

### 1.1. assets

- ### css/main.scss
    **블로그 스킨, 폰트 등을 불러오는 파일**입니다.

- ### images/
    *images* 폴더가 없다면 만들어주도록 합시다. *images* 폴더에 **포스팅에 사용될 이미지들을 저장**하시면 됩니다. 사실 굳이 *assets/images*의 경로일 필요는 없다고 생각하지만, 저는 이 폴더에 이미지들을 저장하고 있습니다.

### 1.2. _data

- ### navigation.yml
    상단의 Quick-Start Guide와 같이 **메뉴와 카테고리를 만들고 주소를 할당하는 파일**입니다. 상단 메뉴 말고도 이 후에 본인이 좌측에 카테고리 메뉴를 만들었을    때에도 사용됩니다.

### 1.3. _include, _layouts, _sass
세 폴더를 한 번에 설명드리는 이유는 블로그 테마를 커스터마이징할 때 이 세 폴더 안에 있는 파일들이 서로 맞물려서 작동하기 때문입니다. 먼저 기본적인 역할만 언급한 후, 제일 마지막에 예시를 들어 추가적으로 설명하도록 하겠습니다.

- ### _include/
    ***_layout* 폴더 안의 각각 다른 파일들에서 사용될 공통적인 내용과 포멧이 담긴 파일들이 저장되는 폴더**입니다.

- ### _layouts/
    이름과 같이 **블로그 각 페이지의 layout과 포멧을 설정하는 파일들이 있는 폴더**입니다. 각 파일들은 한 페이지에 표시될 내용들의 구역을 구분해줍니다.

- ### _sass/
    *_layout* 폴더의 파일들이 페이지 내부의 구역을 구분해놓았다면, *_sass* 폴더의 파일들은 **구역 내에 담길 내용물의 위치나 간격 등 조금 더 세밀한 부분을 조정**해줍니다.

### 1.4. _pages
초기에 존재하지 않는 폴더입니다. 새로 만들어주도록 합시다. **블로그의 각 페이지에서 표시할 내용들이 담긴 파일을 저장하는 폴더**입니다. 예를 들어 제 블로그의 경우 상단의 About 페이지와 Posts 페이지를 눌렀을 때 뜨는 페이지 화면이 다릅니다. 이렇게 본인이 표시하고 싶은 페이지를 각각 파일에 저장해서 이 폴더에 저장하시면 됩니다.

### 1.5. _posts
초기에 존재하지 않는 폴더입니다. 새로 만들어주도록 합시다. 이름에서 알 수 있듯이 **블로그에 포스팅할 게시글을 작성하고 저장할 폴더**입니다.

### 1.6. _config.yml
**블로그 주소, 정보, 본인 프로필 등 기본적인 내용을 수정할 수 있는 파일**입니다. 실제 커스터마이징을 할 때, 가장 먼저 열어볼 파일입니다.

### 1.7. index.html
**블로그의 메인화면 즉, 루트 페이지의 layout을 정하는 파일**입니다. 따라서 다른 layout 파일들과는 달리 루트 디렉토리에 존재합니다. 제 블로그 같은 경우는 메뉴에 Home을 따로 두어 루트 페이지와 홈 페이지의 layout이 다르게 만들었습니다. 루트 페이지는 블로그 기본 주소와 동일합니다. 즉, username.github.io가 되겠죠.

## 2. 페이지 출력 구조
각 폴더를 먼저 열어보신 분들은 아시겠지만, *_include*, *_layouts* 폴더에는 html 파일들이 들어있고, *_sass* 폴더에는 scss파일들이 들어있습니다. 그리고 *_pages*와 *_posts* 폴더에는 md파일들이 저장됩니다. 간단하게 md 파일들이 페이지의 내용물이고 html 파일은 내용물을 담는 페이지의 layout을 만들고, scss 파일들이 이 layout의 세부적인 간격과 너비 등을 조정해준다고 생각하시면 됩니다..

제 블로그의 예시를 들어 전체적으로 한 페이지가 표시되는 과정을 설명하겠습니다.

먼저 제 블로그의 루트페이지에서 메뉴의 포스트를 클릭한다고 합시다. 그럼 포스트 페이지의 주소로 이동되면서 포스트 페이지가 화면에 뜨겠죠?

![root](/assets/images/etc/root.png)

이 때 시스템 내부적으로 보면 상단 메뉴의 내용이 클릭되었으므로 ***_data*/*navigation.yml*** 파일을 들여다봅시다. 제 *navigation.yml* 파일의 내부를 보면 다음과 같은데 Posts 메뉴의 주소는 /posts/로 되어있습니다.

![navi](/assets/images/etc/navi.png)

그 다음 ***_pages*** 폴더에서 /posts/라는 주소가 저장된 md파일을 훑어봅시다. 모든 md파일에는 **YAML Front Matter**라고 해서 내용 이외에 페이지가 참조할 몇 가지 정보들을 저장해 놓는데, 저는 /posts.md 파일에 다음과같이 저장을 해놓았습니다.

![post_md](/assets/images/etc/post_md.png)

**permalink: /posts/** 라 되어있는 부분이 이 md파일이 Posts 페이지의 내용물이라는 것을 말해줍니다. 그럼 이제 layout을 불러와야겠죠. 위에서 볼 수 있듯 **layout: leaderboard**라고 명시해놓았습니다. 그럼 다시 ***_layouts*/*leaderboard.html*** 파일을 봅시다.

![learderboard](/assets/images/etc/leaderboard.png)

leaderboard 파일에서도 **layout: archive**라고 명시해주었습니다. 그리고 아래에 보면 **include leaderboard-single.html**이라는 코드도 있습니다. include leaderboard-single.html이라는 것은 leaderboard.html이 구분하는 구역 중 저 부분에 leaderboard-single.html의 내용을 집어넣겠다는 의미입니다. 다음으로 명시된 **_layout/archive.html** 파일을 봅시다.

![archive](/assets/images/etc/archive.png)

archive.html 파일도 default라는 layout을 쓰겠다고 명시해놓았네요. 그리고 아래를 보시면 leaderboard.html 파일에서 봤던 것처럼 여러 개의 include 문이 존재하고 있습니다. 그리고 제일 아래에 **"content"** 라는 부분도 보이는데, 아까 leaderboard.html 파일이 archive 파일을 layout으로 명시해놓았죠? 따라서, **archive.html 파일의 "content" 부분에 leaderboard.html 파일의 내용이 들어가게 됩니다**. 그럼 동일하게 default.html 파일에도 "content" 라는 부분이 존재할 것이고 그 곳에 archive.html 파일의 내용이 들어가게 되겠네요. default.html 파일의 내용은 생략하도록 하겠습니다.

위에서 각 폴더와 파일의 역할을 설명드릴 때, *_layout* 폴더의 파일들은 큰 구역만을 구분한다고 했죠?

위 사진에서

    <div id="main" role="main">
        <div class="archive">
            <h1 id="page-title"> ... </h1>
        </div>
    </div>

부분이 보이시나요? 이 코드가 각 구역들을 구분하는 코드입니다. 그리고 이렇게 구분된 구역 내부를 조정하려면 scss파일을 봐야겠죠. 어떤 파일을 수정할지 모르시겠다면 일단은 div 혹은 h1같은 구분자 뒤에 있는 **class=** 이나 **id=** 부분을 봅시다. **archive**와 **page-title**이 있는데 아마도 저런 이름을 가진 파일이라고 추측할 수 있습니다.

***_sass/minimal-mistakes/*** 로 가시면 하위 파일들 중 ***_archive.scss*** 파일과  ***_page.scss*** 파일이 있네요. 두 파일을 열어서 쭉 훑어보시면 ***_archive.scss*** 파일에는 **.archive {...}** 함수가 있고, ***_page.scss*** 파일에는 **.page__title {...}** 함수가 있습니다. 이 함수 내부의 바디를 수정하시면 layout을 조금 더 세부적으로 수정할 수 있습니다.

***_scss/minimal-mistakes/_archive.scss***
![.archive](/assets/images/etc/archive_code1.png)

***_scss/minimal-mistakes/_page.scss***
![page_title](/assets/images/etc/page__title.png)


각 구역이 어느 파일에 있는지 도저히 모르시겠다면, 웹 브라우저 페이지에서 **f12** (크롬 기준) 버튼을 누르시면 소스코드가 뜰 거에요. 이 소스코드를 활용하시면 커스터마이징 하는데에 훨씬 도움이 될 거에요.

일단, 오늘은 실제 커스터마이징에 앞서 각 파일들이 어떻게 구조적으로 연결되어 있는지 알아보았고, 사실은 이번 포스팅에서 실제 커스터마이징까지 진행하려 했으나 글이 너무 길어지는 바람에 다음 포스팅에서 이어가도록 하겠습니다.
