# Tech Interview Quiz

퀴즈를 통해 기술 면접을 준비해봐요

[퀴즈 풀어보기](https://gumball12.github.io/tech-interview-quiz)

[퀴즈 추가하기](https://github.com/Gumball12/tech-interview-quiz-items/issues)

## 설치하기

```sh
# 이 리포지토리를 clone 한 다음
git clone https://github.com/Gumball12/tech-interview-quiz.git

# dependencies를 설치합니다
yarn

# 이후 local server를 실행합니다
yarn serve

# build는 아래의 명령을 통해 가능합니다
yarn build
```

## 커스텀 퀴즈

`/public/quiz.yml` 파일을 통해 local server에서 퀴즈를 임의로 만들어볼 수 있어요

퀴즈는 다음과 같이 두 개의 방식으로 정의가 가능합니다

```yml
# 타입 1
-
  - 제목
  - |
    # 내용
    
    마크다운을 지원해요

# 타입 2
- ['제목', '내용']
```

퀴즈의 제목과 내용은 마크다운을 지원해요
