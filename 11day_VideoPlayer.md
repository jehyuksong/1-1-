# 1일 1프로젝트 (11일차 Video Player)

- 프로젝트 강좌에 있는 내용말고도 따로 찾아보면서 **키보드를 이용해서**  `재생`, `일시정지`, `앞으로 이동`, `뒤로 이동`, `전체화면`을 할 수 있는 기능을 구현했다.

```jsx
/* 요소 가져오기 */
const player = document.querySelector(".player");
const video = player.querySelector(".viewer");
const progress = player.querySelector(".progress");
const progressBar = player.querySelector(".progress__filled");
const toggle = player.querySelector(".toggle");
const skipButtons = player.querySelectorAll("[data-skip]");
const ranges = player.querySelectorAll(".player__slider");

/* 함수 만들기 */
// 재생버튼 , video가 정지상태면 play되고, 그렇지 않으면 pause됨.
const togglePlay = () => {
  const method = video.paused ? "play" : "pause";
  video[method]();
};

// 버튼바꾸기 , video가 정지상태면 ► , 재생 상태면 ❚ ❚ 모양으로 바뀜.
const updateButton = (e) => {
  const icon = e.target.paused ? "►" : "❚ ❚";
  return (toggle.textContent = icon);
};

// 스킵버튼 , 비디오의 현재 재생시간이 target 요소의 dataset만큼 스킵된다.
const skip = (e) => {
  video.currentTime += parseFloat(e.target.dataset.skip);
};

// 레인지를 설정하면 타깃의 이름에 설정값이 적용된다.
// e.target.name이 volume이면 value가 volume에 적용되어 볼륨조절이 가능하고,
// e.target.name이 playbackRate이면 value가 playbackRate에 적용되어 재생속도조절이 가능해진다.
const handleRangeUpdate = (e) => {
  video[e.target.name] = e.target.value;
};

// 재생바가 재생시간에 맞게 움직인다.
const handleProgress = () => {
  const percent = (video.currentTime / video.duration) * 100;
  progressBar.style.flexBasis = `${percent}%`;
};

// 재생시간을 클릭으로 설정할 수 있다.
const scrub = (e) => {
  const scrubTime = (e.offsetX / progress.offsetWidth) * video.duration;
  video.currentTime = scrubTime;
};

// 스페이스바로 재생,정지를 할 수 있다.
// 오른쪽 방향키로 10초 앞으로 이동할 수 있다.
// 왼쪽 방향키로 10초 뒤로 이동할 수 있다.
const keyControl = (e) => {
  if (e.key === " ") {
    const method = video.paused ? "play" : "pause";
    video[method]();
  } else if (e.key === "ArrowRight") {
    video.currentTime += 10;
  } else if (e.key === "ArrowLeft") {
    video.currentTime -= 10;
  }
};

// 전체화면인지 체크할 변수를 만든다.
let fullCheck = 2;
// f,F,ㄹ 을 눌렀을 때 fullCheck++가 된다.
// fullCheck이 홀수이면 전체화면으로 바뀌고,
// fullCheck이 짝수이면 전체화면이 해제된다.
const makeFullScreen = (e) => {
  if (e.key === "f" || e.key === "ㄹ" || e.key === "F") {
    fullCheck++;
    console.log(fullCheck);
  }
  if (fullCheck % 2 === 1) {
    return video.classList.add("fullscreen");
  } else {
    return video.classList.remove("fullscreen");
  }
};

/* 이벤트 설정 */
// 비디오 화면을 클릭했을 때 togglePlay 함수가 실행된다.
video.addEventListener("click", togglePlay);
// 키를 눌렀을 때 toggleKeyPlay 함수가 실행된다. 스페이스바에만 작동하게 설정되어있다.
window.addEventListener("keydown", keyControl);
// 키를 눌렀을 때 makeFullScreen 함수가 실행된다. f,F,ㄹ에만 작동하게 설정되어있다.
window.addEventListener("keypress", makeFullScreen);

// 비디오가 재생됐을 때 updataButton 함수가 실행된다.
video.addEventListener("play", updateButton);
// 비디오가 일시정지 됐을 때도 updateButton 함수가 실행된다.
video.addEventListener("pause", updateButton);
// 비디오의 시간이 업데이트되면 handleProgress 함수가 실행된다.
video.addEventListener("timeupdate", handleProgress);

// 재생,일시정지 버튼을 클릭했을 때 togglePlay 함수가 실행된다.
toggle.addEventListener("click", togglePlay);

// 스킵버튼을 누르면 skip 함수가 실행된다.
skipButtons.forEach((button) => button.addEventListener("click", skip));

// 레인지를 바꾸거나 마우스가 이동되면 handleRangeUpdate 함수가 실행된다.
ranges.forEach((range) => range.addEventListener("change", handleRangeUpdate));
ranges.forEach((range) =>
  range.addEventListener("mousemove", handleRangeUpdate)
);

// mousedown 변수를 설정해준다.
let mousedown = false;
// 재생바를 클릭하면 scrub 함수가 실행된다.
progress.addEventListener("click", scrub);
// 마우스를 움직일 때 마우스가 눌렸는지 확인하고 scrub함수가 실행된다.
progress.addEventListener("mousemove", (e) => mousedown && scrub(e));
// 마우스가 눌렸을 때 mousedown은 true가 되고, 왼쪽 버튼에서 손을 떼면 mousedown은 false가 된다.
progress.addEventListener("mousedown", () => (mousedown = true));
progress.addEventListener("mouseup", () => (mousedown = false));
```
