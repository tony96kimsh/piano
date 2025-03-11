# Simple piano & Pitch monitor
![Screenshot 2025-03-10 at 8 17 31 PM](https://github.com/user-attachments/assets/a0df9af0-6a55-4861-9a79-3a20204fbcb9)


- [사이트 링크](https://piano-iota-murex.vercel.app/)
- [앱 소개 구글 슬라이드](https://docs.google.com/presentation/d/e/2PACX-1vSvQx04pRwtseESdSwdGcWvmq9IO26GGf8-MWkcKqvrb9Ua6_Hzmsut6-OwO6teM-2RqkiPLTFd1xY9/pub?start=false&loop=false&delayms=3000)


## 제작동기
- 간단하게 악보를 읽을 때 피아노 어플을 사용하였는데, 건반사이즈가 작아서 사용에 불편함이 있었다.
- 노래의 음을 알고 싶을 때, pitch monitor(음 시각화) 앱을 사용했는데, 피아노 어플과 같이 쓸 수 없어서 불편했다.
- 두 가지 기능이 합쳐진 심플한 피아노 & 음 모니터 앱을 만들기로 결심했다.

## 기능소개
- 클릭과 키보드로 간단하게 피아노를 칠 수 있는 웹 사이트
- (추후 진행 예정) 녹음되는 음을 시각화 기능 제공 - 예시 링크

## 코드 소개 - 클릭 및 키보드 스크립트
``` js
function playNote(noteId) {
  let key = document.getElementById(noteId);
  if (key) {
    key.classList.add("active"); // 눌린 효과 (CSS 필요)
    let audio = new Audio(`piano/${noteId}.mp3`);
    audio
      .play()
      .catch((error) => console.error("Playback error:", error));

    // 일정 시간 후 효과 제거
    setTimeout(() => key.classList.remove("active"), 150);
  }
}

// 마우스 클릭 이벤트
document.querySelectorAll(".key-wh, .key-bk").forEach((key) => {
  key.addEventListener("click", () => playNote(key.id));
});

// 키보드 입력 이벤트
document.addEventListener("keydown", (event) => {
  let noteId =
    keyMap[event.key.toLowerCase()] || sharpKeyMap[event.key];
  if (noteId) playNote(noteId);
});
});
```
### reference
- 피아노 소리 (https://github.com/fuhton/piano-mp3/tree/master)
- 피아노 사진 (https://unsplash.com/photos/music-note-on-brown-piano-MlhJNEUQpBs)
