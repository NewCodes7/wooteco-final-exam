# 우테코 6기 최종 코테 준비

## [시험 전] 행동 강령
- 메모리 정리
- 자바 컴파일 자바 17 확인하기
- 참고 자료 열어두기: 챗지피티(한국말), 깃허브
- 파일 생성 제대로 안 될 때: https://mosei.tistory.com/entry/Intellij-우클릭-New에-Java-Class-가-안보일-때
- [ ] 와이파이
- [ ] 출석 체크(신분증)
- [ ] 화장실 위치
- [ ] 방해금지모드
- [ ] 당충전, 물 구비
- [ ] 시작 30분 전 이메일 안내 확인
- [ ] 에어팟
- [ ] 리팩토링 리스트, 테스트 코드 리스트 메모 작성

## [구현 전] 행동 강령
- 설계 더욱 세밀하게 하고 들어가기
  - 특히 컨트롤러!!
  - 책임(클래스), 내부 메서드, 자료구조 선택 등
  - 특정 클래스 혹은 책임에 관해 복잡하다면 그 부분만 더 설계하기
- MVC 파일 구조 만들어두기 (흐름 끊김 방지): model, view, controller, util
- 단순화: 복잡해보이더라도 하나씩 하면 된다. 하나에 집중하자!
- 테스트 코드 살피기

## [구현 중] 행동 강령
- 네이밍: 더 신경 써서 하기(내가 헷갈리는 것 방지)
- 멘붕의 순간: 차분히 잘 해결하면 지나간다. 차분히 하자!
- 리팩토링: 리팩토링 사항은 컴퓨터 메모에 적어두자.
- 중간 설계: 중간에 설계 다시 점검하는 것 시간 아끼지 말자.
- 특정 자료 구조 순회: 스트림 고려해라! (지피티 이용)
- GPT: 머리 놓고 쓰면 안 된다!! 확인하고 정신차리고 **_**능동적으로 이용해라!**_**

## [구현 후] 행동 강령
### 리팩토링
- 상수화 작업: chatGPT 적극 활용. 단 확인할 것.
- 테스트코드 작성
- 메서드 분리: 한 가지 일만 하고 있는가?

## 실전 구현 순서
### 준비 (약 40분)
1. 프로젝트 세팅 (시험 유의사항, 로컬로 받아오기, 마음가짐)
2. 리드미 숙지하기
3. 기능 목록 작성하기
4. 전체적인 구조 설계하기
5. 테스트 살펴보기

### 구현 (약 3시간 20분)
6. 폴더 만들기 (model, view, controller, util)
7. 파일 만들기 (InputView, OutputView / MainController / Validator, ExceptionMessage)
8. 사용자 입력 기능 구현 (스켈레톤 코드 이용)
9. 도메인 기능 구현 - 테스트 추가하면 좋을만한, 리팩토링할만한 부분 리스트 작성하기
10. 출력 기능 구현 (출력 형식은 chatGPT 참고)

### 마무리 (최소 20분)
11. 테스트 통과 확인하기, PR 날리기 
12. 리팩토링 - 빠뜨린 기능 없는지 다시 체크, (메서드 라인, 로직 최적화, 상수화, 인덴트 뎁스)
13. 테스트 코드 작성 (컨벤션: test)
14. 소감문 작성
15. 테스트 통과 확인!

## 챗지피티
### 능동적으로 사용해라!! 메서드 하나하나 숙지해라.
- 메서드 이름 추천
- 특정 로직 구현
- 리팩토링 조언
- 테스트 코드 작성
- 각종 에러 해결
- 출력문 형식 구현
- validator 구현


## [학습] 
- static: 메서드가 클래스의 인스턴스와 상관이 없고, 오직 클래스 자체의 상태를 변경하거나 조회하는 역할만 한다면 붙일 것 (주로 유틸리티성 메서드)
- sout: System.out.println() 단축키
- do while: while 내부 코드를 무조건 한 번 실행함. 그 후 반복 조건을 고려함.
````
    do {
        // 실행 코드
    } while (//boolean);
````
---

## 스켈레톤 코드

### [상수] 예외 메시지 enum
```
public enum ExceptionMessage {
    INVALID_NOT_NUMERIC("자연수만 입력 가능합니다."),
    INVALID_OUT_OF_INT_RANGE("입력 범위를 초과하였습니다.");

    public static final String BASE_MESSAGE = "[ERROR] %s";
    private final String message;

    ExceptionMessage(String message, Object... replaces) {
        this.message = String.format(BASE_MESSAGE, String.format(message, replaces));
    }

    public String getMessage() {
        return message;
    }
}
```

### [InputView] 입력값 재요청
```
@FunctionalInterface
interface InputReader {
    String readInput();
}

@FunctionalInterface
interface ValidateReader {
    void validate(String userInput);
}

    public static String getValidatedInput(InputReader inputReader, ValidateReader validateReader, String errorMessage) {
        String userInput;
        while (true) {
            try {
                userInput = inputReader.readInput();
                validateReader.validate(userInput);
                break;
            } catch (IllegalArgumentException e) {
                System.out.println(errorMessage);
            }
        }
        return userInput;
    }
    
    public static String readOOO() {
        System.out.println("OOO");
        return Console.readLine();
    }
    
    public static String getValidatedOOO() {
        return getValidatedInput(InputView::readOOO, Validator::validateOOO, "[ERROR] OOO.");
    }
```

### [OutputView] 기본
```
    public static void printError(Exception error) {
        System.out.println(error.getMessage());
    }

    public static void print(String message) {
        System.out.print(message);
    }

    public static void println(String message) {
        System.out.println(message);
    }

    public static void printEnter() {
        System.out.println();
    }
```

### To do list
- [x] 필요한 스켈레톤 코드 수집
- [x] 부족했다고 생각한 부분 다시 보기
- [x] 몇몇 코드 최적화
- [x] ! 공통적인 클리셰 및 행동 강령 추출 !
- [ ] 각 코치를 자료구조가 아닌 인스턴스로 관리하는 방법? 난 그동안 여러 인스턴스를 잘 활용하지 않은 듯
- [ ] 메모리 관리!! IntelliJ 멈추는 현상 해결하기
- [ ] mvc패턴 학습.. 근데 이게 필수인 건 아니다!
- [ ] 테스트코드 추가
- [ ] 메뉴 추천 코드 찾기 힘드네... Coach 인스턴스를 적극 활용해보고픈데. 


### To do list
- [x] 리팩토링
  - [x] enum 클래스 분리
  - [x] 컨트롤러 분리
  - [x] 각 파일 최적화 && 메서드 라인 길이 점검
  - [x] view 제대로 책임 분배되었는지
  - [x] rematch 관련 로직 점검
  - [x] 재매칭 에러문 출력 후 입력 다시 받기 && 입력다시받는 거 메서드 추상화
- [ ] 파일 입출력 학습
- [ ] 60 !! 다른 프로젝트 설계만 해보기 
  - [ ] 테스트 코드 살펴보기 (필요하다면 gpt)
- [x] 5 커밋 관련 깃허브 명령어 정리
- [x] 5 chatGPT 이용 관련 행동 강령 정리 - 너무 의존해서도 안 된다.
- [x] 1 intelliJ 파일별 이동 단축키?
- [x] 5 리팩토링 시간분배
- [x] 피드백 - 재매칭 입력받는 부분에서 오래 걸림
- [ ] 다른 사람 코드 참고
- [x] 40 !! 테스트 코드 추가

- [x] 10 사용자 입력값 다시 받는 메서드 -> 스켈레톤 코드 작성하기
- [x] 10 실전에서의 구현 순서 정리하기
- [x] 10 테스트 코드 살펴보기
- [x] 15 우테코 피드백 확인

- [x] 60 소감문 작성하기
- [ ] 30 행동강령 숙지하기

