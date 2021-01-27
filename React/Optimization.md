# **React 최적화**

이 문서에는 여러 최적화 하는 방법 및 최적화를 해야하는 이유 등에 대해 작성한 글 입니다.
<br/>

---

최적화는 특히 웹 앱을 개발하는 과정에서 가장 신경을 써야한다.<br><br>
최적화된 코드를 작성하는데 도움이 되는 구성 요소는 항상 재사용하도록 해야 한다. 만약 개발을 하면서 더 많은 시간을 훌룡한 코드를 개발하는데 쓰고 더 적은 시간을 평범한 코드를 개발하는데 (실수할 가능성이 훨씬 더 큰) 쓴다면 코드의 재사용성이 올라갈 뿐 아니라 효율적인 개발이 가능하게 된다.

최적화를 막상 하려고 하면 어려운 이유

- **재사용하기 유용한(필요한) 코드**를 잘 파악하지 못하거나 부분을 알지 못한다.
- 하는 방법이 **미숙하거나** 알고 있지만 **어느 상황에 어떻게 써야하는지** 알지 못한다.

`여기서 작성한 것은 최적화를 하는 데 무엇을 써야하고, 어떻게 써야하는지, 재사용 하는 코드는 어떻게 파악하는지에 대해 작성한다.`

---

## **1. useMemo()**

이 함수는 React Hooks 중 하나로 React 에서 CPU 소모가 심한 함수들을 캐싱하기 위해 사용한다.

여기서 CPU소모가 심하다는 것은 `setTimeout`, `setInterval`등의 작업 스케줄링 함수나, 재귀적인 함수나, `syntax-highlighting(코드를 컬러링 하는 작업)`스크립트 등을 뜻합니다.

```jsx
const Count = () => {
  const [count, setCount] = useState(0);
  const expFunc = () => {
    waitTime(3000);
    return count * 30;
  };
  const resCount = expFunc(count);
  return (
    <div>
      <span>count : {resCount}</span>
      <input type="text" onChange={(e) => setCount(e.target.value)} />
    </div>
  );
};
```

위 코드는 input값이 바뀔 때 3초 후에 `count`가 30 이 곱해져서 나오는 Count 컴포넌트다.<br>
만약 이 함수가 3초가 아니라 몇 분, 몇 십 분이 되기 시작하면 처음에 3을 입력하면, 몇 분을 기다리고, 다시 3을 다시 입력해도 같은 값임에도 불구하고, 몇 분을 다시 기다려야 한다. <br>
분명 같은 작업인데도 불구하고, 똑같은 시간을 들여 렌더링을 해야한다. <br> 분명 같은 작업인데도 말이다.

그런 경우에 사용하는 것이 `useMemo()`라는 함수이다.

```js
useMemo(() => func, [input_dependency]);
```

`func`는 캐시하고 싶은 함수이고, `input_dependency`는 useMemo가 캐시할 `func`에 대한 입력의 배열로써, 해당 값이 변경될 때 마다 `func`가 호출된다.

### 최적화 방법

```jsx
const Count = () => {
  const [count, setCount] = useState(0);
  const expFunc = () => {
    waitTime(3000);
    return count * 30;
  };
  const resCount = useMemo(() => {
    expFunc(count);
  }, [count]);
  return (
    <div>
      <span>count : {resCount}</span>
      <input type="text" onChange={(e) => setCount(e.target.value)} />
    </div>
  );
};
```

이렇게 작성하면 이제 `expFunc`는 `count` 입력에 대해 캐싱되며, 동일한 입력이 발생할 때는 `expFunc`를 호출하지 않고, 입력에 대해 캐싱된 결과 값을 리턴한다.<br>
useMemo를 통해 성능향상과 함수형 컴포넌트에서는 props 값들 또한 캐싱할 수 있다.

---

## **2. 가상화된 List**

웹사이트를 만들다 보면 여러 List들을 다루는 상황이 올텐데, 여러 방법으로 List들을 다룰 테고, 그 방법에는 `Array.map()` 함수나, 테이블을 사용하는 경우가 다반사이고, 많은 리스트를 모두 렌더링 해서 스크롤을 하는 형식으로 하는 경우도 많죠, 하지만 그렇게 되면 그 많은 리스트를 한번에 렌더링을 해야하고, 리렌더링을 할 때도 그 많은 리스트를 다시 렌더링을 해야하는 경우가 생기기 때문에 가상화 List를 사용합니다. <br>

많은 List를 다룰 땐 브라우저에서 보여지는 Viewport 부분의 리스트만 렌더링 하고, 스크롤 시 더 보여지는 부분을 따로 렌더링 하는 것을 `windowing`이라고 한다.
`windowing`하는데 사용하는 라이브러리엔 `react-virtualized`등이 있다.

---

## **3. 리터럴 함수**

우리가 컴포넌트를 작성할 때 별 로직이 없는 함수의 경우 **리터럴**로 함수를 생성하곤 한다 <br>

```jsx
return (
  <div>
    <input value={input} onChange={(e) => setInput(e.target.value)} />
  </div>
);
```

함수의 경우도 마찬가지로 불변데이터가 아니므로, 동일한 함수임을 증명하려면 상당히 지저분한 방법을 사용하므로 리터럴이 아닌 따로 함수로 지정해줘야 한다.

```jsx
const handleChange = (e) => {
  setInput(e.target.value);
};
return (
  <div>
    <input value={input} onChange={handleChange} />
  </div>
);
```

---

## **4. useCallback()**

`useMemo()`가 연산을 최적화 하며 컴포넌트를 최적화 했다면, `useCallback()`은 주로 렌더링 성능을 최적화 하는 상황에 사용한다. 이 `Hook`을 사용하면 이벤트 핸들러를 필요할 때만 생성할 수 있게 된다.
<br><br>
여러 함수를 선언하게 되면, 컴포넌트가 리렌더링 될 때마다 그 함수들이 새로 생성 됩니다.<br>
작은 프로젝트나 이런 상황에선 큰 문제가 되지 않지만, 컴포넌트의 렌더링이 자주 발생하거나, 컴포넌트의 깊이가 깊어지거나 리렌더링 해야할 컴포넌트가 많아진다면, 최적화 해주는 것이 좋다.

```jsx
import React, { useState, useMemo, useCallback } from "react";

const getAverage = (numbers) => {
  console.log("평균값 계산중..");
  if (numbers.length === 0) return 0;
  const sum = numbers.reduce((a, b) => a + b);
  return sum / numbers.length;
};

const Average = () => {
  const [list, setList] = useState([]);
  const [number, setNumber] = useState("");

  const onChange = useCallback((e) => {
    setNumber(e.target.value);
  }, []); // 컴포넌트가 처음 렌더링 될 때만 함수 생성
  const onInsert = useCallback(
    (e) => {
      const nextList = list.concat(parseInt(number));
      setList(nextList);
      setNumber("");
    },
    [number, list]
  ); // number 혹은 list 가 바뀌었을 때만 함수 생성

  const avg = useMemo(() => getAverage(list), [list]);

  return (
    <div>
      <input value={number} onChange={onChange} />
      <button onClick={onInsert}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값:</b> {avg}
      </div>
    </div>
  );
};

export default Average;
```

`useCallback()`함수의 첫 번째 파라미터에는 최적화할 함수(생성할 함수)를 작성하고, 2번째 파라미터에는 배열을 넣어주는데 그 배열에는 어떤 값이 바뀌었을 때 함수를 새로 생성해줄 것인지에 대한 값을 명시해주면 된다.
<br><br>
만약 `onChange` 처럼 비어있는 배열을 넣게 되면, 컴포넌트가 한번 렌더링 될 때 단 한번만 함수가 생성되며, `onInsert` 처럼 배열 안에 `number`, `list`를 넣어주게 되면 `input`의 `value` 값이 바뀌거나, list값이 생성, 제거, 변경이 될 때마다 새로운 함수가 생성된다고 볼 수 있다.
<br><br>
여기서,`onChange`같은 함수의 경우에는 `number`이라는 `input`값을 변경시키는데 왜 두번 째 인자 배열 값 안에 `number`가 안들어 가는 것에 대해 의문점을 가질 수 있다.
<br>
`onChange`함수는 number를 바로 설정을 해줄 뿐이지, 기존 값을 참조하지 않기 때문에 처음 렌더링 될 때 한번만 생성되어도 상관이 없는 것이다.
