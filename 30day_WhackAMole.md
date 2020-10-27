# 1일 1프로젝트 (30일차 Whack A Mole)

```html
<!-- html -->

<h1>Whack-a-mole! <span class="score">0</span></h1>
    <button onClick="startGame()">Start!</button>

    <div class="game">
      <div class="hole hole1">
        <div class="mole"></div>
      </div>
      <div class="hole hole2">
        <div class="mole"></div>
      </div>
      <div class="hole hole3">
        <div class="mole"></div>
      </div>
      <div class="hole hole4">
        <div class="mole"></div>
      </div>
      <div class="hole hole5">
        <div class="mole"></div>
      </div>
      <div class="hole hole6">
        <div class="mole"></div>
      </div>
    </div>
```

---

```jsx
// js

// 요소들을 가져오고, 변수들을 선언한다.
      const holes = document.querySelectorAll(".hole");
      const scoreBoard = document.querySelector(".score");
      const moles = document.querySelectorAll(".mole");
      let lastHole;
      let timeUp = false;
      let score = 0;

      // 랜덤시간을 만드는 함수이다.
      function randomTime(min, max) {
        // 0.2초에서 1초 사이의 랜덤시간이 나오게끔 설정한다.
        return Math.round(Math.random() * (max - min) + min);
      }

      // 랜덤으로 구멍을 설정한다.
      function randomHole(holes) {
        // 홀의 개수로 설정
        const idx = Math.floor(Math.random() * holes.length);
        const hole = holes[idx];
        // 만약 구멍이 가장최근에 나온 구멍과 같다면 randomeHole 함수를 다시 실행한다.
        if (hole === lastHole) {
          console.log("Ah nah thats the same one bud");
          return randomHole(holes);
        }
        // 지금 나온 구멍을 lastHole 변수에 담는다.
        lastHole = hole;
        // 구멍을 리턴한다.
        return hole;
      }

      // 두더지들이 랜덤으로 튀어오르게 하는 함수이다.
      function peep() {
        // 시간은 0.2초에서 1초로 랜덤하게 설정되게끔 만들어 놓은 함수를 사용한다.
        const time = randomTime(200, 1000);
        // 구멍도 랜덤하게 설정되게끔 만들어 놓은 함수를 사용한다.
        const hole = randomHole(holes);
        // 구멍에 up 클래스를 추가한다.
        hole.classList.add("up");
        // 시간이 되면 hole에 up클래스를 지우고, 만약 게임시간이 남았다면 다시 peep 함수를 실행한다.
        setTimeout(() => {
          hole.classList.remove("up");
          if (!timeUp) peep();
        }, time);
      }

      // 게임시작 함수를 만든다.
      function startGame() {
        // 스코어보드를 초기화한다.
        scoreBoard.textContent = 0;
        // timeUp =false로 만든다.
        timeUp = false;
        // 스코어를 0으로 만든다.
        score = 0;
        // 두더지들이 랜덤으로 나오게 한다.
        peep();
        // 시간이 10초가 흐르면 timeUp = true로 만든다.
        setTimeout(() => (timeUp = true), 10000);
      }

      // 두더지를 잡는 함수이다.
      function bonk(e) {
        // 만약 두더지가 없다면 그대로 리턴한다.
        if (!e.isTrusted) return; // cheater!
        // 스코어를 올린다.
        score++;
        // 부모요소의 up 이라는 클래스를 제거한다.
        this.parentNode.classList.remove("up");
        // 스코어보드에 스코어를 최신화한다.
        scoreBoard.textContent = score;
      }

      // 두더지를 클릭하면 bonk함수가 실행된다.
      moles.forEach(mole => mole.addEventListener("click", bonk));
```

- 마지막 프로젝트는 재미있고 친근한 두더지 잡기였다! 1일 1프로젝트 30일차까지 전부 끝!!!
