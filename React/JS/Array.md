## 자바스크립트 Array 관련 공부 문서

---

Javascript를 사용하다 보면 Array 를 사용해야 하는 상황이 많이 발생한다. <br/>
그 상황에서 for문에.. 또 for문에... 이런 중첩 for문을 사용하는 것은 많은 중복을 부른다.<br>
이런 중첩을 줄이기 위해 Array Method 를 사용하는데, 메소드를 사용하면 편하게 사용이 가능하다.

### **pop - 배열의 뒷부분을 삭제**

```js
let arr = [1, 2, 3, 4, 5];
arr.pop();
console.log(arr); // [1,2,3,4]
```

---

### **push - 배열 뒷 부분에 값을 삽입**

```js
let arr = [1, 2, 3];
arr.push(4);
console.log(arr); // [1,2,3,4]
```

---

### **unshift - 배열 앞 부분에 값을 삽입**

```js
let arr = [2, 3, 4];
arr.unshift(1);
console.log(arr); // [1,2,3,4]
```

---

### **shift - 배열 앞 부분에 값을 삭제**

```js
let arr = [3, 1, 2, 3, 4];
arr.shift(3);
console.log(arr); // [1,2,3,4]
```

---

### **splice - 배열의 특정 위치에 요소를 추가하거나 삭제**

```js
let arr = [1, 2, 3, 4, 5, 6, 7];
arr.splice(3, 2); //3번째 인덱스부터 2개 제거
console.log(arr); //[1,2,3,6,7]

let arr2 = [1, 2, 3, 4, 5, 6, 7];
arr.splice(2, 1, "a", "b");
console.log(arr2); // [1,2,"a", "b", 4,5,6,7]
```

---

### **slice(startIndex, endIndex)**

**배열의 startIndex 부터 endIndex까지(endIndex는 불포함)에 대한 shallow copy를 새로운배열 객체로 변환**

```js
let arr = [1, 2, 3, 4, 5, 6, 7];
const copyArray = arr.splice(3, 6); // arr[3]부터 ~ arr[5] 까지 새로운 배열로 반환
console.log(copyArray); // [4,5,6]
```

---

### **concat - 다수의 배열을 합치고, 병합된 배열의 사본을 반환**

```js
let arr = [1, 2, 3];
let arr2 = [4, 5, 6];
let arr3 = arr.concat(arr2);
console.log(arr3); // [1,2,3,4,5,6]
```

---

### **every - 배열의 모든 요소가 테스트를 통과하는지의 여부를 반환**

```js
let arr = [1, 2, 3, 4, 5, 6, 7];
console.log(
  arr.every((item) => {
    return item % 2 === 0;
  })
); // false 모든 요소가 짝수이면 true를 return
```

---

### **forEach - 배열의 각 원소별로 지정된 함수를 실행한다.**

```js
let arr = [1, 2, 3];
arr.forEach((item) => {
  console.log(item); //1 2 3
});
```

---

### **map - 배열의 각 원소별로 지정된 함수를 실행한 결과로 새로운 배열을 반환한다.**

```js
let arr = [1, 2, 3];
const isEven = arr.map((item) => item * 2); // [2,4,6]
```

---

### **filter - 지정된 함수의 결과 값을 true로 만드는 원소들로만 구성된 별도의 배열을 반환한다.**

```js
let arr = [1, 2, 3, 4, 5, 6];
let evenArr = arr.filter((item) => item % 2);
console.log(evenArr); // [2,4,6]
```

---

### **reduce - 누산기 및 배열의 각 값에 대해 한 값으로 줄도록 함수를 적용**

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let sumArr = arr.reduce((preValue, curValue, index) => {
  return preValue + curValue;
});
console.log(sumArr); // 55
```

---

### **reverse - 배열의 원소 순서를 거꾸로 바꾼다**

```js
let arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr); // [5,4,3,2,1]
```

---

### **sort - 배열의 원소를 알파벳순으로, 또는 지정된 함수에 따른 순서로 정렬한다, 모든 원소를 문자열로 취급하여 사전순으로 정렬**

```js
let arr = ["banana", "orange", "apple"];
arr.sort();
console.log(arr); // ["apple", "banana", "orange"]

//sort안에 함수를 작성 하는 경우

let numArr = [2, 4, 5, 3, 1];
numArr.sort((a, b) => {
  return a - b;
});
console.log(numArr); // [1,2,3,4,5]
```

---

### **toString - 배열을 문자열로 바꾸어 반환한다.**

```js
let arr = [1, 2, 3, 4, 5, 6, 7];
console.log(arr.toString()); // 1, 2, 3, 4, 5, 6, 7
```

---

### **join - 배열 원소 전부를 하나의 문자열로 합친다.**

```js
let arr = [1, 2, 3, 4];
console.log(arr.join("-")); // 1-2-3-4
```

---
