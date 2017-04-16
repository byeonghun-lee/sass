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

Sass파일이 변경될 때마다 Sass파일을 관찰하고 CSS로 업데이트할 수 있다:  

```  
sass --watch input.scss:output.css  
```  

Sass파일이 많은 디렉토리가 있는 경우, 전체 디렉토리를 관찰하도록 지시할 수 있다:  

```  
sass --watch app/sass:public/stylesheets
```  

전체문서를 보려면 `sass --help` 를 사용한다.  

루비코드에서 Sass 사용은 매우 간단하다. Sass gem을 설치한 후, `require "sass"`을 실행하고  [Sass::Engine](http://sass-lang.com/documentation/Sass/Engine.html)을 다음과 같이 사용할 수 있다:  

```  
engine = Sass::Engine.new("#main {background-color: #0000ff}", :syntax => :scss)  
engine.render #=> "#main { background-color: #0000ff; }\n"  
```  

### Rack/Rails/Merb Plugin  

Rails 3이전 버전의 Sass in Rails을 사용하려면, `environment.rb`에 다음 줄을 추가한다:  

```  
config.gem "sass"  
```  

Rails 3의 경우, 다음 줄을 Gemfile에 추가한다:  

```
gem "sass"  
```  

Merb에서 Sass를 사용하려면 `config/dependencies.rb`에 다음 행을 추가한다:  

```  
dependency "merb-haml"  
```  
Rack어플리케이션에서 Sass를 사용하기 위해선, `config.ru`에 다음 행을 추가한다:  

```
require 'sass/plugin/rack'  
use Sass::Plugin::Rack  
```  

Sass스타일시트는 보는 것과 동일하게 작동하지 않는다. 동적 콘텐츠가 포함되어 있지 않으므로, CSS는 Sass파일이 업데이트 될 때 생성하면 된다. 기본적으로 `.sass` 와 `.scss` 파일은 public/stylesheets/sass에 위치한다.([`:template_location`]()옵션으로 사용자정의를 할 수 있다.) 그 다음에 필요할 때마다 public/stylesheets의 해당 CSS 파일로 컴파일된다. 예를 들어 public/stylesheets/sass/main.scss는 public/stylesheets/main.css로 컴파일된다.  

### Caching  
기본적으로 Sass는 컴파일 된 템플릿과 [partials]()를 캐시한다(역: 저장한다.). 이렇게하면 Sass 파일의 대량 컬렉션을 재 컴파일하는 속도가 크게 빨라지고 별도의 파일로 분할된 Sass 템플릿이 하나의 큰 파일로 모두 [`@import`]()되면 가장 효과적이다.  

프레임워크가 없으면, Sass는 캐시된(역: 저장된) 템플릿을 `.sass-cache` 디렉토리에 저장한다. Rails와 Merb에서는 `tmp/sass-cache`에 저장된다. 디렉토리는 [`:cache_location`]() 옵션을 사용하여 사용자 정의 할 수 있다. Sass가 캐싱을 전혀 사용하지 않게하려면 [`:cache`](#cache-option) 옵션을 `false`로 설정한다.  

### Options  
Rails의 `environment.rb` 또는 Rack의 `config.ru`에서 옵션은 [Sass::Plugin#options](http://sass-lang.com/documentation/Sass/Plugin/Configuration.html#options-instance_method)의 해시를 세팅하여 설정할 수 있다...  

```
Sass::Plugin.options[:style] = :compact  
```   

...또는 Merb의 `init.rb`에서 `Merb::Plugin.config[:sass]` 해시의 세팅...

```
Merb::Plugin.config[:sass][:style] = :compact  
```  

또는 옵션 해시를 [Sass::Engine # initialize](http://sass-lang.com/documentation/Sass/Plugin/Configuration.html#options-instance_method)에 전달하면된다. 모든 관련 옵션은 커멘드라인에서 실행가능한 sass 및 scss의 플래그를 통해 사용할 수 있다. 사용가능한 옵션은 다음과 같다:  

{#style-option} `:style`  

CSS 아웃풋의 스타일을 설정한다. [아웃풋 스타일]()참고.

{#syntax-option} `:syntax`  

인풋파일의 구문으로, 들여 쓰기 구문은 : sass, CSS 확장 구문은 : scss 이다. 이는 [Sass::Engine](http://sass-lang.com/documentation/Sass/Engine.html) 인스턴스를 직접 생성 할 때만 유용하다; [Sass::Plugin](http://sass-lang.com/documentation/Sass/Plugin.html)을 사용할 때 자동으로 올바르게 설정됩니다. 기본값은 `:sass`이다.  

{#property_syntax-option} `:property_syntax`  

들여 쓰기된 구문 문서가 속성에 대해 하나의 구문을 사용하도록 한다. 올바른 구문을 사용하지 않으면 오류가 발생한다. `:new`는 속성 이름 다음에 콜론 사용을 강제한다. 예: `color: #0f3` 또는 `width: $main_width`. `:old`는 속성 이름 앞에 콜론 사용을 강제한다. 예: `:color #0f3` 또는 `:width $main_width`. 기본적으로 두 구문 다 유효하다. SCSS 문서에는 아무런 영향을 미치지 않는다.  

{#cache-option} `:cache`  

 빠르게, 파싱된 Sass 파일을 캐싱해야하는지 여부. 기본값은 true이다.  

{#read_cache-option} `:read_cache`  

 이것이 설정되어 있고 `:cache`가 없다면 Sass 캐시가있는 경우에만 읽기 만하고 Sass 캐시가없는 경우에는 쓰면 안 된다.  

{#cache_store-option} `:cache_store`  

 [Sass::CacheStores::Base](http://sass-lang.com/documentation/Sass/CacheStores/Base.html)의 하위 클래스 인스턴스로 설정하면 캐시 저장소가 캐시 된 컴파일 결과를 저장하고 검색하는 데 사용된다. [:cache_location]() 옵션을 사용하여 초기화되는 [Sass::CacheStores::Filesystem](http://sass-lang.com/documentation/Sass/CacheStores/Filesystem.html)이 기본 설정된다.  

{#never_update-option} `:never_update`  

 템플릿 파일이 변경 되더라도 CSS 파일은 업데이트되지 않는다. 이 값을 true로 설정하면 성능이 약간 향상 될 수 있다. 항상 기본값은 false이다. Rack, Ruby on Rails 또는 Merb에서만 의미가 있다.  

{#always_update-option} `:always_update`  

 템플릿이 수정된 경우만 제외하고, 컨트롤러가 엑세스될 때 CSS파일이 항상 업데이트 된다. 기본값은 false이다. Rack, Ruby on Rails 또는 Merb에서만 의미가 있다.  

{#always_check-option} `:always_check`  

 서버를 시작할 때를 제외하고, 컨트롤러가 엑세스될 때 Sass 템플릿은 엡데이트를 항상 체크한다. Sass 템플릿이 업데이트됐다면 다시 컴파일되고 해당 CSS 파일을 덮어 쓴다. 프로덕션 모드에서는 기본값이 false이고 그렇지 않다면 true이다. Rack, Ruby on Rails 또는 Merb에서만 의미가 있다.  

{#poll-option} `:poll`  

true일 때 네이티브 파일시스템 백엔드보다   [Sass::Plugin::Compiler#watch](http://sass-lang.com/documentation/Sass/Plugin/Compiler.html#watch-instance_method)에 폴링 백엔드를 사용한다.  

{#full_exception-option} `:full_exception`  

 Sass코드에 에러가 있거나 없거나 Sass에서 생성 된 CSS 파일에 자세한 설명을 제공해야 한다. true로 설정하면  오류가 CSS 파일의 주석과 페이지 상단(지원되는 브라우저일 경우)에 줄 번호와 소스 코드 조각으로 함께 표시된다. 또 다르게 Ruby코드에서 예외가 발생한다. 프로덕션 모드에서는 기본값이 false이고 그렇지 않으면 true이다.  

{#template_location-option} `:template_location`  

 당신의 어플리케이션에서 root sass 템플릿 디렉토리에 대한 경로. hash인 경우 `:css_location`이 무시되고 이옵션은 input과 output 디렉토리 간의 mapping을 지정한다. 또한 hash 대신 2-element lists의 목록이 제공 될 수 있다. 기본 값은 `css_location + "/sass"`이다. Rack, Ruby on Rails 또는 Merb에서만 의미가 있다. 여러 개의 템플릿 위치가 지정되면, 모든 템플릿이 import path에 배치되고, 그 사이에 import할 수 있다. **가능한 많은 형식때문에 이 옵션은 오직 직접 설정하거나 액세스또는 수정하지 말아야 한다. [Sass::Plugin#template_location_array](http://sass-lang.com/documentation/Sass/Plugin/Configuration.html#template_location_array-instance_method), [Sass::Plugin#add_template_location](http://sass-lang.com/documentation/Sass/Plugin/Configuration.html#add_template_location-instance_method)과 [Sass::Plugin#remove_template_location](http://sass-lang.com/documentation/Sass/Plugin/Configuration.html#remove_template_location-instance_method) 메소드를 대신 사용하라**  

 {#css_location-option} `:css_location`  

CSS output을 기록해야하는 경로. `:template_location`이 hash인 경우 이 옵션은 무시된다. 기본 값은 `"./public/stylesheets"`이다. Rack, Ruby on Rails 또는 Merb에서만 의미가 있다.  

{#cache_location-option} `:cache_location`  

캐시된 `sassc`파일을 기록해야하는 경로. 기본값은 Rails와 Merb에선 `"./tmp/sass-cache"` 다른 곳에선 `"./.sass-cache"`이다. [`:cache_store` option]()이 설정되면 무시된다.  

{#unix_newlines-option} `:unix_newlines`  

true인 경우, 파일 작성시 Unix-style newlines을 사용하라. 오직 Windows에서 Sass파일로 작성할 때만 의미 있다.(Rack, Rails또는 Merb에서는 [Sass::Plugin](http://sass-lang.com/documentation/Sass/Plugin.html)을 직접 사용하거나, command-line  executable을 사용할때)  

{#filename-option} `:filename`  

랜더링된 파일의 파일이름. 이것은 오류보고에만 사용되고, Rack, Rails 또는 Merb에서는 자동으로 설정된다.  

{#line-option} `:line`  

Sass 템플릿의 첫번째 줄 번호. 오류가 있는 줄 번호를 보고하는데 사용한다. Sass 템플릿이 Ruby 파일에 내장되어 있는 경우 유용하다.  

{#load_paths-option} `:load_paths`  

Sass 템플릿에 [@import]() directive로 import된 파일 시스템과 importters 경로의 배열. 이들은 문자열, `Pathname`객체 또는 [Sass::Importers::Base](http://sass-lang.com/documentation/Sass/Importers/Base.html)의 하위 클래스 일 수 있다. 기본적으로 작업 디렉토리와 rack, Rails 또는 Merb에서 `:template_location`이다. 로드 경로는 [Sass.load_paths](http://sass-lang.com/documentation/Sass.html#load_paths-class_method) 및 `SASS_PATH` 환경 변수에 의해 알려준다.  

{#filesystem_importer-option} `:filesystem_importer`  

[Sass::Importers::Base](http://sass-lang.com/documentation/Sass/Importers/Base.html)의 하위 클래스는 일반 문자 로드 경로를 처리하는데 사용된다. 파일시스템에서 파일을 import해야 한다. 이것은 단일 문자열 인수(로드 경로)를 사용하는 생성자를 사용하여 [Sass::Importers::Base](http://sass-lang.com/documentation/Sass/Importers/Base.html)에서 상속받은 Class 객체 여야 한다. 기본값은 [Sass::Importers::Filesystem](http://sass-lang.com/documentation/Sass/Importers/Filesystem.html)이다.  

{#sourcemap-option} `:sourcemap`  

어떻게 sourcemaps이 생성되는지 제어한다. 이런 sourcemaps은 브라우저에 각 CSS 스타일을 생성시키는 Sass 스타일을 찾는 방법을 알려준다. 여기 3가지 유효한 값이 있다: **`:auto`** 는 가능한 경우 상대 URIs를 사용하고, 소스 스타일 시트는 사용하는 어떠한 서버에서도 가능하고 상대 위치는 로컬 파일 시스템과 동일하게 가정한다. 상대 URI를 사용할 수없는 경우 "file :"URI가 대신 사용됩니다. **`:file`** 은 로컬에서 작동하는 "file:" URIs로 항상 사용하지만 원격 서버에 배포할 수 없다.  **`:inline`** 은 sourcemap에서 전체 소스 텍스트를 포함한다. 이는 최대한 portable하지만 매우 큰 sourcemap파일을 생성한다. 마지막으로 **`:none`** 은 sourcemap을 전혀 생성하지 않는다.  

{#line_numbers-option} `:line_numbers`  

true로 설정하면 선택자가 정의 된 줄 번호와 파일을 컴파일 된 CSS에 주석으로 표시한다. 디버깅과, 특히 imports와 mixins을 사용할 때 유용하다. 이옵션은 `:line_comments`라고도 한다. `:compressed`  output style 또는 `:debug_info`/`:trace_selectors` 옵션을 사용할 때 자동으로 비활성화 한다.  

{#trace_selectors-option} `:trace_selectors`  

true로 설정하면 각 선택자 앞에 imports와 mixins의 전체 추적을 emit한다. 이것은 imports와 mixin을 포함한 스타일시트의 브라우저 내의 디버깅을 도와주는 데 유용하다. 이 옵션은 `:line_comments` 옵션을 대체하며 `:debug_info` 옵션으로 대체된다. `:compressed` output style을 사용할 때 자동으로 비활성화 된다.  

{#debug_info-option} `:debug_info`  

true로 설정하면 선택자가 정의 된 줄 번호와 파일이 브라우저에서 이해할 수있는 형식으로 컴파일 된 CSS로 내보내진다. Sass 파일 이름과 줄 번호를 표시하기 위해 [the FireSass Firebug extension](https://addons.mozilla.org/en-US/firefox/addon/firesass-for-firebug/) 확장과 함께 사용하면 유용하다.(역: 이젠 없는 것 같다.) `:compressed` output style을 사용할 때 자동으로 비활성화 된다.  

{#custom-option} `:custom`  

custom Sass 기능에서 데이터를 사용할 수 있도록 개별 응용 applications에서 설정할 수있는 옵션.  

{#quiet-option} `:quiet`  

true로 설정하면 경고가 비활성화 된다.  

### Syntax Selection(구문 선택)  

Sass command-line tool은 파일 확장명을 사용하여 사용중인 구문을 확인하지만 항상 파일 이름은 아니다. `sass` command-line 프로그램은 기본적으로 들여 쓰기 구문이지만 입력을 SCSS 구문으로 해석해야하는 경우 `--scss` 옵션을 전달할 수 있다. 또는 `sass`프로그램과 똑같은 `scss` command-line 프로그램을 사용할 수 있지만 구문이 SCSS라고 가정하는 것을 기본으로 한다.  

### Encodings  

Ruby 1.9 이상에서 실행될 때 Sass는 문서의 character encoding을 알고 있다. Sass는 [CSS spec](https://www.w3.org/TR/2013/WD-css-syntax-3-20130919/#determine-the-fallback-encoding)을 따라 스타일 시트의 인코딩을 결정하고, Ruby 문자열 인코딩으로 돌아간다. 즉, 유니 코드 바이트 순서 표시를 확인한 다음 `@charset` 선언과 Ruby 문자열 인코딩을 먼저 확인한다. 설정되지 않은 경우 문서는 UTF-8로 간주된다.  

스타일 시트의 인코딩을 명시적으로 지정하려면 CSS와 마찬가지로 `@charset` 선언을 사용한다. `@charset "encoding-name";`을 스타일 시트 시작 부분(공백이나 주석 앞)에 추가하면 Sass가 주어진 인코딩을 해석한다. 사용하는 인코딩에 관계없이 유니 코드로 변환할 수 있어야 한다.  

Sass는 항상 output을 UTF-8로 인코딩한다. output 파일에 비 ASCII 문자가 포함되어있는 경우에만 `@charset` 선언이 포함된다. 압축 모드에서는 `@charset` 선언 대신  UTF-8 byte order mark가 사용됩니다.  

## CSS Extensions(CSS 확장 기능)  

### Nested Rules(중첩 규칙)  

Sass를 사용하면 CSS 규칙을 서로 중첩시킬 수 있다. 내부 규칙은 외부 규칙의 선택자 내에서만 적용된다. 예 :  

```scss  
#main p {
  color: #00ff00;
  width: 97%;

  .redbox {
    background-color: #ff0000;
    color: #000000;
  }
}
```  

아래와 같이 컴파일 됨:  

```css  
#main p {
  color: #00ff00;
  width: 97%; }
  #main p .redbox {
    background-color: #ff0000;
    color: #000000; }
```  

이렇게하면 상위 선택자의 반복을 방지하고 중첩된 선택자를 많이 사용하는 복잡한 CSS 레이아웃을 훨씬 단순하게 만든다. 예 :  

```scss  
#main {
  width: 97%;

  p, div {
    font-size: 2em;
    a { font-weight: bold; }
  }

  pre { font-size: 3em; }
}
```  

아래와 같이 컴파일 됨:  

```css  
#main {
  width: 97%; }
  #main p, #main div {
    font-size: 2em; }
    #main p a, #main div a {
      font-weight: bold; }
  #main pre {
    font-size: 3em; }
```  

### Referencing Parent Selectors(부모 선택자 참조): `&` {#parent-selector}  

때때로 기본값보다 중첩규칙의 부모선택자를 사용하는 것이 유용하다. 예를 들어, 선택자가 hovered over 되거나 body 요소가 특정 class를 가질 때 특별한 스타일을 원할 수 있다. 이 경우, 부모 선택자에 &문자를 삽입하여 위치를 명시적으로 지정할 수 있다. 예를 들어:  

```scss
a {
  font-weight: bold;
  text-decoration: none;
  &:hover { text-decoration: underline; }
  body.firefox & { font-weight: normal; }
}
```  

아래와 같이 컴파일 됨:  

```css  
a {
  font-weight: bold;
  text-decoration: none; }
  a:hover {
    text-decoration: underline; }
  body.firefox a {
    font-weight: normal; }
```  

&는 CSS에 나타나는대로 부모 선택자로 대체된다.  

즉, 당신이 깊은 중첩규칙을 사용한다면, 부모선택자는 &으로 완전히 대체되어 해결된다. 예를 들어:  

```scss  
#main {
  color: black;
  a {
    font-weight: bold;
    &:hover { color: red; }
  }
}
```  

아래와 같이 컴파일 됨:  

```css  
#main {
  color: black; }
  #main a {
    font-weight: bold; }
    #main a:hover {
      color: red; }
```  

&는 복합 선택자의 앞부분의 나타나야 하지만 부모 선택자에 추가될 접미사가 뒤에 올 수 있다. 예를 들어:  

```scss  
#main {
  color: black;
  &-sidebar { border: 1px solid; }
}
```  

아래와 같이 컴파일 됨:  

```css   
#main {
  color: black; }
  #main-sidebar {
    border: 1px solid; }
```  

부모 선택자에 접미사를 적용할 수 없을 경우, Sass는 오류를 발생시킨다.  

### Nested Properties(중첩 속성)  

CSS는 “namespaces;”에 있는 많은 속성을 가지고 있다. 예를들어 `font-family`, `font-size`, 와 `font-weight`은 모두 `font`의 namespace이다. CSS에서 동일한 namespace에 다양한 속성을 설정하려면 매번 입력해야한다. Sass는 이처럼 간단한 방법을 제공한다: namespace를 한번 작성한 다음, 각 하위 속성은 중첩한다. 예를 들어:  

```scss  
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```  

아래와 같이 컴파일 됨:  

```css  
.funky {
  font-family: fantasy;
  font-size: 30em;
  font-weight: bold; }
```  

속성 namespace자체도 값을 가질 수 있다. 예를 들어:  

```scss  
.funky {
  font: 20px/24px fantasy {
    weight: bold;
  }
}
```  

아래와 같이 컴파일 됨:  

```css  
.funky {
  font: 20px/24px fantasy;
    font-weight: bold;
}
```  

### Placeholder Selectors: `%foo`  
