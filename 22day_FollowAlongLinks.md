# 1일 1프로젝트 (22일차 Follow Along Links)

```html
<!-- html -->

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>👀👀👀Follow Along Nav</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <nav>
      <ul class="menu">
        <li><a href="">Home</a></li>
        <li><a href="">Order Status</a></li>
        <li><a href="">Tweets</a></li>
        <li><a href="">Read Our History</a></li>
        <li><a href="">Contact Us</a></li>
      </ul>
    </nav>

    <div class="wrapper">
      <p>
        Lorem ipsum dolor sit amet, <a href="">consectetur</a> adipisicing elit.
        Est <a href="">explicabo</a> unde natus necessitatibus esse obcaecati
        distinctio, aut itaque, qui vitae!
      </p>
      <p>
        Aspernatur sapiente quae sint <a href="">soluta</a> modi, atque
        praesentium laborum pariatur earum <a href="">quaerat</a> cupiditate
        consequuntur facilis ullam dignissimos, aperiam quam veniam.
      </p>
      <p>
        Cum ipsam quod, incidunt sit ex <a href="">tempore</a> placeat maxime
        <a href="">corrupti</a> possimus <a href="">veritatis</a> ipsum fugit
        recusandae est doloremque? Hic, <a href="">quibusdam</a>, nulla.
      </p>
      <p>
        Esse quibusdam, ad, ducimus cupiditate <a href="">nulla</a>, quae magni
        odit <a href="">totam</a> ut consequatur eveniet sunt quam provident
        sapiente dicta neque quod.
      </p>
      <p>
        Aliquam <a href="">dicta</a> sequi culpa fugiat
        <a href="">consequuntur</a> pariatur optio ad minima, maxime
        <a href="">odio</a>, distinctio magni impedit tempore enim repellendus
        <a href="">repudiandae</a> quas!
      </p>
    </div>
  </body>
</html>
```

---

```jsx
// js

      // 모든 링크 태그를 가져온다.
      const triggers = document.querySelectorAll("a");
      // 하이라이트 하는 데 사용할 요소를 만든다.
      const highlight = document.createElement("span");
      // 하이라이트 효과를 담은 css를 적용시킨다.
      highlight.classList.add("highlight");
      // hightlight를 바디에 넣는다.
      document.body.appendChild(highlight);

      // 하이라이트 함수를 만든다.
      function highlightLink() {
        // 마우스가 가르키고 있는 요소의 위치, 크기 등 박스의 모든 요소를 가져온다.
        const linkCoords = this.getBoundingClientRect();

        // 너비,높이,위치 등을 객체로 만들어서 담는다.
        const coords = {
          width: linkCoords.width,
          height: linkCoords.height,
          top: linkCoords.top + window.scrollY,
          left: linkCoords.left + window.scrollX
        };

        // 하이라이트 효과를 각 요소들의 사이즈와 위치에 맞게 적용 시킨다.
        highlight.style.width = `${coords.width}px`;
        highlight.style.height = `${coords.height}px`;
        highlight.style.transform = `translate(${coords.left}px, ${coords.top}px)`;
      }

      // 모든 링크에 마우스를 올리면 highlightLink 함수가 동작한다.
      triggers.forEach(a => a.addEventListener("mouseenter", highlightLink));
```

- absolute 포지션과 임의의 span 태그를 이용해서 이런 효과를 넣을 수 있다는 게 굉장히 놀라웠다.
