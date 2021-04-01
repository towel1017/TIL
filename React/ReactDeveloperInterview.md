## 리액트 개발자 면접 질문

- CSR와 SSR의 차이점은?

- 평소에 가장 자신있는 언어와 그 이유는? 장단점에 대해서도 말해주세요.

- 효율적인 코드를 작성하실 때 신경쓰는 부분이 어떤 것들이 있나요?

- 서버와 데이터 통신을 해본 경험이 있나요?

- 리액트는 생명주기가 있고 그것을 맞춰주는 것이 어려운데, 이러한 부분은 어떻게 해셜하셨나요?
- Svelt를 사용해본 경험이 있나요?

- 라이브러리를 선택할 때, 특정 라이브러리를 선택하게 된 이유가 있나요?

- 캔버스 관련 작업을 해보신 적이 있나요?

- Closure를 currying과 함께 사용한 예시 코드를 작성해주세요.

- 원시값과 참조값(array, object)의 차이점을 메모리 관점에서 설명해주세요.

- 서버에서 1초 단위로 바뀌는 많은 양의 동적 데이터를 받아올 때, 실시간으로 바뀌는 데이터를 프론트단에서 어떻게 시각적으로 업데이트 할까요?

---

## Javascript

- Function 키워드로 사용하는 일반 함수와 화살표 함수의 차이점은 무엇인가요?

- 화살표 함수를 사용했을 때는 new 생성자를 사용해서 새로운 객체고 상속등을 할 수 없습니다. 그 이유에 대해서 설명해주세요.

- Event Bubbling에 대해서 설명해주세요.

- 아래의 코드는 어떠한 차이가 있나요?

```js
    const add = function() { ... }
    const add = () => { ... }
```

- strict mode 를 사용했을 때의 구체적인 특징은?

## React

- useCallback/useMemo에 대해서 설명해주세요.

- 리액트에서 setState는 비동기 동작인가요, 동기동작인가요?

- setState가 비동기 동작을 취했을 때 얻을 수 있는 이점은 무엇인가요?

- 리액트의 useCallback, useEffect등을 사용할 때 의존성 배열을 받게 됩니다. 이 배열의 역할은 무엇인가요?

- 의존성 배열은 shallow equal, deep equal중 무엇을 하게 되나요?

- props로 전달받은 함수는, props나 상태가 업데이트될 때마다 새로 생성이 됩니다. 이 때 최적화할 수 있는 방법은 어떤게 있나요?

- 아래 코드의 경우, useCallback을 사용을 하더라도 isClicked 의존성을 가지고 있습니다. 이 경우, 아예 의존성이 없게 만드는 방법이 있나요?

  ```js
  const handleToggle = useCallback(() => setIsClicked(!isClicked), [isClicked]);
  ```

- 다이나믹한 데이터를 받아올 때, useEffect에서 의존성배열을 어떻게 하실건가요?

- Next.js에서 getStaticProps, getServerSideProps의 차이점은?

- useLayoutEffect는 무엇인가요?

- 리액트를 사용할 때, 최적화에 신경쓰는 부분은 어떤 것이 있는지 구체적인 예시가 있나요?

- 아래와 같이 자식 컴포넌트를 React.memo로 감쌌을 때 props를 통해서 전달되어지는 함수에 useCallback을 사용한 경우와 사용하지 않은 경우에 차이가 있나요?

```js
  function Parent(){
  const handleClick = useCallback(() => { ... }, []); // (1)
  const handleClick = () =>{ ... } // (2)

      return <Child onClick={handleClick} />

  }


function Child({ onClick }) {
return <div onClick={onClick} />
}
export default React.memo(Child);
```

- React.memo의 특징에 대해서 설명해주세요.

- 얕은 비교(Shallow Equal)와 깊은 비교에 대해서 설명해주세요.

- React의 hook에 대해서 설명해주세요.

- 주로 어떤 경우에 custom hook을 사용했고, 그로 인해서 얻은 장점이 무엇인가요?

- Styled-components의 퍼포먼스에 대한 이슈에 대해서 경험해보신 적이 있나요?

- 리액트의 성능개선 방법에 대해서 설명해주세요.

- 상태 관리에 대해서 설명해주세요.

> **suyeonme 님의 면접 후기를 참고 했습니다.**
