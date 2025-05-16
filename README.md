# ✨ HODU 프로젝트 소개🐱

웹 표준, 유지보수성, 접근성을 고려한 퍼블리싱 프로젝트입니다.  
**시멘틱 마크업, CSS 설계, 반응형 대응, 인터랙션 구현 등** 다양한 측면에서 실무 역량을 표현하고자 했습니다.

> 🔗 **배포 링크**: [https://creative-entremet-af17b3.netlify.app/](https://creative-entremet-af17b3.netlify.app/)

---

## ✅ 주요 구현 포인트

### 1. ✅ 시멘틱 마크업

HTML5 시멘틱 태그(`header`, `main`, `section`, `footer`, `article` 등)를 적극적으로 활용하여 **의미 있는 구조와 SEO 친화적인 마크업**을 구성했습니다.

```html
<header class="site-header">
  <nav class="global-nav">
    <ul>
      <li><a href="#subscribe">구독</a></li>
      <li><a href="#contact">문의</a></li>
    </ul>
  </nav>
</header>
```

---

### 2. 🧏 웹 접근성을 위한 `text-ir` 기법 적용

스크린리더 사용자도 정보를 인식할 수 있도록 `text-ir` 기법을 사용하여 시각적으로는 숨기되 접근성은 유지했습니다.

```css
.text-ir {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

```html
<h1 class="text-ir">Creative 프로젝트 접근성 고려 타이틀</h1>
```

> 📌 **웹 접근성**을 고려하여 **스크린리더 사용자**에게도 정보를 제공할 수 있도록 처리했습니다.

---

### 3. 🧑‍💻 CSS 파일 구조

프로젝트의 **유지보수성을 높이기 위해 CSS 파일을 여러 개로 분리**하여 관리하고, `@import`를 활용하여 필요한 파일들을 불러왔습니다.

- **`reset.css`**: 기본 스타일 초기화
- **`layout.css`**: 레이아웃 관련 스타일
- **`main.css`**: 주요 스타일
- **`popup.css`**: 팝업 관련 스타일

```css
@import url(//spoqa.github.io/spoqa-han-sans/css/SpoqaHanSansNeo.css);
@import url('./reset.css');
@import url('./layout.css');
@import url('./main.css');
@import url('./popup.css');
```

> 📌 **파일 분리와 `@import` 활용**으로 **유지보수성 및 코드 가독성**을 향상시켰습니다.

---

### 4. 🎨 CSS 변수(`:root`)와 `rem` 단위 통일

CSS는 유지보수성과 일관성을 높이기 위해 다음과 같은 방법을 사용했습니다:

- `:root`에 변수 등록하여 **컬러 일괄 관리**
- 모든 여백/폰트/패딩 등의 단위를 `rem`으로 통일해 **반응형 기반 설계 용이성 확보**

```css
:root {
  --main-black:#000000;
  --color-primary:#D97652;
  --color-secondary:#263140;
}
```

---

### 5. 📛 케밥 케이스(kebab-case) 네이밍

클래스명은 `kebab-case`로 통일하여 **가독성 높고 일관된 코드 스타일**을 유지했습니다.

```html
ul class="container gallery-banner-wrap">
  <li class="img-wrap"><img src="./src/img/img_1.png" alt="Hodu on a cat tower"></li>
  <li class="img-wrap"><img src="./src/img/img_2.png" alt="Back of Hodu’s head"></li>
  <li class="img-wrap"><img src="./src/img/img_3.png" alt="Hodu looking at me"></li>
</ul>
```

---

### 6. 🧩 모든 해상도 대응을 위한 `clamp()` 활용

브레이크포인트 없이도 자연스러운 반응형 구성을 위해 CSS `clamp()`를 적극 활용했습니다.

#### ✅ 예시: 구독 입력창

```css
.subscribe form .input-box-wrap input {
  font-size: 1.6rem;
  width: clamp(40rem, 35.6vw, 53rem);
  padding: 2rem 14rem 2rem 6.8rem;
  border-radius: 6rem;
  background-color: var(--color-white);
  position: relative;
  border: none;
}
```

> 📌 화면 크기에 따라 유동적으로 변화하면서도 최소/최대값을 제어하여 깨지지 않는 레이아웃을 구성했습니다.

---

### 7. ⚙️ `<dialog>` 모달 및 GNB 스크롤 인터랙션

- **HTML5 `<dialog>` 요소 사용**으로 팝업 구현
- `.showModal()` 및 `.close()` 메서드로 모달 제어
- 팝업은 간단하고 직관적인 코드로 구현했으며 접근성도 기본 반영됨

```html
<button class="btn primary-btn" type="button" onclick="subscribe()">Subscribe</button>
<dialog>
  <article class="popup-wrap">
    <h2 class="text-ir">Thank you Subscribe</h2>
    <div class="popup-content">
      <p class="primary-font">Thank you!</p>
      <p>Lorem Ipsum is simply dummy text of the printing industry.</p>
      <button class="btn primary-btn close-pop-btn" onclick="popClose()">OK! I Love HODU</button>
    </div>
  </article>
</dialog>
```

- **스크롤 시 GNB(상단 네비게이션)에 효과 적용**
  - JavaScript로 스크롤 위치를 감지하여 `.scrolled` 클래스를 추가/제거
  - GNB 배경 색 변경 및 그림자 추가 등 시각적 피드백 제공

```js
if(window.scrollY>10){
  document.getElementById('header').classList.add('shadow');
  pageTopBtn.classList.add('show')
}else{
  document.getElementById('header').classList.remove('shadow');
  pageTopBtn.classList.remove('show')
}
```

---

### 8. 🌐 언어 통일성 유지

웹사이트 내 모든 텍스트 요소는 **한 가지 언어(영문)**로 통일하여 사용자 혼란을 최소화하고, 브랜드 이미지의 일관성을 유지하려고 노력했습니다.

- 버튼, 입력 필드, 폼 안내문, 타이틀 등 **전체 UI 텍스트를 영어로 구성**
- `lang="en"` 속성을 `<html>`에 명시하여 **스크린리더와 검색엔진**에서도 정확한 언어 인식 가능하게 처리

```html
<html lang="en">
```

> 📌 UI에서 언어 혼용을 피함으로써 **전반적인 사용자 경험을 매끄럽게 유지**하였습니다.

---

## 🧠 기술 요약

- **HTML5**: 시멘틱 마크업 구성
- **CSS3**: root 변수, clamp, text-ir, rem 통일, 케밥 케이스
- **JavaScript**: scroll 이벤트 기반 GNB 효과, dialog 모달
- **접근성**: 스크린리더 대응 텍스트 처리 및 시멘틱 구조
- **반응형**: clamp 활용, 가변 레이아웃 설계
- **배포**: Netlify

---
