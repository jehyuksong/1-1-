# 1일 1프로젝트 (20일차 Native Speech Recognition)

```jsx
// html

<div class="words" contenteditable></div>
```

```jsx
// js

// 음성인식 api를 사용한다.
      window.SpeechRecognition =
        window.SpeechRecognition || window.webkitSpeechRecognition;

      // 변수로 지정해준다.
      const recognition = new SpeechRecognition();
      // 최종결과를 반환하는 것이 아닌 중간결과를 반환한다.
      recognition.interimResults = true;
      // 인식언어를 설정한다.
      recognition.lang = "en-US";

      // html 문단 요소를 만든다.
      let p = document.createElement("p");
      // div 요소를 선택한다.
      const words = document.querySelector(".words");
      // div 요소에 p 요소를 넣는다.
      words.appendChild(p);

      // 음성인식 서비스가 결과를 반환할 때 일어나는 이벤트가 result이다.
      recognition.addEventListener("result", e => {
        const transcript = Array.from(e.results)
          .map(result => result[0])
          .map(result => result.transcript)
          .join("");

        // 일부 단어들을 💩 으로 바꾼다.
        const poopScript = transcript.replace(/poop|poo|shit|dump/gi, "💩");
        p.textContent = poopScript;

        // 마지막 단어일경우 p를 만들고 div에 넣는다.
        if (e.results[0].isFinal) {
          p = document.createElement("p");
          words.appendChild(p);
        }
      });

      // 음성인식이 끝나면 음성인식을 다시 실행한다.
      recognition.addEventListener("end", recognition.start);

      // 음성인식을 실행한다.
      recognition.start();
```

- 음성인식이 엄청 어려운거라고 막연하게만 생각하고 있었는데 생각보다 어렵지 않게 구현되는 걸 보고 신기했다.
