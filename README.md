## UDEMy - Svelte 3 | Crash Course - Movie App with Svelte JS [2020]

<pre>
pages 폴더에 페이지 별로 svelte 파일을 만들고
필요한 컴포넌트는 components 폴더에 있는 svelte 파일들을 불러와
레고 조립하듯이 하나 하나 조립해서 만들어서 완성하는 영화 검색 사이트

스벨트 파일 하나에 HTML, CSS, JS가 하나에 뭉쳐서 있어서
바로 바로 필요한 부분을 수정할 수 있는 점이 매우 좋음.

</pre>

- 배포: netlify
  <https://chosangho.netlify.app>
- TMDB movie api 사용
  <https://www.themoviedb.org/?language=ko>

  ![플레이 화면](/screenshot/screen.gif)
  ![자격증](/screenshot/certificate.jpg)

## 소스 사용법

<pre>
1. 소스 다운로드 또는 git clone으로 가져오기
2. https://www.themoviedb.org 사이트로 이동 후 회원 가입을 하고 TMDB에서 제공해주는 영화 API 키를 복사
3. vscode에서 다운받은 폴더를 열고 .env.example 파일을 .env로 이름을 변경한 뒤에 아래와 같은 형식으로 API_KEY의 값을 입력
API_KEY=4a17a20b247589ceae416940a8(TMDB에서 가져온 API의 키를 붙여넣으면 됨)
4. 터미널을 켜고 npm install 또는 npm i 명령어 실행(node_modules 설치됨)
5. 터미널 창에서 npm run dev 실행 후에 아래와 같은 글자가 뜬다면

  Your application is ready~! 🚀

  - Local:      http://localhost:8080
  - Network:    Add `--host` to expose

6. 크롬 브라우저 켜고 http://localhost:8080 실행
(간혹 다른 프로그램에서 8080 포트를 사용중이라면 포트 번호가
다른 번호로 나올 수 있으니 포트 번호만 유의해서 실행 요함.)
</pre>
