## 리액트 개발자 면접 질문

- `CSR`와 `SSR`의 차이점은?

```
CSR (Client Side Rendering) :
- 처음 웹서버에 요청할 때 데이터가 없는 문서를 반환하고, HTML 및 Static 파일들이 로드 되면서, 데이터가 있다면 데이터 또한 서버에 요청하고, 데이터와 함께 화면상에 나타나게 된다. 그 후 사용자의 요청에 따라 javascript를 통해 동적으로 서버에서 요청을 받아와서 Rendering.

SSR (Server Side Rendering) :
 - 완전하게 만들어진 HTML 파일을 받아오고 Rendering 한다.
웹 서버에 요청할 때 마다 Browser 새로고침이 일어나고, 서버에 새로운 페이지에 대한 요청을 하는 방식.
```

- 평소에 가장 자신있는 언어와 그 이유는? `장단점`에 대해서도 말해주세요.

```
 - React, 자바스크립트 하이브리드 웹을 만들어 주는 library.
 - 데이터가 업데이트 될 때 마다 Data를 Virtual DOM 에 리렌더링을 합니다.

 장점
   - Components -> 모든 것을 컴포넌트 로 생각하며 사용하고, 커스터마이징한다.
   - JSX -> Javascript의 Syntax 확장으로, 빠르고, Type-safe로 편리하게 사용할 수 있다.
   - 단일방향 & Flux -> 데이터가 항상 단일방향으로 흐르기 때문에, 추적이 쉽고, 디버깅이 쉽다.
   - 라이브러리이므로, 프레임워크와 함께 혼용가능.
   - CSR, SSR 을 지원하여, SEO 호환 및 최적화 가능.
   - 컴포넌트 재사용성 극대화
 단점
   - VIEW ONLY, View 이외의 기능은 써드파티 라이브러리(패키지, 모듈)를 이용하거나 직접 구현해야함.
   - IE8 이하는 지원하지 않음. ( 사실 의미가 없음 )
```

- `효율적인 코드`를 작성하실 때 신경쓰는 부분이 어떤 것들이 있나요?

```
 1. 코드의 재사용성
   - 같은 코드, 같은 기능을 하는 함수들이 많아지는 경우 현저히 효율성은 떨어지기 때문에, 최대한 같은 기능, 같은 역할을 하는 코드는 작성하지 않으려고 한다.
 2. UI 재사용성
   - 같은 UI 및 컴포넌트가 겹치지 않게 하도록 합니다. 같은 템플릿이나 코드 및 UI 재사용성이 높은 리액트 에서는 그 장점을 극대화 시키도록 해야한다고 생각합니다.
```

- `서버와 데이터 통신`을 해본 경험이 있나요?

```
  - 네, REST API 와 HTTP API, GraphQL 로 서버와 데이터 통신을 한 경험이 있습니다.
  - REST API는 ~
  - HTTP API는 ~
  - GraphQL은 ~
```

- 리액트는 생명주기가 있고 그것을 맞춰주는 것이 어려운데, 이러한 부분은 어떻게 해셜하셨나요?

```
  - 리액트의 생명주기는 Class Component에서 존재하는데 클래스 컴포넌트는 componentDidMount 등의 여러 생명주기 메서드들을 사용할 수 있지만, Functional Component 에서는 라이프사이클이 존재하지 않으므로, 온전히 render만 구현합니다.

  - Class Component 는 생명주기의 큰 문제가 존재합니다. 바로 props를 재사용 하기 때문인데, 그로 인해 timeout 이나 lifecycle에 영향을 주는 함수들을(this.props를 읽는 콜백을 가진 함수들) 실행하는 동안 props가 바뀔경우 바뀌기 전에 로직이 실행되더라도, 바뀐 값이 영향을 주므로 그에 대한 예방을 해야함.

  - 예방법? 예방법은 props를 읽는 콜백을 가진 로직이 lifrcycle에 영향을 줄 경우 this.props를 참조를 먼저 하는 방법이 있다.
```

- 라이브러리를 선택할 때, 특정 라이브러리를 선택하게 된 이유가 있나요?

```
  - React를 선택을 했는데, 리액트를 사용하는 이유는 현재 개발을 편리하게 해주는 모듈이나 패키지들이 많이 존재하고, 컴포넌트 단위로 커스터마이징 할 수 있다는 점이 편리했고,
  HTML이 편리했던 저로써는 JSX를 사용하는 것이 적응이 쉬웠습니다.
```

- Closure를 currying과 함께 사용한 예시 코드를 작성해주세요.

```
  - closure란 독립적인 함수를 가리키며, 클로저 안에 정의된 함수는 그 환경을 기억한다.
  한 함수 내에서 함수를 정의하고 사용하면 클로저라고 한다.
```

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
