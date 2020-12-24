# JS 와 JSX

## 1. React 의 컴파일 방식

React는 작성한 코드를 꼭 컴파일 하는 과정을 거쳐야만 한다. <br>
Babel을 통해 컴파일을 진행하면 이 코드는

```js
class HelloMessage extends React.Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}
ReactDOM.render(<HelloMessage name="John" />, mountNode);
```

Babel(render 함수)를 통해 컴파일이 되면

```js
class HelloMessage extends React.Component {
  render() {
    return React.createElement("div", null, "Hello ", this.props.name);
  }
}

ReactDOM.render(React.createElement(HelloMessage, { name: "John" }), mountNode);
```

이러한 코드로 변환이 되게 됩니다.

## 2. Js vs JSX

사실 파일 자체의 코드에는 별 차이가 존재하지 않습니다.
JS 에서도 JSX 문법이 사용이 가능하기 때문입니다.

그럼에도 불구하고 JSX문법이나 JSX를 사용하는 이유는

> 1. JSX는 컴파일링 되면서 최적화가 되므로, <strong>빠르다.</strong>
> 2. Type-Safe (즉, 어떠한 연산도 정의되지 않은(undefined) 라는 결과를 내놓지 않습니다. ) 이를통해 컴파일 과정에서 에러를 잡을 수 있습니다.
> 3. HTML에 익숙한 우리들은 JSX를 사용하여 쉽고 빠르게 템플릿을 작성할 수 있습니다.

## 3. React

리액트에서의 JSX 사용은 당연하듯이 사용되고 있습니다. <br>
그 누가 babel로 컴파일된 코드를 React에서 직접 짜려고 할까요?

가상 DOM과 JSX를 통한 React는 당연시 되어가고 있고, <br>
JSX를 템플릿 언어라고만 생각할 수 있지만, Js의 문법은 모두 들어가 있기 때문에 JSX를 사용하는 것이겠죠.
