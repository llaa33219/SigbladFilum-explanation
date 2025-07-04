# SigbladFilum 공식 문서 v1.0

## 📊 옵션

* 이름: **SigbladFilum**
* 형식: 스프레드시트 기반 프로그래밍 언어
* 시작 위치: **A1** 셀
* 와드 언어 같이 가볍게 동작
* 상태 저장: 변수 없음, 셀이 가치 가정

---
## SigbladFilum 철학

SigbladFilum은 복잡한 추상화나 변수 개념 없이, 셀 단위 명령과 명시적 흐름만으로 구성된 스프레드시트 기반 프로그래밍 언어이다.  
이 언어는 다음 6가지 철학을 기반으로 한다:

1. **단순함을 최우선으로**  
   - 복잡한 문법은 배제한다.  
   - 한 셀에는 하나의 명령만, 흐름은 명시적으로 지정.

2. **직관적 실행 흐름**  
   - 실행 순서는 셀에 적힌 대로 따라간다.  
   - 눈으로 따라갈 수 있는 흐름이 가장 중요하다.

3. **셀은 모든 것이다**  
   - SigbladFilum에는 변수, 메모리, 출력 영역 같은 별도의 구조가 없다.  
   - 모든 저장, 출력, 상태의 표현은 셀을 통해 직접 이루어진다.  
   - 셀 하나가 곧 코드이자 값이며, 기록이자 결과이다.

4. **실행된 셀은 과거다**  
   - 초기화 없이, 실행은 그대로 이어지며 다음으로 넘어간다.
   - 실행이 끝나더라도 모든 셀은 현재 상태가 보존된다.

5. **보이는 것이 전부다**  
   - 숨겨진 로직이나 암시적 규칙은 없다.  
   - 모든 것은 셀에 명시되어 있어야 한다.

6. **단순함에서 피어나는 창의성**  
   - **극도로 단순하게 설계된 환경 속에서**, 사용자는 셀을 조합해 창의적인 흐름과 결과를 만들어낸다.  
   - SigbladFilum은 복잡함을 허용하지 않지만, 그 단순함 자체가 무한한 가능성의 출발점이 된다.

---

## ✨ 언어 차례

**SigbladFilum**은 다수의 명령어가 다음 셀의 위치를 명시해, 각 셀이 하나의 명령을 가지는 구조이다. 기본적으로 실행 중 cell은 편집이 불가능하다

정확한 명령의 형식은:

```
<명령어(인자)> [다음 셀]
```

---

## ⚖️ 기본 명령어 명세

| 명령어 | 형식 | 설명 |
|-----------|--------|--------|
| `change` | `change(셀, "값") [다음]`<br>`change(셀1, 셀2) [다음]` | 셀에 값 쓰기 / 다른 셀 값 복사 |
| `if`     | `if(셀) [참], [거짓]` | 셀의 내용이 비어 있지 않으면 [참]으로, 비어 있으면 [거짓]으로 이동 |
| `goto`   | `goto [셀]` | 무조건 해당 셀로 이동 |
| `input`  | `input(셀) [다음]` | 셀을 사용자 입력이 가능한 셀로 전환 |
| `wait`   | `wait(밀리초) [다음]` | 지정한 시간(ms) 동안 대기한 뒤 다음 셀로 이동 |
| `end`    | `end` | 프로그램 종료 |

## ⚖️ 기본 연산 명세

SigbladFilum은 단순한 수식 기반 문법을 사용해 셀 내부에서 기본 연산을 수행할 수 있다. 연산은 주로 `change`, `if` 명령어의 인자에서 사용되며, 다음과 같은 형태와 규칙을 따른다.

### 📌 지원 연산자 목록

| 연산자 | 설명               | 예시                         |
|--------|--------------------|------------------------------|
| `+`    | 숫자 덧셈 / 문자열 연결 | `A1 + 5`, `"Hi" + B1`       |
| `-`    | 숫자 뺄셈           | `10 - A2`                    |
| `*`    | 숫자 곱셈 / 문자열 반복 | `A1 * 3`, `"*"` `*` `4`     |
| `/`    | 정수 나눗셈 (버림)  | `A1 / 2`                     |
| `=`    | 값 비교 (같음)     | `A1 = "5"`                   |
| `!=`   | 값 비교 (같지 않음) | `A1 != B1`                   |
| `<`    | 비교 (미만)        | `A1 < 10`                    |
| `>`    | 비교 (초과)        | `B2 > A3`                    |

---

### ⚠️ 연산 자료형 규칙

- `+`
  - 숫자 + 숫자 → 덧셈  
  - 문자열 포함 → 문자열 연결 (`"Hi" + 3` → `"Hi3"`)

- `-`, `/`
  - 숫자 + 숫자만 가능  
  - 문자열이 포함되면 **에러 발생**

- `*`
  - 숫자 × 숫자 → 곱셈  
  - 문자열 × 숫자 → 문자열 반복  
    (예: `"a" * 3` → `"aaa"`)  
  - 다른 조합은 **에러 발생**

- 비교 연산 (`=`, `!=`, `<`, `>`)
  - 숫자 또는 문자열 모두 비교 가능  
  - `"5" = 5`는 **거짓**  
  - `"a" < "b"`는 사전식 비교

---


### ➖ 수식 구조 제한

SigbladFilum은 단순함 철학을 유지하기 위해 **한 번에 하나의 연산**만 허용한다.

- ✅ 가능한 예시:
  - `5 + 3`
  - `B2 - B5`
  - `"*" * 5`

- ❌ 허용되지 않음:
  - `3 + 5 + B2`
  - `B4 - B5 / 2`
  - `(A1 + A2) * 3`

따라서 **모든 수식은 반드시 단일 이항 연산자(`+, -, *, /, =, !=, <, >`)만을 포함해야 하며**, 중첩 계산이나 우선순위, 괄호 사용은 지원하지 않는다.

복잡한 계산이 필요한 경우, **중간 결과를 별도 셀에 순차적으로 저장**하여 여러 셀을 통해 단계를 나누어 처리해야 한다.

---

### 🛑 에러 처리 규칙

- 연산 중 다음 상황에 해당하면 **즉시 실행이 정지된다.**
  - 정의되지 않은 셀 참조
  - 잘못된 연산자 조합 (예: `"a" - 1`)
  - 문법 오류
- 프로그램은 멈추며 이후 셀은 실행되지 않는다.  
- 에러 메시지는 외부 UI에서 표시될 수 있으며, 시트에는 저장되지 않는다.


## 🧪 예제 모음

> 아래 표는 프로그램 **초기 시트**에 기록되는 명령만을 나타낸다. 실행이 끝난 뒤 어떤 셀이 결과를 담는지는 예제 설명으로 확인한다. 중간 과정에서 값이 변하는 셀은 표에 포함하지 않는다.

### 예제 1 – 값 복사

|     | A                                   | B | C |
|-----|-------------------------------------|---|---|
| 1   | `change(B1, "Hello") [A2]`         |   |   |
| 2   | `change(A1, B1) [A3]`               |   |   |
| 3   | `end`                               |   |   |

*실행 완료 후 `A1` 셀 값 ⇒ `Hello`*

---

### 예제 2 – 조건 분기

|     | A                                        | B | C |
|-----|------------------------------------------|---|---|
| 1   | `if(B3) [A2], [A3]`                      |   |   |
| 2   | `change(C1, "참이다") [A4]`              |   |   |
| 3   | `change(C1, "거짓이다") [A4]`            | `B1 = 4` |   |
| 4   | `end`                                    |   |   |

*사전에 `B1` 셀에 `원하는 숫자` 를 입력해 둔다. 실행 종료 후 결과는 `C1` 셀에서 확인한다.*

---

### 예제 3 – 5회 반복하여 별 5개 출력

|     | A                                              | B | C |
|-----|------------------------------------------------|---|---|
| 1   | `change(B2, "5") [A2]`                        |   |   |
| 2   | `change(B3, "B2 = 0") [A3]`                   |   |   |
| 3   | `change(B4, B1 + "*") [A4]`                   |   |   |
| 4   | `if(B3) [A6], [A5]`                            |   |   |
| 5   | `change(B1, B4) [A7]`                          |   |   |
| 6   | `end`                                          |   |   |
| 7   | `change(B2, B2 - 1) [A3]`                      |   |   |

*사전에 `B2` 셀(카운터)에 `5`, `B1` 셀(출력 대상)에 빈 문자열을 입력해 둔다. 실행 완료 후 `B1` 셀 값 ⇒ `*****`*



### 예제 4 – 입력 후 1초 대기·출력, `quit` 입력 시 종료

|     | A                                                    | B | C |
|-----|------------------------------------------------------|---|---|
| 1   | `input(B1) [A2]`                                     |   |   |
| 2   | `change(B3, "B1 = \"quit\"") [A3]`                |   |   |
| 3   | `if(B3) [A7], [A4]`                                  |   |   |
| 4   | `wait(1000) [A5]`                                    |   |   |
| 5   | `change(C1, B1) [A6]`                                |   |   |
| 6   | `goto [A1]`                                          |   |   |
| 7   | `end`                                                |   |   |

*사용자가 `quit` 이외의 문자열을 입력하면 1초 후 `C1` 셀에 그대로 복사되어 출력된다. `quit` 를 입력하면 프로그램이 종료된다.*

```
