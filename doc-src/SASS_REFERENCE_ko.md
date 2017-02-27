# Sass (Syntactically Awesome StyleSheets)  

Sass는 CSS라는 기본 언어에 힘과 우아함을 더한 CSS의 확장이다. Sass는  [variables]()(변수), [nested rules]()(중첩 규칙), [mixins](), [inline imports]()등 모든 CSS의 호환되는 문법이 사용 가능하다. Sass는 큰 스타일 시트를 잘 정리된 상태로 유지해주고, 특히 [Compass스타일 라이브러리](http://compass-style.org/)의 도움으로 빠르게 작동하는 작은 스타일시트를 얻을 수 있게 해준다.  

## 특징
- 완전한 CSS 호환  
- variables(변수), nesting(중첩), mixins과 같은 언어 확장  
- 색상및 다른 값들을 처리하는 [유용한 기능들](http://sass-lang.com/documentation/Sass/Script/Functions.html)  
- 라이브러리에 대한 제어 지시같은 고급 기능  
- 형식화가 잘되고 사용자 정의가 가능한 출력  

## 문법
Sass에는 두가지 문법이 존재한다. 첫 번째로, 이 레퍼런스에서 계속 사용될 SCSS(Sassy CSS: 멋진 CSS)는 CSS문법을 확장한 것이다. 이 의미는 모든 유효한 CSS 스타일시트는 SCSS파일과 같다는 뜻이다. 게다가 SCSS는  많은 CSS 핵과 [IE’s old filter syntax](https://msdn.microsoft.com/en-us/library/ms530752.aspx)같은 vendor-specific syntax도 이해한다. SCSS 문법은 아래에 설명된 Sass와 함께 향상되었다. 이 구문을 사용하는 파일의 확장자는 `.scss`이다.  

두번째로 더 오래된 문법이고, 들여쓰기 문법으로 알려진 Sass는 CSS를 작성하는 것보다 간결한 방법을 제공한다. 선택자의 중첩을 나타내는 괄호 대신 들여 쓰기를 사용하고 속성을 분리하기 위해 세미콜론보다는 줄 바꿈을 사용한다. 몇몇 사람들은 Sass가 SCSS보다 읽기 쉽고 더 빠르게 쓸수있다고 한다. 들여쓰기 문법은 모두 동일한 기능을 갖지만 일부는 문법이 약간 다르다; 이것은 [들여쓰기 문법 레퍼런스](http://sass-lang.com/documentation/file.INDENTED_SYNTAX.html)에서 설명한다. 이 문법을사용하는 파일의 확장자명은 `.sass`이다.  

어느 문법이든 다른 문법으로 작성된 파일을 가져올 수 있다. `sass-convert` 커멘드 라인 툴(command line tool)를 사용하여 파일을 하나의 문법에서 다른 문법으로 자동 변환 할 수 있다:  
```
# Convert Sass to SCSS
$ sass-convert style.sass style.scss

# Convert SCSS to Sass
$ sass-convert style.scss style.sass
```  
이 명령은 CSS파일을 생성하지 않는다. 때문에 다른 곳에서 설명하는 Sass명령을 사용해야한다.  

## Sass 사용하기  
Sass는 세가지 방법으로 사용될 수 있다: 커멘드 라인 툴(command line tool), 루비모듈, Ruby on Rails와 Merb를 포함한 모든 Rack 지원 프레임 워크 용 플러그인으로 사용할 수 있다. 이 모든 작업의 첫 번째 단계는 Sass gem을 설치하는 것이다.  

```
gem install sass
```

Windows를 사용하는 경우 먼저 [Ruby를 설치](http://rubyinstaller.org/)해야 한다.  
커멘드 라인에서 Sass를 실행하려면,  

```
sass input.scss output.css
```
