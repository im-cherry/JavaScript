# 05 자바스크립트 HTML DOM

> **목차**
>
> 1. [DOM Element](#1-dom-element)
> 2. [DOM Attribute](#2-dom-attribute)
> 3. [HTML 내용 변경](#3-html-내용-변경)
> 4. [DOM 이벤트](#4-dom-이벤트)
> 5. [DOM Style](#5-dom-style)

자바스크립트는 HTML 문서의 모든 요소에 접근하여 변경할 수 있습니다. 사용자가 웹 페이지에 접근하면 웹 페이지가 로드되면서 브라우저는 웹 페이지에 대한 DOM을 생성하게 됩니다.

![그래프](https://user-images.githubusercontent.com/100753621/156879276-ec91ae47-2478-450a-9aad-aa28a6bae21d.png)

### 1. DOM Element

#### HTML요소의 id로 HTML 요소 찾기

> document.getElementById(id)

```html
<!DOCTYPE >
<html>
  <body>
    <input type="text" id="userid" />
    <script>
      let element = document.getElementById("userid");
    </script>
  </body>
</html>
```

#### HTML요소의 태그명을 이용해서 HTML요소 찾기

> document.getElementsByTagName(태그명)

```html
<!DOCTYPE >
<html>
  <body>
    <p>태그명을 사용해서 HTML 요소를 찾습니다.</p>
    <p>태그명을 사용해서 HTML 요소를 찾습니다.</p>
    <script>
      let elements = document.getElementsByTagName("p");
    </script>
  </body>
</html>
```

#### 클래스명을 이용해서 HTML요소 찾기

> document.getElementsByClassName(클래스명)

```html
<!DOCTYPE >
<html>
  <body>
    <p class="para">클래스명을 사용해서 HTML 요소를 찾습니다.</p>
    <p class="para">클래스명을 사용해서 HTML 요소를 찾습니다.</p>
    <script>
      let elements = document.getElementsByClassName("para");
    </script>
  </body>
</html>
```

#### CSS선택자를 이용해서 HTML요소 찾기

```css
/* 태그 선택자 */
p {
  color: red;
  text-align: center;
}

/* 클래스 선택자 */
.bg-red {
  background-color: red;
}
.h-100 {
  height: 100px;
}

/* 아이디 선택자 */
#container {
  width: 100%;
  font-size: 14pt;
}

/* 하위 선택자 */
section ul {
  border: 1px dotted black;
  font-size: 14pt;
}

/* 자식 선택자 */
section > ul {
  border: 1px dotted black;
  font-size: 14pt;
}

/* 인접 형제 선택자 */
h1 + ul {
  background: blue;
}

/* 일반 형제 선택자 */
h1 ~ ul {
  background: green;
}

/* 속성 선택자 */
a[href] {
  color: black;
  text-decoration: none;
}
input[type="text"] {
  width: 200px;
  border: 1px solid #ddd;
}
```

> document.querySelectorAll(css선택자);

```html
<!DOCTYPE >
<html>
  <body>
    <p class="para">선택자를 사용해서 HTML요소를 찾습니다.</p>
    <script>
      const elements = document.querySelectorAll(".para");
    </script>
  </body>
</html>
```

```html
<!DOCTYPE >
<html>
  <body>
    <label>
      <input type="checkbox" name="chk_interest" value="it" />IT/컴퓨터
    </label>
    <label>
      <input type="checkbox" name="chk_interest" value="sports" />스포츠
    </label>
    <label>
      <input type="checkbox" name="chk_interest" value="shopping" />쇼핑
    </label>
    <label>
      <input type="checkbox" name="chk_interest" value="book" />도서/책
    </label>
    <script>
      let elements = document.querySelectorAll("[name=chk_interest]:checked");
    </script>
  </body>
</html>
```

### 2. DOM Attribute

#### getAttribute()

```html
<!DOCTYPE >
<html>
  <body>
    <input type="text" id="test" value="ABC" />
    <script>
      let test = document.getElementById("test");
      let testValue1 = test.value;
      let testValue2 = test.getAttribute("value");

      console.log(testValue1); // ABC
      console.log(testValue2); // ABC
    </script>
  </body>
</html>
```

#### setAttribute()

```html
<!DOCTYPE >
<html>
  <head>
    <style>
      .btn-blue {
        background-color: blue;
        color: white;
      }
      .btn-black {
        background-color: black;
        color: white;
      }
    </style>
  </head>
  <body>
    <button onclick="doSave(event);" class="btn-blue">저장</button>
    <script>
      function doSave(e) {
        let obj = e.target;

        if (obj.getAttribute("class") == "btn-blue") {
          obj.setAttribute("class", "btn-black");
        } else {
          obj.setAttribute("class", "btn-blue");
        }
      }
    </script>
  </body>
</html>
```

#### hasAttribute()

```html
<!DOCTYPE >
<html>
  <body>
    <input type="test" id="test" value="ABC" data-role="name" />
    <script>
      let test = document.getElementById("test");
      console.log(test.hasAttribute("data-role")); // true
    </script>
  </body>
</html>
```

#### removeAttribute()

```html
<!DOCTYPE >
<html>
  <body>
    <button onclick="doSave(event);">저장</button>
    <script>
      function doSave(e) {
        let obj = e.target;
        obj.disabled = true;

        setTimeout(function () {
          obj.removeAttribute("disabled");
        }, 2000);
      }
    </script>
  </body>
</html>
```

### 3. HTML 내용 변경

#### innerHTML

```html
<!DOCTYPE >
<html>
  <body>
    <select id="sel"></select>
    <script>
      let sel = document.getElementById("sel");
      sel.innerHTML = `<option value="">선택하세요</option>`;
    </script>
  </body>
</html>
```

#### innerText

```html
<!DOCTYPE >
<html>
  <body>
    <h1 id="title"></h1>
    <script>
      document.getElementById("title").innerText = "제목입니다.";
    </script>
  </body>
</html>
```

#### insertAdjacentHTML()

```html
<!DOCTYPE >
<html>
  <body>
    <!-- beforebegin-->
    <ul id="myUl">
      <!-- afterbegin-->
      <li>항목 1</li>
      <li>항목 2</li>
      <li>항목 3</li>
      <li>항목 4</li>
      <!-- beforeend-->
    </ul>
    <!-- afterend -->
    <button onclick="myFunction()">항목 추가</button>
    <script>
      function myFunction() {
        let ul = document.getElementById("myUl");
        ul.insertAdjacentHTML("beforeend", `<li>새로운 항목</li>`);
      }
    </script>
  </body>
</html>
```

#### insertAdjacentText()

```html
<!DOCTYPE >
<html>
  <body>
    <!-- beforebegin -->
    <p class="para">
      <!-- afterbegin -->
      World
      <!-- beforeend -->
    </p>
    <!-- afterend -->
    <script>
      document
        .getElementsByClassName("para")[0]
        .insertAdjacentText("afterbegin", "Hello ");
    </script>
  </body>
</html>
```

#### remove()

```html
<!DOCTYPE >
<html>
  <body>
    <p id="demo">p태그 문장입니다.</p>
    <button onclick="myFunction()">Remove</button>
    <script>
      function myFunction() {
        let myObj = document.getElementById("demo");
        myObj.remove();
      }
    </script>
  </body>
</html>
```

### 4. DOM 이벤트

#### click 이벤트(onclick)

```html
<!DOCTYPE >
<html>
  <body>
    <button onclick="myFunction();">클릭1</button><br />
    <button id="btn">클릭2(클릭1을 눌러야지 실행됩니다.)</button>
    <script>
      function myFunction() {
        alert("클릭1");

        document.getElementById("btn").addEventListener("click", function () {
          alert("클릭2");
        });
      }
    </script>
  </body>
</html>
```

#### change 이벤트(onchange)

> change 이벤트가 발생하는 DOM 요쇼
>
> `<select>, <input type="checkbox">, <input type="radio">`

```html
<!DOCTYPE >
<html>
  <body>
    <select id="selectCountry" onchange="doChange();">
      <option value="KO">Korea</option>
      <option value="CN">China</option>
      <option value="JP">Japan</option>
    </select>
    <script>
      function doChange() {
        let selectedValue = document.getElementById("selectCountry").value;
        console.log(selectedValue);
      }
    </script>
  </body>
</html>
```

#### focus 이벤트(onfocus)

```html
<!DOCTYPE >
<html>
  <body>
    <input type="text" id="content" onfocus="doFocus();" />
    <script>
      function doFocus() {
        console.log("doFocus");
      }
    </script>
  </body>
</html>
```

#### blur 이벤트(onblur)

```html
<!DOCTYPE >
<html>
  <body>
    <input type="text" id="content" onblur="doBlur(this);" />
    <script>
      function doBlur(obj) {
        if (obj.value == "") {
          return alert("필수값입니다. 반드시 입력하세요.");
        }
        console.log(obj.value);
      }
    </script>
  </body>
</html>
```

#### key 이벤트(onkeydown, onkeypress, onkeyup)

```html
<!DOCTYPE >
<html>
  <body>
    <input type="text" onkeypress="myFunction(event);" />
    <script>
      function myFunction(e) {
        console.log(e.type); // keypress
        console.log(e.target); // <input type="text" onkeypress="myFunction(event);" />
        console.log(e.target.value);
      }
    </script>
  </body>
</html>
```

#### scroll 이벤트(onscroll)

```html
<!DOCTYPE >
<html>
  <body>
    <div style="height: 100px; overflow-y: auto" onscroll="myFunction(event);">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
      <p>Paragraph 3</p>
      <p>Paragraph 4</p>
      <p>Paragraph 5</p>
      <p>Paragraph 6</p>
      <p>Paragraph 7</p>
      <p>Paragraph 8</p>
      <p>Paragraph 9</p>
      <p>Paragraph 10</p>
    </div>
    <script>
      function myFunction(e) {
        console.log(e);
      }
    </script>
  </body>
</html>
```

#### mouse 이벤트 (onmouserover, onmouseout)

```html
<!DOCTYPE >
<html>
  <head>
    <style>
      #box {
        width: 100px;
        height: 100px;
        border: 3px solid black;
      }
      #box.hover {
        background: orange;
        color: white;
      }
    </style>
  </head>
  <body>
    <div id="box">
      <p>마우스를 올려 주세요.</p>
    </div>
    <script>
      let box = document.getElementById("box");

      box.addEventListener("mouseover", function () {
        box.setAttribute("class", "hover");
      });
      box.addEventListener("mouseout", function () {
        box.removeAttribute("class");
      });
    </script>
  </body>
</html>
```

### 5. DOM Style

```html
<!DOCTYPE >
<html>
  <head>
    <style>
      .border-red {
        border: 2px solid red;
      }
      .border-green {
        border: 2px solid green;
      }
      .border-default {
        border: 2px solid black;
      }
    </style>
  </head>
  <body>
    이름:<br />
    <input
      type="text"
      id="name"
      onblur="changeBorder();"
      class="border-default"
    /><br />
    이메일수신:<br />
    <label>
      <input
        type="radio"
        name="radio_email_yn"
        value="Y"
        onclick="showEmail();"
      />
      동의</label
    >
    <label>
      <input
        type="radio"
        name="radio_email_yn"
        value="N"
        onclick="hideEmail();"
      />
      거부</label
    >
    <div id="divEmail" style="display: none">
      이메일: <input type="text" id="email" />
    </div>
    <br />
    국적:
    <br />
    <select id="selectCountry" onchange="doChange(this);">
      <option value=""></option>
      <option value="KO">Korea</option>
      <option value="CN">China</option>
      <option value="JP">Japan</option>
    </select>
    <select id="koreaCity" style="display: none">
      <option value="Seoul">서울</option>
      <option value="Busan">부산</option>
      <option value="Deajeon">대전</option>
      <option value="Jeju">제주</option>
    </select>
    <button type="button" onclick="doSave();">저장하기</button>
    <script>
      function changeBorder() {
        let name = document.getElementById("name");
        if (name.value != "") {
          name.className = "border-green";
        } else {
          name.className = "border-default";
        }
      }

      function showEmail() {
        document.getElementById("divEmail").style.display = "";
      }
      function hideEmail() {
        document.getElementById("divEmail").style.display = "none";
      }

      function doChange(obj) {
        if (obj.value == "KO") {
          document.getElementById("koreaCity").style.display = "";
        } else {
          document.getElementById("koreaCity").style.display = "none";
        }
      }

      function doSave() {
        let name = document.getElementById("name");
        if (name.value == "") {
          name.className = "border-red";
          return alert("이름을 입력해주세요!");
        }
        alert("저장합니다.");
      }
    </script>
  </body>
</html>
```

<br/>  
<br/>

:arrow_forward: [06 자바스크립트의 메모리 관리](./06%20%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%9D%98%20%EB%A9%94%EB%AA%A8%EB%A6%AC%20%EA%B4%80%EB%A6%AC.md) :arrow_forward:
