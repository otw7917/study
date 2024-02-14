# Callback

```js
const appDiv = document.getElementById("app");

const button = document.createElement("button");
button.innerHTML = "click";
appDiv.appendChild(button);

const div = document.createElement("div");

appDiv.appendChild(div);

function showCircle(cx, cy, radius, cb) {
  div.style.width = 0;
  div.style.height = 0;
  div.classList.add("circle");
  setTimeout(() => {
    div.style.width = radius * 2 + "px";
    div.style.height = radius * 2 + "px";

    div.addEventListener("transitionend", () => handleTransition(cb));

    div.addEventListener("transitionend", function handler() {
      alert("how many times?");
      cb(div);
      div.removeEventListener("transitionend", handler);
    });
  }, 0);
}

function handleTransition(cb) {
  alert("how many times?");
  console.log("transition over");
  div.removeEventListener("transitionend", handleTransition);
  cb(div);
}

button.addEventListener("click", () =>
  showCircle(150, 150, 100, (div) => {
    div.classList.add("message-ball");
    div.append("안녕하세요!");
  })
);
```

**1번 케이스**

- 콜백함수로 넘겨주기
- 해당 alert 가 두번 작용함 (transition property가 2개여서 두번)

```js
div.addEventListener("transitionend", () => handleTransition(cb));

function handleTransition(cb) {
  alert("how many times?"); // 2번
  console.log("transition over");
  div.removeEventListener("transitionend", handleTransition);
  cb(div);
}
```

**2번 케이스**

- 함수 선언으로 넘겨줌
- 얘는 왜 한번?

```js
div.addEventListener("transitionend", function handler() {
  alert("how many times?");
  cb(div);
  div.removeEventListener("transitionend", handler);
});
```

https://ko.javascript.info/callbacks#ref-107
