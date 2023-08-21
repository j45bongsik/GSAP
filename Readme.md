# 퍼블리싱 환경 (Gulp) 가이드

node js : 14.16.1v<br>
gulp : 2.3.0v<br>
jQuery : 3.1.1v<br><br>

## 로컬호스트 실행

gulp 세팅파일 zip파일로 다운로드 (클론 X)<br>
※ 클론하면 작업하고 push 할 경우 최초 다운로드한 레포지터리로 덮어쓰게 됨

<br>
압축해제 > IDE에서 해당 PJT 폴더열기 > 터미널 > 디렉토리 pre-build 이동 > npm install <br>

<br><br>

pre-build폴더 하위에 node_modules 폴더 생겼으면,
<br>
터미널 pre-build경로에서 gulp 입력!

<br><br>


### 자주 쓰는 라이브러리 목록

- [Swiper api](https://swiperjs.com/swiper-api)
- [Aos.js](https://github.com/michalsnik/aos)
- [jQuery ui Docs](https://api.jqueryui.com/)
- [jqGrid](http://trirand.com/blog/jqgrid/jqgrid.html)
- [RealGrid2](https://docs.realgrid.com/start/overview)
- [mScroll](https://manos.malihu.gr/jquery-custom-content-scroller/)
- [clipboard.js](https://clipboardjs.com/)
- [fullPage.js](https://github.com/alvarotrigo/fullPage.js/)
- [jQuery multisortable](https://github.com/shvetsgroup/jquery.multisortable)
- [jQuery splitter](https://github.com/jcubic/jquery.splitter)
- [jQuery easeScroll](https://creativestudio.kr/2113)<br>
**easeScroll 라이브러리 자체 코드 이슈가 있어서 아래 코드로 대체**<br>
[💡 코드 보기](/pre-build/easeScroll.md)

<br>

## 작업폴더 구조 (pre-build)

📦pre-build<br>
 ┣ 📂html<br>
 ┃ ┣ 📂include<br>
 ┃ ┃ ┣ 📜footer.html<br>
 ┃ ┃ ┣ 📜head.html<br>
 ┃ ┃ ┗ 📜header.html<br>
 ┃ ┣ 📜00_coding_list.html<br>
 ┃ ┗ 📜index.html<br>
 ┣ 📂images<br>
 ┣ 📂js<br>
 ┃ ┗ 📜ui.js<br>
 ┣ 📂node_modules<br>
 ┃ ┣ 📜...<br>
 ┣ 📂scss<br>
 ┃ ┣ 📜_mixins.scss<br>
 ┃ ┣ 📜common.scss<br>
 ┃ ┣ 📜components.scss<br>
 ┃ ┣ 📜fonts.scss<br>
 ┃ ┣ 📜hover.scss<br>
 ┃ ┣ 📜reset.scss<br>
 ┣ 📜.babelrc<br>
 ┣ 📜gulpfile.js<br>
 ┣ 📜package-lock.json<br>
 ┣ 📜package.json<br>
 ┗ 📜Readme.md<br>

<br>

- html폴더 : HTML 파일을 모아둔 폴더입니다. 페이지가 추가되면 쉽게 볼 수 있게 반드시 `00_coding_list.html` 에 추가해야합니다.

- include폴더 : 헤더나 푸터처럼 공통된 요소들을 담아둔 폴더입니다. <br> 폴더 안에 html을 작성 후 불러올 html 파일 자리에서 아래와 같이 선언해주면 됩니다.


    ```html
        @@include('include/header.html')
    ```

<br>

- images폴더 : 페이지에 사용되는 아이콘이나 이미지를 모아둔 폴더입니다.<br>
작성자 마다 구분이 다를수 있습니다. 일반적으로 bg_ / ico_ / img_ / logo_ 나누어 집니다.

<br>

- js폴더 : js 파일을 모아둔 폴더입니다. 

    - ui.js : UI 제어에 사용되는 코드만 작성합니다.
    <!-- - a11y.js : 접근성 제어에 사용되는 코드만 작성합니다. -->

<br>

- scss폴더 : scss 파일을 모아둔 폴더입니다.
(파일 명 앞에 언더바가 붙은 파일은 따로 build되지 않습니다.)
<!-- 
    - _function.scss : scss 설정 파일입니다.

    <br>

    ```scss
    $html-font-size: 16px;

    @function stripUnit($value) {
        @return $value / ($value * 0 + 1);
    }

    @function rem($pxValue) {
        @return #{stripUnit($pxValue) / stripUnit($html-font-size)}rem;
    }
    ```
    html 기본 폰트 사이즈를 16px로 설정하고, px 단위를 rem으로 변환 시켜주는 함수입니다. 반응형 프로젝트가 아니라면 px로 사용해도 무방합니다.

    사용은 다음과 같이 할 수 있습니다.

    ```scss
        .text{font-size: rem(16px);}

        /* => 적용 : 1rem */
    ```
 -->
<br><br>

- _mixins.scss : scss mixin을 모아둔 파일입니다.
아래는 font mixin을 사용한 예시이며, mixin은 작업자 편의에 따라 추가될 수도 있습니다.

    ```scss
        .test {@include font(16px, 'Noto Sans', #000);}
    ```

<br><br>
<!-- 
    - button.scss : 버튼 스타일만 모아둔 파일입니다.
 -->
- common.scss : header, gnb, lnb, aside, footer 등 공통된 요소들의 스타일을 모아둔 파일 입니다.

- component.scss : wrapper,container,box,card 같은 레이아웃을 구성하는 요소들의 스타일을 모아둔 파일입니다.

- fonts.scss : font 들을 모아둔 파일입니다.

- hover.scss : hover 되었을때 스타일을 모아둔 파일입니다.

    ```css
        @media (hover:hover){

        }
    ```

위 미디어쿼리 hover 구문은 PC에서만 호버 스타일을 적용하고 모바일은 적용하고 싶지 않을 때 사용합니다. 반응형 프로젝트가 아니라면 사용 할 필요가 없습니다.

<br>

<!-- - mobile.scss : 반응형 처리 스타일들을 모아둔 파일입니다. -->
- reset.scss : css 스타일 초기화 코드 및 공통으로 사용되는 클래스들을 모아둔 파일입니다.

- gulpfile.js : gulp 설정 파일입니다. 웬만해선 수정하거나 건드릴 일은 없습니다.

<br><br>

## 배포폴더 구조 (build)

📦build<br>
 ┣ 📂css<br>
 ┃ ┣ 📂font<br>
 ┃ ┃ ┣ 📂notoSans<br>
 ┃ ┃ ┃ ┣ 📂eot<br>
 ┃ ┃ ┃ ┃ ┣ 📜...<br>
 ┃ ┃ ┃ ┣ 📂otf<br>
 ┃ ┃ ┃ ┃ ┣ 📜...<br>
 ┃ ┃ ┃ ┗ 📂woff<br>
 ┃ ┃ ┃ ┃ ┣ 📜...<br>
 ┃ ┣ 📜common.css<br>
 ┃ ┣ 📜components.css<br>
 ┃ ┣ 📜fonts.css<br>
 ┃ ┣ 📜hover.css<br>
 ┃ ┗ 📜reset.css<br>
 ┣ 📂html<br>
 ┃ ┣ 📂include<br>
 ┃ ┃ ┣ 📜footer.html<br>
 ┃ ┃ ┣ 📜head.html<br>
 ┃ ┃ ┗ 📜header.html<br>
 ┃ ┣ 📜00_coding_list.html<br>
 ┃ ┗ 📜index.html<br>
 ┣ 📂images<br>
 ┃ ┣ 📂...<br>
 ┣ 📂js<br>
 ┃ ┗ 📜ui.js<br>
 ┃ ┗ 📜ui.min.js<br>
 ┗ 📂lib<br>
 ┃ ┣ 📂images<br>
 ┃ ┃ ┣ 📜ui-icons_444444_256x240.png<br>
 ┃ ┃ ┗ 📜ui-icons_555555_256x240.png<br>
 ┃ ┣ 📜jquery-3.4.1.min.js<br>
 ┃ ┣ 📜jquery-sortable.js<br>
 ┃ ┣ 📜jquery-ui.css<br>
 ┃ ┗ 📜jquery-ui.min.js<br>

 build 에서는 작업 폴더 (pre-build) 에서 작업한 파일들이 build 폴더로 올라가게 됩니다. **파일 명이 변경되거나, 파일이 추가/삭제** 될 경우, build 폴더에 히스토리가 그대로 남게됩니다.

> 이럴경우, 빌드 폴더 청소를 위해, build에서 파일이 변경 된 폴더를 지우고 pre-build에서 다시 gulp를 실행해야 합니다. (주로 html 폴더나 이미지 폴더)

<br>

- font : 프로젝트에 사용되는 폰트 파일들을 모아둔 폴더입니다. 프로젝트에 따라 추가될 수 있습니다.

- lib : 프로젝트에 사용되는 라이브러리 폴더 / 파일들을 모아둔 폴더입니다. 프로젝트에 따라 추가될 수 있습니다.
