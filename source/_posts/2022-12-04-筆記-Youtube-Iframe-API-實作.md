---
title: '2022-12-04-[筆記]Youtube Iframe API 實作'
tags:
  - JavaScript
  - Youtube
categories:
  - JavaScript
abbrlink: 1052275469
---
前言：
紀錄一下這次開發 Youtube Iframe API 實作遇到一些小問題

<!-- more -->
---
參考資料：
[Youtube Iframe API 常用功能
](https://www.letswrite.tw/youtube-iframe-api/)
[YouTube JavaScript API not triggering onYouTubeIframeAPIReady](https://vector.cool/youtube-javascript-api-not-triggering-onyoutubeiframeapiready/)

---

### 需求

- 影片自動播放，並能從外部控制聲音開啟或靜音（示意圖如下）

![示意圖](https://i.imgur.com/FOmueJu.png)

- 同個頁面需要各別控制影片靜音、開啟聲音

### 實作遇到問題點

- youtubeIframe API 全域只能載入一次
- 靜音時無法自動播放

### 解決方法

1. 先建立 `onYouTubeIframeAPIReady` function
2. 當影片載入後，在 onReady 方法中呼叫 `onPlayerReady`
3. 將影片先關靜音才能自動播放
4. 如果需要多個 `onYouTubeIframeAPIReady` 則必須自己先建立一個實體，才能各別控制

```jsx
 var player;
function onYouTubeIframeAPIReady() {
  // 一般使用 影片的id寫在js裡
  player = new YT.Player("video0", {
    events: {
      onReady: onPlayerReady,
    },
  });
}
function onPlayerReady(e) {
  // 檢查 YT object 是否已存在全域
  checkYT();
  // 為確保瀏覽器上可以自動播放，要把影片調成靜音
  e.target.mute().playVideo();
  const toggleVoice = document.querySelector(".toggleVoice");
  toggleVoice.addEventListener("click", () => {
    if (e.target.isMuted()) {
      toggleVoice.src = "./content/assets/img/voice.svg";
      e.target.unMute().playVideo();
    } else {
      toggleVoice.src = "./content/assets/img/novoice.svg";
      e.target.mute().playVideo();
    }
  });
}

var player2;
function yt_init() {
  player2 = new YT.Player("video1", {
    events: {
      onReady: onPlayerReady1,
    },
  });
}

var checkYT = () => {
  if (YT && YT.loaded) {
    yt_init()
  }
};

function onPlayerReady1(e) {
  // 為確保瀏覽器上可以自動播放，要把影片調成靜音
  e.target.mute().playVideo();
  const toggleVoice1 = document.querySelector(".toggleVoice1");
  toggleVoice1.addEventListener("click", () => {
    if (e.target.isMuted()) {
      toggleVoice1.src = "./content/assets/img/voice.svg";
      e.target.unMute().playVideo();
    } else {
      toggleVoice1.src = "./content/assets/img/novoice.svg";
      e.target.mute().playVideo();
    }
  });
}
```

1. 必須要注意 `iframe` 連結必須加上 enablejsapi 參數 且 `allow` 屬性 也必須帶上 `autoplay`

```jsx
<iframe
    src="https://www.youtube.com/embed/OBH26hA6GLA?enablejsapi=1"
    title="YouTube video player"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
    id="video0"
  ></iframe>
```
