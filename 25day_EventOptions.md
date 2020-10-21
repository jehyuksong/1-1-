# 1일 1프로젝트 (25일차 Event Capture, Propagation, Bubbling and Once)

```html
<!-- html -->

<div class="one">
      <div class="two">
        <div class="three"></div>
      </div>
    </div>
```

---

```jsx
// js

// div를 다 가져온다.
      const divs = document.querySelectorAll("div");
      // 버튼을 가져온다.
      const button = document.querySelector("button");

      // 클래스 이름이 콘솔에 뜬다.
      function logText(e) {
        console.log(this.classList.value);
      }

      // 각 div를 누르면 logText함수가 실행된다.
      divs.forEach(div =>
        div.addEventListener("click", logText, {
          // 버블링과 캡쳐링의 차이라고 하는데 많은 포스트를 봐도 뭘 뜻하는지 잘모르겠다.
          capture: true,
          // once가 true이면 이벤트리스너가 한번만 실행된다.
          once: true
        })
      );

      // 버튼을 클릭하면 콘솔에 Click!!!이라고 뜬다.
      // once가 true이기 때문에 많이 눌러도 한번만 뜬다.
      button.addEventListener(
        "click",
        () => {
          console.log("Click!!!");
        },
        {
          once: true
        }
      );
```

- 버블링과 캡쳐링의 차이가 어떤건지 아무리 찾아봐도 모르겠다..........
