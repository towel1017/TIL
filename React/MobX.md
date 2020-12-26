# MobX

## MobX 개념 파악하기

MobX 상태 관리 라이브러리는 리덕스와 같이 리액트에 종속되어 있는 라이브러리가 아님.

MobX 는 크게 3가지로 나눌 수 있다.

### <strong>Observable </strong> (관찰 받고 있는 state)

- 리액트 안에서 사용되는 글로벌 상태를 직접 변경하며, 어떻게 상태가 변했는지 파악하는 요소.

### <strong>Computed Value</strong> (연산된 값)

- 이벤트 발생으로 인해 어떠한 연산에 필요로 하는 state에 변화가 생겼을 때, <br> 그 state 변화에 따라서 새로운 연산 작업을 수행하게 된다. 해당 state에 변화가 없으면, 그냥 기존의 값을 사용한다.

### <strong>Actions </strong>(액션, 행동)

- 상태에 어떻게 변화를 일으킬 것인지 정의하는 부분<br>
  Redux의 action과 같은 개념

<br><br><br>

## 리액트에서 MobX 사용하기

<strong>MobX 라이브러리 설치</strong>

```shell
$ yarn add mobx mobx-react
```

<strong>MobX 기본 사용 함수</strong>

```js
import React from "react";
import { decorate, observable, action, computed } from "mobx";
import { observer } from "mobx-react";
```

## Functional Component 에서 MobX 사용하기

mobx-react에서 제공하는 `observer`로 래핑된 함수형 컴포넌트에서는<br>
useState 같은 훅 API를 사용하려고 하면 React 에서 `"훅은 함수형 컴포넌트 에서만 사용할 수 있다"` 라는 메세지의 이슈를 발생시킨다. <br>
찾아보니 observer API는 클래스 컴포넌트를 리턴하는 hoc(higher order component)이기 때문이다. <br>

### mobx-react v6

Functional Component 에서 지원하는 mobx 대신 React에서 제공하는 `createContext API`를 통해 store를 가져오는 방법을 제안한다.

### 함수형 컴포넌트에서 `inject`를 대체할 `useStore`함수

- 마이그레이션을 위해서 코드를 수정할 필요는 X, 훅을 사용하는 함수형 컴포넌트를 위한 store를 가져오는 Helper함수를 작성 해야한다.

```js
import React from "react";
import { MobXProviderContext } from "mobx-react";

/**
 * React hooks를 사용하는 컴포넌트에서 store를 가져올 때 사용한다.
 * 참조) https://mobx-react.js.org/recipes-migration#hooks-for-the-rescue
 */
function useStores() {
  return React.useContext(MobXProviderContext);
}

export default useStores;
```
