# 1. Base64 인코딩이란? 

## 면접 한 줄 정리
: Base64는 Binary Data(8비트 이진데이터)를 Text로 변경하는 인코딩 방식중 하나로<br>
바이너리 데이터를 문자 코드에 영향을 받지 않는 공통 ASCII 영역의 문자들로 이루어진 문자열로 변경합니다.

- `Base64를 사용하는 이유` <br>
문자를 위한 Media에 Binary Data를 전송할 때 ASCII로 인코딩하여 전송하면 시스템간 데이터를 전달하기에 안전하지 않다
  - ASCII는 7bits Encoding 인데 나머지 1bit를 처리하는 방식이 시스템 별로 상이하다
  - 일부 제어문자 (ex: Line ending)의 경우 시스템 별로 다른 코드값을 갖음

따라서 <br>
ASCII중 제어문자와 일부 특수문자를 제외한 64개의 안전한 출력 문자(문자 코드에 영향을 받지 않는 공통 ASCII를 의미)만 사용하는 Base64를 사용하는 것

---

자세한 내용은 [블로그 링크](https://velog.io/@may_yun/JAVA-Base64%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)를 참고해 주세요.
