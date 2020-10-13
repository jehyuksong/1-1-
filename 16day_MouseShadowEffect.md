# 1일 1프로젝트 16일차  Mouse Shadow Effect

- html, css

```css
<div class="hero">
      <h1 contenteditable>🔥WOAH!</h1>
    </div>

    <style>
      html {
        color: black;
        font-family: sans-serif;
      }

      body {
        margin: 0;
      }

      .hero {
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        color: black;
      }

      h1 {
        text-shadow: 10px 10px 0 rgba(0, 0, 0, 1);
        font-size: 100px;
      }
    </style>
```

- js

```jsx
// 기준이 되는 div와 글자를 선택한다.
      const hero = document.querySelector(".hero");
      const text = hero.querySelector("h1");
      const walk = 500; // 500px

      // shadow 함수를 만든다.
      function shadow(e) {
        // hero의 크기를 구조분해해서 변수로 저장
        const { offsetWidth: width, offsetHeight: height } = hero;
        // 마우스 위치를 저장
        let { offsetX: x, offsetY: y } = e;

        if (this !== e.target) {
          x = x + e.target.offsetLeft;
          y = y + e.target.offsetTop;
        }

        // 현재 마우스 위치를 div 높이와 너비로 나누고 일정량을 곱한 뒤 반올림해준 값을 변수로 담는다.
        const xWalk = Math.round((x / width) * walk - walk / 2);
        const yWalk = Math.round((y / height) * walk - walk / 2);
        
        // 그림자가 어떻게 생길지 설정해준다.
        text.style.textShadow = `
      ${xWalk}px ${yWalk}px 0 rgba(255,0,255,0.7),
      ${xWalk * -1}px ${yWalk}px 0 rgba(0,255,255,0.7),
      ${yWalk}px ${xWalk * -1}px 0 rgba(0,255,0,0.7),
      ${yWalk * -1}px ${xWalk}px 0 rgba(0,0,255,0.7)
    `;
      }

      // 마우스가 움직일때 shadow 함수를 실행한다.
      hero.addEventListener("mousemove", shadow);
```

- 다양한 프로젝트를 해나가면 해나갈수록 순수 자바스크립트만으로 모든 것을 구현할 수 있고, 순수 자바스크립트를 잘해야 한다는 이유를 알 것 같다.
