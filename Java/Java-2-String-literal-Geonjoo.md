# 문자열을 리터럴(`string = "abcd"`)로 할당하는 것과 객체(`string = new String("abcd")`)로 할당하는 방식의 차이가 무엇인가요?

## 한 줄 정리

String을 리터럴로 할당하는 경우 생성된 객체는 Heap 영역의 String Constant Pool에 들어간다. 나중에 String으로 할당한 객체의 값이 String Constant Pool에 존재하는 경우, String Constant Pool의 값을 참조한다.

String을 객체로 참조하는 경우 String Constant Pool이 아닌 Heap 영역에 새로운 객체를 만들어 별도의 객체를 참조한다.

## String을 리터럴로 할당하는 경우

```java
String animal1 = "Cat";
String animal2 = "Cat";
String animal3 = "Dog";
```

![image](https://user-images.githubusercontent.com/69177351/232790988-17a011e8-5bfe-4baa-8ac1-0a4410160eed.png)

- 위와 같이 String을 리터럴로 할당하는 경우 `animal1` , `animal2` , `animal3` 는 Stack 영역에, `"Cat"` 과 `"Dog"` 는 Heap 영역에 저장된다.
    
    → 자바는 **String Constant Pool** 을 사용해 String의 불변성을 지킨다
    
    → **String Constant Pool** 을 사용하는 것을 String Interning 이라고 한다.
    
- String Constant Pool은 내부적으로 HashTable 구조를 갖고있다.
    
    
- String이 리터럴로 할당될 때, **String Constant Pool**에 String이 있는지 확인한다
    
    → **String Constant Pool**에 있는 경우 새로운 메모리에 할당하지 않고 재사용한다.
    

```java
System.out.println(animal1.equals(animal2)); // true
System.out.println(animal1==animal2); // true
```

- 따라서 위처럼 `animal1` 과 `animal2` 의 주소와 값을 비교하면 `true` 가 나오게 된다

## String 을 객체로 할당하는 경우

```java
String animal4 = new String("Cat");
```

![image](https://user-images.githubusercontent.com/69177351/232791138-b90f7672-fb95-4f6e-9e53-10b393968c42.png)

- String 을 객체로 할당하게 되면 **String Constant Pool**과 상관 없이,Heap 영역에 새로운 객체를 생성해 참조하게 된다

```java
System.out.println(animal1.equals(animal4)); // true
System.out.println(animal1==animal4); // false
```

- `animal1` 과 `animal4` 의 값을 비교하면 `true` 이다
- `animal1` 과 `animal4` 의 주소를 비교하면 서로 다른 객체를 참조하므로 `false` 이다
