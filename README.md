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