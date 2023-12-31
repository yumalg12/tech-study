## SASS, SCSS

### scss(sass)란? [1]
Syntactically Awesome StyleSheet의 약어이며, CSS를 효율적으로 작성할 수 있도록 도와주는 전처리기이다.


### .sass란?
sass는 css의 전처리기, 즉 해석되어 css로 컴파일되는 스크립트 언어이다. 기존 우리가 사용하던 sass에서 많이들 들어봤을 mixin, function 등 여러 기능을 제공한다. 또한 변수 정의를 허용하는데, 변수는 $ 기호로 시작되고, 변수 할당은 콜론(:)으로 마무리한다. sassScript는 4가지 자료형을 지원하는데, 수(int), 문자열(string), 컬러, 불린(boolean)을 지원한다.

 
### .scss란?
scss는 sass의 3버전에서 등장한 언어이다. 퍼블리셔에게 익숙한 css와 비슷한 구문을 가지고 있으며, css와 완전히 호환되도록 새로운 구문을 도입한 css의 상위 호환 스타일시트이다. sass기능을 지원하되, css와 거의 같은 문법으로 사용된다는 점에서, 퍼블리셔들에게 각광받는 언어이다.

 
### SCSS - SASS를 사용하는 이유? [2]
css가 복잡한 언어는 아니지만 프로젝트의 크기가 커질수록 유지보수에 어려움이 생긴다. 예를 들어 기존의 CSS는 불필요한 선택자(Selector), 연산 기능 한계, 구문(Statement)의 부재의 문제점이 있고 SASS와 SCSS는 이러한 이슈를 해소시켜줄 수 있다.


### CSS, Sass, SCSS 비교 [3]

- CSS
```
/**CSS Syntax**/

nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

- Sass
```
/**Sass Syntax**/

nav
  ul
    margin: 0
    padding: 0
    list-style: none

  li
    display: inline-block

  a
    display: block
    padding: 6px 12px
    text-decoration: none
```

- SCSS
```
/**SCSS Syntax**/

nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

###출처
[1] https://heewon26.tistory.com/360 <br>
[2] https://thdud4479.tistory.com/210 <br>
[3] https://yunzema.tistory.com/269 <br>