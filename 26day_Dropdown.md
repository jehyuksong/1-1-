# 1일 1프로젝트 (26일차 Stripe Follow Along Dropdown)

```jsx
// html

<nav class="top">
      <div class="dropdownBackground">
        <span class="arrow"></span>
      </div>

      <ul class="cool">
        <li>
          <a href="#">About Me</a>
          <div class="dropdown dropdown1">
            <div class="bio">
              <img src="https://logo.clearbit.com/wesbos.com" />
              <p>
                Wes Bos sure does love web development. He teaches things like
                JavaScript, CSS and BBQ. Wait. BBQ isn't part of web
                development. It should be though!
              </p>
            </div>
          </div>
        </li>
        <li>
          <a href="#">Courses</a>
          <ul class="dropdown courses">
            <li>
              <span class="code">RFB</span>
              <a href="https://ReactForBeginners.com">React For Beginners</a>
            </li>
            <li>
              <span class="code">ES6</span>
              <a href="https://ES6.io">ES6 For Everyone</a>
            </li>
            <li>
              <span class="code">NODE</span>
              <a href="https://LearnNode.com">Learn Node</a>
            </li>
            <li>
              <span class="code">STPU</span>
              <a href="https://SublimeTextBook.com">Sublime Text Power User</a>
            </li>
            <li>
              <span class="code">WTF</span>
              <a href="http://Flexbox.io">What The Flexbox?!</a>
            </li>
            <li>
              <span class="code">GRID</span>
              <a href="https://CSSGrid.io">CSS Grid</a>
            </li>
            <li>
              <span class="code">LRX</span>
              <a href="http://LearnRedux.com">Learn Redux</a>
            </li>
            <li>
              <span class="code">CLPU</span>
              <a href="http://CommandLinePowerUser.com"
                >Command Line Power User</a
              >
            </li>
            <li>
              <span class="code">MMD</span>
              <a href="http://MasteringMarkdown.com">Mastering Markdown</a>
            </li>
          </ul>
        </li>
        <li>
          <a href="#">Other Links</a>
          <ul class="dropdown dropdown3">
            <li>
              <a class="button" href="http://twitter.com/wesbos">Twitter</a>
            </li>
            <li>
              <a class="button" href="http://facebook.com/wesbos.developer"
                >Facebook</a
              >
            </li>
            <li><a class="button" href="http://wesbos.com">Blog</a></li>
            <li>
              <a class="button" href="http://wesbos.com/courses"
                >Course Catalog</a
              >
            </li>
          </ul>
        </li>
      </ul>
    </nav>
```

---

```jsx
// js

// html 요소들을 가져온다.
      const triggers = document.querySelectorAll(".cool > li");
      const background = document.querySelector(".dropdownBackground");
      const nav = document.querySelector(".top");

      // mouseenter 이벤트가 발생하면 실행되는 함수
      function handleEnter() {
        // 마우스를 올린 li에 trigger-enter 클래스를 추가한다.
        this.classList.add("trigger-enter");
        // 0.15초 뒤에 trigger-enter-active 클래스를 추가한다.
        setTimeout(
          () =>
            this.classList.contains("trigger-enter") &&
            this.classList.add("trigger-enter-active"),
          150
        );
        // background에 open 클래스를 추가한다.
        background.classList.add("open");

        // 선택된 li에 자식요소들을 가져온다.
        const dropdown = this.querySelector(".dropdown");
        // div요소 사이즈를 측정한다.
        const dropdownCoords = dropdown.getBoundingClientRect();
        const navCoords = nav.getBoundingClientRect();

        // div 요소 사이즈 측정한 것들을 객체로 담는다.
        const coords = {
          height: dropdownCoords.height,
          width: dropdownCoords.width,
          top: dropdownCoords.top - navCoords.top,
          left: dropdownCoords.left - navCoords.left
        };

        // background에 스타일 값을 측정한 값을 기준으로 설정해서 효과를 준다.
        background.style.setProperty("width", `${coords.width}px`);
        background.style.setProperty("height", `${coords.height}px`);
        background.style.setProperty(
          "transform",
          `translate(${coords.left}px, ${coords.top}px)`
        );
      }

      // mouseleave 이벤트가 발동되면 실행되는 함수
      function handleLeave() {
        // li에서 trigger-enter, trigger-enter-active 클래스를 없앤다.
        this.classList.remove("trigger-enter", "trigger-enter-active");
        // background 에서 open 클래스를 없앤다.
        background.classList.remove("open");
      }

      // li에 마우스를 올리면 handleEnter 함수가 실행된다.
      triggers.forEach(trigger =>
        trigger.addEventListener("mouseenter", handleEnter)
      );
      // li에서 마우스를 빼면 handleLeave 함수가 실행된다.
      triggers.forEach(trigger =>
        trigger.addEventListener("mouseleave", handleLeave)
      );
```

- 효과를 줄 때 `getBoundingClientRect()` 함수를 전에 했던 프로젝트에서도 많이 사용하는 것을 보니, div에 효과를 줄 때 효과적으로 사용할 수 있을 것 같다.
