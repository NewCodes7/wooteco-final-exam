# 우테코 6기 최종 코테 준비

## [시험 전] 행동 강령
- 메모리 정리
- 자바 컴파일 자바 17 확인하기
- 참고 자료 열어두기: 챗지피티, 깃허브
- 파일 생성 제대로 안 될 때: https://mosei.tistory.com/entry/Intellij-우클릭-New에-Java-Class-가-안보일-때
- [ ] 와이파이
- [ ] 출석 체크(신분증)
- [ ] 화장실 위치
- [ ] 방해금지모드
- [ ] 당충전, 물 구비
- [ ] 시작 30분 전 이메일 안내 확인
- [ ] 에어팟

## [구현 전] 행동 강령
- 전체적으로 설계해두고 들어가기: 책임(클래스), 내부 메서드, 자료구조 선택 등
- MVC 파일 구조 만들어두기 (흐름 끊김 방지): model, view, controller, util
- 단순화: 복잡해보이더라도 하나씩 하면 된다. 하나에 집중하자!

## [구현 중] 행동 강령
- 네이밍: 더 신경 써서 하기(내가 헷갈리는 것 방지)
- 멘붕의 순간: 차분히 잘 해결하면 지나간다. 차분히 하자!

## [구현 후] 행동 강령
### 리팩토링
- 상수화 작업: chatGPT 적극 활용. 단 확인할 것.
- 테스트코드 작성
- 메서드 분리: 한 가지 일만 하고 있는가?

### 기타
- 미리 작성해둔 소감문에 조금 더하기
- 미리 PR 날리기


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

### [컨트롤러] 입력값 재요청
```
    private void manage__() {
        while(true) {
            try {
                // 입력 요청 메서드
                break;
            } catch (IllegalArgumentException e) {
                System.out.println(e.getMessage());
            }
        }
    }
```


### To do list
- [x] 필요한 스켈레톤 코드 수집
- [ ] 부족했다고 생각한 부분 다시 보기
- [ ] 몇몇 코드 최적화
- [ ] ! 공통적인 클리셰 및 행동 강령 추출 !
- [ ] 각 코치를 자료구조가 아닌 인스턴스로 관리하는 방법? 난 그동안 여러 인스턴스를 잘 활용하지 않은 듯
- [ ] 메모리 관리!! IntelliJ 멈추는 현상 해결하기
- [ ] mvc패턴 학습.. 근데 이게 필수인 건 아니다!
- [ ] 테스트코드 추가
- [ ] 메뉴 추천 코드 찾기 힘드네... Coach 인스턴스를 적극 활용해보고픈데. 

