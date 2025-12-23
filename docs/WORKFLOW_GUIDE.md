# 🎓 깃허브 액션(GitHub Actions) 워크플로우 가이드

이 문서는 **`marp-pages.yml`** 파일이 도대체 무슨 일을 하는지, 대학생도 이해할 수 잇도록 쉽게 풀어서 설명한 가이드입니다.

이 파일은 **"자동화된 공장 라인"**을 만드는 설계도라고 생각하면 됩니다. 우리가 PPT(마크다운)를 고치고 저장하면, 이 공장이 자동으로 돌아가서 예쁜 웹사이트로 딱 만들어줍니다. 😎

---

## 1. 언제 공장이 돌아가나요? (Trigger)

```yaml
on:
  push:
    branches:
      - main
    paths:
      - 'docs/presentation.md'
      - '.github/workflows/marp-pages.yml'
```

- **`on: push`**: 누군가가 코드를 **밀어 넣었을 때(Push)** 실행됩니다.
- **`branches: main`**: 아무 데나 올린다고 되는 게 아니고, **`main` 브랜치**에 올렸을 때만 작동합니다.
- **`paths`**: 특히, **발표 자료(`presentation.md`)**나 **이 설정 파일(`marp-pages.yml`)**이 변경되었을 때만 실행됩니다. (다른 잡다한 파일 고쳤을 땐 안 돌아가서 자원을 아낍니다!)

---

## 2. 첫 번째 공정: 빌드 (Build) 🏗️

이 단계는 재료를 다듬어서 완성품(HTML 파일)을 만드는 과정입니다.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest  # 공장 컴퓨터는 '우분투(리눅스)'를 씁니다.
```

### 단계별 설명 (Steps)

1.  **`Checkout code`**
    - 공장 컴퓨터에 우리 프로젝트 코드를 **내려받습니다**. (재료 준비)

2.  **`Install Marp CLI`** ✨ **(중요!)**
    ```yaml
    run: npm install -g @marp-team/marp-cli
    ```
    - **Marp**는 마크다운을 PPT로 바꿔주는 도구입니다.
    - 공장 컴퓨터에는 Marp가 안 깔려있어서, `npm`(자바스크립트 패키지 관리자)을 통해 **직접 설치**해줍니다.

3.  **`Build Presentation`**
    ```yaml
    run: marp docs/presentation.md -o public/index.html --theme gaia
    ```
    - 설치한 Marp를 이용해서 변환을 수행합니다.
    - `docs/presentation.md` (재료) ➡️ `public/index.html` (완성품)
    - `--theme gaia`: **Gaia**라는 예쁜 테마를 입힙니다.

4.  **`Upload metadata`**
    - 만들어진 `public` 폴더(HTML 파일이 들어있음)를 **잠시 보관함(Artifact)에 업로드**해둡니다. 다음 공정으로 넘겨주기 위해서요!

---

## 3. 두 번째 공정: 배포 (Deploy) 🚀

이 단계는 완성된 HTML 파일을 인터넷 세상(GitHub Pages)에 공개하는 과정입니다.

```yaml
  deploy:
    needs: build  # '빌드' 공정이 성공적으로 끝나야만 시작합니다.
    environment:
      name: github-pages
```

### 단계별 설명 (Steps)

1.  **`Download metadata`**
    - 아까 '빌드' 공정에서 보관함에 넣어둔 `public` 폴더를 다시 꺼내옵니다.

2.  **`Upload artifact` (Pages 전용)**
    - GitHub Pages가 이해할 수 있는 특별한 형태로 포장해서 업로드합니다.

3.  **`Deploy to GitHub Pages`**
    - **최종 공개!** 🎉
    - 이제 `https://[아이디].github.io/[저장소이름]/` 주소로 접속하면 우리가 만든 PPT가 웹사이트로 뜹니다.

---

## 💡 요약

1. **트리거**: `mk` 파일이나 설정 파일을 수정해서 Push하면...
2. **빌드**: 리눅스 컴퓨터가 켜지고 ➡️ Marp를 설치해서 ➡️ HTML로 변환하고 ➡️ 보관함에 넣습니다.
3. **배포**: 보관함에서 꺼내서 ➡️ GitHub Pages 서버로 전송합니다.
4. **결과**: 나만의 멋진 웹 프레젠테이션 완성! 🥳
