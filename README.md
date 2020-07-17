# Hello React

- 프론트엔드 프레임워크를 통해 개발자는 DOM을 조작하지 않고, 데이터 처리에만 집중할 수 있다.
- React를 통해 DOM에 접근하지 않고 데이터를 변경
- React에서 데이터에 접근할 때는 state, setState를 사용해야 한다. 오직 코딩을 통해서만 데이터에 접근할 수 있음
- 각 컴포넌트는 자신만의 상태를 가지므로 중복해서 생성하더라도 서로 다른 상태를 가진다.


## React Fragment
Fragment의 사용을 통해 div의 무분별한 사용을 줄일 수 있다.

```js
<>
</>

// 웹팩이나 babel2를 import 하지 않았다면 아래처럼 사용한다.
<React.Fragment>
</React.Fragment>
```
 
리액트 컴포넌트 안에서 return 값에 사용되는 소괄호`()`는 그룹 연산자이다.  
리액트에서는 코드의 가독성을 높이기 위해 주로 사용한다.  
그룹 연산자는 수식에서 우선 순위를 높일 때 `5 * (2 + 3)`만 의미가 있다.  


## React에서 HTML Attribute 사용
React에서 HTML Attribute 사용할 때 (onload, onclick, onsubmit,onfocus, onchange) on 뒤의 첫 번째 문자는 대문자로 사용.  
- form에서 발생하는 이벤트일 경우 `onSubmit` 
- 일반적인 버튼에서 발생하는 경우 `onClick`

## Arrow Function
직접 만든 함수들은 `Arrow Function`을 사용해야 한다.
그렇지 않으면 `this`가 달라진다.

## 실무에서 class 사용
실무에서 class 사용할 때는  
`constructor(props)`와 `super(props)` 없이 사용할 수도 있다.


```js
class Gugudan extends React.Component {
  state = {
    firstNum: Math.ceil(Math.random() * 9),
    secondNum: Math.ceil(Math.random() * 9),
    value: '',
    result: '',
  } 
}
```

### prevState
setState를 통해 상태를 변경할 때 **이전 상태**와 **바꿀 상태**를 구분하기 위해 **React에서 제공하는 API**  
setState 안으로 함수를 전달하며, parameter를 통해 상태를 구분할 수 있다.  
**이전 state의 값으로 새로운 값을 만들 때는 함수를 전달하여 prevState를 사용하는 API를 사용해야 한다. 즉, `this.setState`를 통해 값을 변경할 때 `this.state`가 들어가야 할 경우 함수를 전달하여 `prevState`를 사용해야 한다.**

```js
this.setState((prevState) => {
  return {
    firstNum: Math.ceil(Math.random() * 9),
    secondNum: Math.ceil(Math.random() * 9),
    value: '',
    // result: `${this.state.value} 정답`,
    result: '정답: ' + prevState.value,
  }
})
```


## ref
DOM을 조작하고 싶을 때는 React에서 제공해주는 도구를 사용해야 한다. 그것이 React의 철학과 맞다.

```js
// document.querySelector('input'); 
<input ref={c => this.input = c } type="number" value={this.state.value} onChange={this.onChange} />
```

## state를 바꾸었을 때 일어나는 현상

`setState()`를 사용하면 다시 render된다는 것을 이해해야 한다.  
10초가 걸리는 복잡한 작업이 있는데, `setState()`로 인해 계속해서 render된다면
서비스를 이용하기 어려운 환경이 된다. 그래서 성능 최적화를 위해 setState의 특징을 기억해야 한다.

함수를 메서드로 빼는 이유는 화면을 다시 그릴 때 함수 또한 마찬가지로 계속 다시 그려질 수 있다.  
함수가 계속 다시 생성되는 일을 방지하기 위해 메서드로 빼는 게 좋다.


---