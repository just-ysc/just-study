# How to Initialize Arrays in JAVA

## 1. For 반복문
```java
int[] array = new int[5];

for (int i = 0; i < array.length; i++) {
  array[i] = i + 1;
}
```

## 2. 선언과 동시에 초기화
```java
// 배열 길이를 별도로 지정하지 않아도 된다.
String array[] = new String[] { 
  "Toyota", "Mercedes", "BMW", "Volkswagen", "Skoda" };

int array[] = { 1, 2, 3, 4, 5 };
```

## 3. `Arrays.fill()`

- 배열의 일부 혹은 전부를 동일한 값으로 채울 수 있는 메서드를 `java.util.Arrays` 클래스에서 제공한다.

```java
// 배열 전체를 동일한 값으로 채움
int array[] = new int[5];
Arrays.fill(array, 30);

// 배열 일부를 동일한 값으로 채움(0: 시작 인덱스, 3: 채울 갯수)
int array[] = new int[5];
Arrays.fill(array, 0, 3, 30);
```

## 4. `Arrays.copyOf()`

- 다른 배열을 복사해서 새로운 배열을 생성하는 메서드이다.

```java
int array[] = { 1, 2, 3, 4, 5 };
int[] copy = Arrays.copyOf(array, 5);
```
- `Arrays.copyOf()`는 다양한 오버로딩을 지원하지만, 위 예시에서 두번째 argument는 새롭게 생성될 array의 길이를 의미한다.
  - 새롭게 생성되는 배열의 길이가 source 배열의 길이보다 클 경우, 초과하는 요소들은 기본값으로 초기화된다.

## 5. `Arrays.setAll()`

- 배열과 람다를 받아서 배열 요소를 갱신하는 메서드이다.

```java
int[] array = new int[5];
Arrays.setAll(array, idx -> idx > 9 ? 0 : idx);
```

## Reference

- https://www.baeldung.com/java-initialize-array