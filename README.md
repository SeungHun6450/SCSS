# Scss
Scss 문법을 통해 표준 css문법보다 쉽고 강력한 기능을 가지고 있기에 사용한다.
하지만 브라우저에서 실제로 동작할 수 있는 것은 표준의 css뿐이므로 Sass문법을 css 문법으로 변환(컴파일)을 해줘야 한다.
css의 전처리 도구라고 한다.


## 1. 주석
```scss
/* */ : 변환된 후에도 주석이 남아 있어야 하면 사용하는 방법
//    : 그 외의 방법
```

## 2. 중첩
```html
<div classs="container">
  <ul>
    <li>
      <div class="name">Hun</div>
      <div class="age">27</div>
    </li>
  </ul>
</div>
```
```scss
.container {
  ul {
    li {
      font-size: 40px;
      .name {
        color: royalblue;
      }
      .age {
        color: orange;
      }
    }
  }
}
```

## 3. 상위 선택자 참조
&: 자신이 포함되어져 있는 영역의 선택자를 참조한다.

```scss
// css
.btn {
  position: absolute;
}
.btn.active {
  color: red;
}
// scss
.btn {
  position: absolute;
  &.active {
    color: red;
  }
}

// css
.list li:last-child {
  margin-right: 0;
}
// scss
.list {
  li {
    &:last-child {
      margin-right: 0;
    }
  }
}


// css
.fs-small {
  font-size: 12px;
}
.fs-medium {
  font-size: 14px; 
}
.fs-large {
  font-size: 16px;
}
//scss
.fs { 
  &-small { font-size: 12px; }
  &-medium { font-size: 14px; }
  &-large { font-size: 16px; }
}

```

## 4. 중첩된 속성
선택자 처럼 사용 하되 뒷부분에 ':' 을 붙혀주고 중괄호 끝에 ';' 를 붙혀줘야한다.
'-': 네임스페이스, 이름을 통해 구분 가능한 범위를 만들어내는 것으로 일종의 유효범위를 지정하는 방법을 말한다.

```scss
// css
.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 20px;
  padding-right: 30px
}

// scss
.box {
  font: {
    weight: bold;
    size: 10px;
    family: sans-serif;
  };
  margin: {
    top: 10px;
    left: 20px;
  };
  padding: {
    top: 10px;
    bottom: 40px;
    left: 20px;
    right: 30px
  };
};

```

## 5. 변수

'$변수' 로 사용한다.
선언된 범위에서 유효범위를 가지고 있다.
변수 javascript의 let과 같이 재할당이 가능하다!


```scss
// css
.container {
  position: fixed;
  top: 100px;
  left: 100px;
}
.container .item {
  width: 100px;
  height: 100px;
  transform: translateX(100px);
}
//scss
container {
  $size: 200px;
  position: fixed;
  top: $size;
  .item {
    $size: 100px;
    width: $size;
    height: $size;
    transform: translateX($size);
  }
  left: $size;  // left: 100px;
}
```
## 6. 산술 연산자
- 단위가 동일해야 산술 연산자를 사용할 수 있다. 다른 단위로 계산하여 사용하고 싶다면 calc()를 사용한다.
```scss
  div {
    // width: 100% - 200px;
    width: calc(100% - 200px);
  }
```
- '/(나누기)': scss에서 '/'는 단축 속성을 사용한 것 처럼 출력이 된다.
제대로 사용하려면 소괄호를 사용하거나 변수에 값을 할당하여 적용한다.
```scss
// css
div {
  $size: 30px;
  width: 40px;
  height: 30px;
  font-size: 20px;
  margin: 30px / 2;
  // margin: $size / 2;
  // margin: (30px / 2);
  // margin: 10px + 10px / 2;
  padding: 6px;
}
// scss
div {
  width: 20px + 20px;
  height: 40px - 10px;
  font-size: 10px * 2;
  margin: 30px/2;
  padding: 20px % 7;
}
span { 
  font-size: 10px;
  line-height: 10px;
  font: 10px;
}
```

## 7. 재활용(Mixins)
@mixin을 사용하면 코드를 재활용 할 수 있다.
@include로 가져와서 해당 부분에 적용할 수 있다!
변수와 비슷하지만 여러가지 스타일을 한 번에 담아낼 수 있다는 차이점이 있다.
매개변수를 추가해서 사용이 가능하며 기본 값을 지정할 수 있다.
- 키워드 인수: 인수를 하나 사용하는데 인수 앞에 매개변수 이름을 지정하는 것이다.
```html
  <div class="container">
    <div class="item">
      Mixin!
    </div>
  </div>
```
```scss
// css
.container {
  width: 200px;
  height: 200px;
  background-color: red;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: green;
  display: flex;
  justify-content: center;
  align-items: center;
}
.box {
  width: 100px;
  height: 100px;
  background-color: royalblue;
}

// scss
// 기본값 설정
@mixin box($size: 100px, $color: royalblue) {
  width: $size;
  height: $size;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  @include box(200px, red);
  .item {
    // 키워드 인수
    @include box($color: green);
  }
}
.box {
  @include box;
}
```

## 8. 반복문
css 선택자에서는 숫자를 그대로 명시하는 것이 불가능하여 보간을 사용하는데 '#{}'를 사용한다. 
값을 적는 부분이 아닌 경우에 보간을 사용해 준다.
```scss
// javascript의 반복문 예시
/*
  for (let i = 0; i < 10; i += 1){
    console.log(`loop-${i}`)
  }
*/
@for $i form 1 through 10 {
  .box:nth-child(#{$i}) {
    width: 100px * $i;
  }
}
```
## 9. 함수
어떠한 값을 따로 연산해서 반환된 결과로 사용하기 위해서 만들어내는 개념이다.

```scss
// css
.box {
  width: 100px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}

// scss
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}

@function ratio($size, $ratio) {
  @return $size * $ratio
}

.box {
  $width: 100px;
  width: $width;
  height: ratio($width, 1/2);
  @include center;
}
```
## 10. 색상 내장 함수
- mix(color1, color2): 첫 번째 인수의 색상과 두 번째 인수의 색상을 섞어서 새로운 색상을 만들어 준다.
- lighten(color1, %): 첫 번째 인수의 색상을 %만큼 더 밝게 만들어 준다.
- darken(color1, %): 첫 번째 인수의 색상을 %만큼 더 어둡게 만들어 준다.
- saturate(color1, %): 첫 번째 인수의 색상의 채도를 %만큼 더 올려준다.
- desaturate(color1, %): 첫 번째 인수의 색상의 채도를 %만큼 더 낮춰준다.
- grayscale(color): 주어진 색상을 회색으로 만들어준다.
- invert(color): 주어진 색상을 반전 시켜준다.
- rgba(color, .n): 주어진 색상을 투명도를 적용시켜 준다.

```html
<div class="box"></div>
<div class="box built-in"></div>
```
```scss
.box {
  $color: royalblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  border-radius: 10px;
  background-color: $color;
  &:hover {
    // darken
    // background-color: darken($color, 10%);

    // desaturate
    // background-color: desaturate($color, 10%);
  }
  &.built-in {
    // mix
    // background-color: mix($color, red);

    // lighten
    // background-color: lighten($color, 10%);

    // saturate
    // background-color: saturate($color, 10%);

    // grayscale
    // background-color: grayscale($color);

    // invert
    // background-color: invert($color);

    // rgba
    background-color: rgba($color, .5);

  }
}

```

## 11. 가져오기
main.scss와 root경로에 sub.scss, sub2.scss 2개의 scss의 파일이 있다고 가정하자.
@import를 사용하여 main.scss에서 sub, sub2 scss파일을 연결하여 가져오는 방법이다.
@import url; 방식으로 작성을 하는데 아래의 예시에서 어떻게 사용을 하는지 보자.
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="./main.scss" />
</head>
<body>
  <div class="container">
    <h1>Hello SCSS!</h1>
  </div>
</body>
</html>
```
```scss
// @import './sub1';
@import './sub1', './sub2';
// @import './sub1.scss', './sub2.scss';
// @import url('./sub1'), url('./sub2');

$color: royalblue;

.container {
  h1 {
    color: $color;
  }
}
```
```scss
// sub1.scss
body {
  .container {
    background-color: orange;
  }
}
```
```scss
// sub2.scss
body {
  background-color: skyblue;
}
```

## 12. 데이터 종류
- $number: 숫자, px, em
- $string: relative, ""... ★red나 blue같은 색상들은 색상데이터이다.
- $color: red, blue, rgba(0,0,0,.1)
- $boolean: true, false
- $null: null, null을 사용하면 출력이 안되게 만들 수 있다.
- $list: javascript의 배열과 유사하다. 쉼표로 구분하여 순서대로 데이터를 명시한다. 
- $map: javascript의 객체와 유사하다. 소괄호로 영역을 잡고 key와 value로 구성되어 있다.
```scss
// css
.box {
  width: 100px;
  color: red;
  position: relative;
}

// scss
$number: 1;     // .5, 100px, 1em
$string: bold;  // rerlative, "../images/a.png"
$color: red;    // blue,  rgba(0,0,0,.1)
$boolean: true; // false
$null: null;
$list: orange, royalblue, yellow;
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);

.box {
  width: 100px;
  color: red;
  position: relative;
}
```
## 13. 반복문 @each
- lsit
@each 변수 in 리스트 {}: 리스트 안에 데이터들을 반복적으로 변수에 담아 중괄호 사이에서 처리한다.
```scss
// css: list 반복
.box {
  color: orange;
}
.box {
  color: royalblue;
}
.box {
  color: yellow;
}


// scss
$list: orange, royalblue, yellow;

@each $c in $list {
  .box {
    color: $c;
  }
}
```
- map
key, value 형태이기 때문에 ,로 구분하여 key와 value형태로 내부에서 사용할 수 있다.

```scss
// css: map 반복
.box-o {
  color: orange;
}
.box-r {
  color: royalblue;
}
.box-y {
  color: yellow;
}


// scss
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);

@each $key, $value in $map {
  .box-#{$k} {
    color: $v;
  }
}

```
## 14. 재활용 @content
필요에 따라 @mixin에 추가적인 내용을 더해서 사용할 수 있는 문법이다.
아래의 예시를 예로 들면 @include의 중괄호 사이에 있는 새로운 코드들이 @content에 들어가는 개념이다.
```scss
// css
.container {
  width: 100px;
  height: 100px;
  position: absolute;
  top: 0;
  left: 0;
}

.box {
  width: 200px;
  height: 300px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}

// scss
@mixin left-top {
  position: absolute;
  top: 0;
  left: 0;
  @content;
}
.container {
  width: 100px;
  height: 100px;
  @include left-top;
}
.box {
  width: 200px;
  height: 300px;
  @include left-top {
    bottom: 0;
    right: 0;
    margin: auto;
  }
}

```