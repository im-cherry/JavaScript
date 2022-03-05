# 07 자바스크립트 주요 Web APIs

> **목차**
>
> 1. [LocalStorage, SessionStorage](#1-localstorage-sessionstorage)
> 2. [Geolocation API](#2-geolocation-api)
> 3. [Web Speech API](#3-web-speech-api)
> 4. [encodeURI / decodeURI](#4-encodeuri--decodeuri)

### 1. LocalStorage, SessionStorage

#### LocalStorage

로컬스토리지는 저장된 데이터를 삭제하기 전까지 영구히 보존되므로 보안에 위배되지 않고 영구히 저장해도 상관 없는 데이터를 저장할 때 적합합니다.
저장되는 모든 데이터는 키와 값의 쌍으로 저장할 수 있으며, 저장되는 모든 값은 String으로만 저장할 수 있습니다.  
Number, Boolean, Object, Array 같은 형태의 데이터를 저장할 때는 JSON.stringify 를 이용하여 문자열로 변환해 저장합니다. 반대로 데이터를 읽을 때는 JSON.parse 를 이용하여 원래의 데이터 형태로 변환해서 사용할 수 있습니다.

```javascript
if (typeof Storage !== "undefined") {
  localStorage.setItem("title", "The Great");

  const users = [
    {
      id: 1,
      name: "임채은",
    },
    {
      id: 2,
      name: "이지은",
    },
  ];
  localStorage.setItem("users", JSON.stringify(users));
}
```

```javascript
if (typeof Storage !== "undefined") {
  console.log(localStorage.getItem("title"));
  console.log(JSON.parse(localStorage.getItem("users")));
}
```

```javascript
localStorage.removeItem("title");
localStorage.removeItem("users");
```

#### SessionStorage

세션스토리지에 저장된 데이터는 브라우저 창(탭)을 닫는 순간 자동으로 삭제되므로 일회성 데이터를 저장합니다. 사용자 정보 중 세션을 유지하는 동안에만 참조할 데이터 혹은 화면 이동 시 전달해야 할 파라미터가 많은 데이터를 저장할 때 적합합니다.

```javascript
if(typof Storage !== "undefined") {
    sessionStorage.setItem("title", "The Great");

    const users = [
        {
            id: 1,
            name: "임채은",
        },
        {
            id: 2,
            name: "이지은",
        },
    ];
    sessionStorage.setItem("users", JSON.stringify(users));
}
```

```javascript
if(typof Storage !== "undefined") {
    console.log(sessionStorage.getItem("title"));
    console.log(JSON.parse(sessionStorage.getItem("users")));
}
```

```javascript
sessionStorage.removeItem("title");
sessionStorage.removeItem("users");
```

### 2. Geolocation API

Geolocation API는 웹 브라우저에 접속한 사용자의 지리적 위치 정보에 대한 위도, 경도 값을 확인할 수 있게 해주는 API 입니다.

```javascript
if ("geolocation" in navigator) {
  // 위치정보 사용 가능

  // 현재 접속한 사용자의 위치 정보
  navigator.geolocation.getCurrentPosition((position) => {
    const latitude = position.coords.latitude; // 위도
    const longitude = position.coords.longitude; // 경도
  });
} else {
  // 위치정보 사용 불가능
}
```

```javascript
// 사용자가 이동 중일때, 콜백함수를 통해 사용자의 위치 정보 조회 가능
const watchID = navigator.geolocation.watchPosition((position) => {
  const latitude = position.coords.latitude; // 위도
  const longitude = position.coords.longitude; // 경도
});

// 실시간 사용자 위치 정보를 사용하지 않을 때는 반드시 함수 종료
navigator.geolocation.clearWatch(watchID);
```

### 3. Web Speech API

Web Speech API는 음성 정보를 텍스트로 변환해주는 API입니다.

```javascript
// 현재 브라우저가 Web Speech API를 지원하는지 체크
let recognition = null;

function checkCompatibility() {
  recognition = new SpeechRecognition();

  if (!recognition) {
    alert("Web Speech API를 사용할 수 없습니다.");
  }

  recognition.lang = "en"; // 사용할 언어 코드
  recognition.maxAlternatives = 3; // 음성에 대한 텍스트 전환 시, 음성에 가장 가까운 텍스트 3개까지 결과 반환
}

// 음성 인식 시작 함수
function startSpeechRecognition() {
  recognition.addEventListener("speechstart", () => {
    // 음성 시작
    console.log("말하세요.");
  });

  recognition.addEventListener("speechend", () => {
    // 음성 종료
    console.log("그만 말하세요.");
  });

  recognition.addEventListener("result", (event) => {
    // 음성 결과 가져오기
    console.log(event.results);
    const text = event.results[0][0].transcript;
    document.getElementById("speech_result").value = text; // 음성을 텍스트로 전환한 결과를 보여줌.
  });

  recognition.start(); // 음성 인식 시작
}

// 음성 인식 종료 함수
function endSpeechRecognition() {
  recognition.stop(); // 음성 인식 종료
}
```

### 4. encodeURI / decodeURI

#### encodeURI()

encodeURI()는 URI의 특정한 문자를 UFT-8로 인코딩하고 연속된 이스케이프 문자로 변환합니다.

```javascript
console.log(encodeURI("http://domain.com?x=A")); // http://domain.com?x=A
console.log(encodeURI("http://domain.com?x=가")); // http://domain.com?x=%EA%B0%80
```

#### decodeURI()

decodeURI()는 인코딩된 문자를 디코딩 해줍니다.

```javascript
const encoded = encodeURI("http://domain.com?x=가");

console.log(encoded); // http://domain.com?x=%EA%B0%80
console.log(decodeURI(encoded)); // http://domain.com?x=A
```

<br/>  
<br/>

:arrow_forward: [00 Summary](./00%20Summary.md) :arrow_forward:
