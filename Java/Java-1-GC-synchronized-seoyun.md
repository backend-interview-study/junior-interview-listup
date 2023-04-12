# 1. Garbage Collection(가비지 컬렉션)의 동작 방식에 대해서 설명해주세요.

## 면접 한 줄 정리
: Stop the world, Mark and Sweep 순서로 동작하며 가비지 컬렉션이 될 대상 객체를 식별(Mark)하고 제거(Sweep)하며 객체가 제거되어 파편화된 메모리 영역을 앞에서부터 채워나가는 작업(Compaction)을 반복 수행하게 됩니다.<br>

- Stop the world는<br>
JVM이 GC를 실행하기 위해 애플리케이션의 실행을 멈추는 작업으로 실행하는 스레드 외 다른 모든 스레드는 작업이 중단됩니다.

- Mark and Sweep<br>
Stop the world 이후 Root Space로부터 연결된 객체를 찾아 어떤 객체를 참조하고 있는지 찾아서 `마킹`하고, <br>
참조하고 있지 않은 객체를 Heap에서 제거하는 `Sweep` 과정을 거치면<br>
가비지 컬렉터 종류에 따라 compact 과정에서 Sweep 이후 분산된 객체들을 분리하여 압축해줍니다. 

--- 

자세한 내용은 [블로그 링크](https://velog.io/@may_yun/Java-Q2.-%EA%B0%80%EB%B9%84%EC%A7%80-%EC%BB%AC%EB%A0%89%EC%85%98-GC%EC%97%90-%EA%B4%80%ED%95%B4%EC%84%9C-%EC%84%A4%EB%AA%85%ED%95%B4-%EC%A3%BC%EC%84%B8%EC%9A%94)를 참고해 주세요.

---

# 2. 자바의 synchronized 키워드에 대해 설명해주시고 Reentrant Lock와의 차이는 무엇인지 말씀해주세요.
