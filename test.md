# 리액트 입문

#### 목차
1. 리액트는 어쩌다가 만들어졌을까.
2. 작업환경 준비
3. 첫번째 리액트 컴포넌트
4. JSX
5. props를 통해 컴포넌트에게 값 전달하기
6. 조건부 랜더링
7. useState를 통해 컴포넌트에게 바뀌는 값 관리하기
8. input 상태 관리하기
9. 여러개의 input 상태 관리하기
10. useRef로 특정 DOM 선택하기
11. 배열 랜더링하기
12. useRef로 컴포넌트 안의 변수만들기 
13. 배열에 항목 추가하기
14. 배열에 항목 제거하기
15. 배열에 항목 수정하기
16. useEffect를 사용하여 마운트/언마운트/업데이트시 할 작업 설정하기
17. useMemo 를 사용하여 연산한 값 재사용하기
18. useCallback 을 사용하여 함수 재사용하기
19. React.memo 를 사용한 컴포넌트 리렌더링 방지
20. useReducer 를 사용하여 상태 업데이트 로직 분리하기
21. 커스텀 Hooks 만들기
22. Context API 를 사용한 전역 값 관리
23. Immer 를 사용한 더 쉬운 불변성 관리
24. 클래스형 컴포넌트
25. LifeCycle Method
26. componentDidCatch 로 에러 잡아내기 / Sentry 연동
27. 리액트 개발 할 때 사용하면 편리한 도구들 - Prettier, ESLint, Snippet
---

## 01. 리액트는 어쩌다가 만들어졌을까.


---
## 02. 작업환경 준비
리액트를 사용하기위해서는 다음 항목들을 설치해야한다.

- Node.js
- yarn (혹은 npm으로 대체해도 된다.)
- editor (자신의 취향에 맞는 것으로 사용)
- git bash
  - 윈도우의 경우, linux 형태의 명령창이 필요할 때가 있다. 이럴경우 git bash를 사용하는 것이 보다 편리하다.

모든 항목이 전부 설치되면 새로운 리액트 프로젝트를 만들어 보자
git bash에서 아래의 명령어를 실행해 보자
``` bash
$ npx create-react-app begin-react
```
해당 명령어가 완료되고 나면, `begin-react` 폴더에 새로운 리액트 프로젝트가 생성되었다. 아래의 명령어를 통해서 리액트를 실행할 수 있다.

먼저 begin-react 폴더로 이동하자
``` bash
$ cd begin-react 
```
그리고, 리액트 프로젝트를 실행하자
``` bash
$ yarn start
// 혹은 npm start를 실행하면 된다.
```

---
## 03. 첫번째 리액트 컴포넌트
리액트에서 컴포넌트를 만드는 방법에 대해 알아보자.
먼저 `Hello.js` 파일을 생성한다.

리액트를 사용하기 위해서는 아래의 세 요소가 필요하다.

먼저 리액트를 불러와야한다.
```javascript
import React from 'react';
```
이후, 컴포넌트를 함수 혹은 클래스 형태로 작성한다. 아직 우리는 초보자이기 때문에 당분간은 함수로 컴포넌트를 만들 것이다.
```javascript
import React from 'react';

function Hello(){
  return;
}

```

컴포넌트를 생성하고 나면, 다른 컴포넌트에서 사용할 수 있도록 `export` 속성을 지정해주면 된다.  
이렇게 완성된 코드는 아래와 같다.
```javascript
import React from 'react';

function Hello(){
  return;
}

export default Hello;
```

---
## 04 JSX
html 문법을 `react.createElement`로 변환해주는 문법  
바벨을 이용해서 컴파일됨  
컴파일 되기위한 규칙들이 있음

1. 태그는 꼭 닫혀야 됨
   - `self closing`도 필수
2. 2개이상의 태그는 하나의 태그로 감싸져야됨
   - 굳이 불필요하게 감싸야되는 경우에는 리액트 fragemenet 사용(빈 `<></>`태그. 컴파일시 해당 빈태그는 생략됨) 
3. JSX 내부에서 JS값을 사용하기 위해서는 `{}`로 감싸주면 됨
4. 객체로 style 지정해주어야 되며, 속성명은 카멜케이스로 작성해주어야 됨 
``` javascript
const style = {
  backgroundColor = 'aqua',
  borderStyle = 'solid',
  padding = 16 // 기본단위는 px
}
```
5. class를 지정해주고 싶다면 ~className~으로 지정해야됨 
``` html
<div className="gray-box"></div>
```
6. 주석은 `{/**/}`
7. 태그 내부에서 주석을 사용하고 싶다면 `//`를 이용

---
## 05 props
컴포넌트에게 값을 넘겨주는 속성

1. props 사용
``` javascript
// props 값을 사용
function Hello(props){
  return <div> 안녕하세요 {props.name} </div>;
}
// 컴포넌트 호출(props값 설정)
<Hello name="react" />
```
2. 여러개의 props, 비구조할당 방식
``` javascript
function Hello({name, color}){
  return <div style={
    color: color // 혹은 color 만 사용해도 됨
  }> 안녕하세요 {name}</div>
}
```
3. props.children
``` javascript
// 컴포넌트 태그 사이의 값을 렌더링하기 위해 사용
function Wrapper({ children }){
  return (
    <div> { children } </div>
  )
}
// 컴포넌트 호출
<Wrapper>
  <Hello name="react" />
</Wrapper>
```

---
## 06 조건부 랜더링
특정 조건에 따라, 다른 결과를 렌더링하는 것을 의미  
true/false 일때, 값이 달라지는 경우 삼항연산자를 사용  
```javascript
// 컴포넌트 선언
function Hello({name, isSpecial}){
  return (
    <div> 
      {isSpecial ? <b>*</b> : null}
      안녕하세요 {name} 
    </div>
  );
}
// 컴포넌트 호출(props값 설정)
<Hello name="react" isSpecial="true" />
```
true일 때, 값이 보여지는 경우에는 && 연산자를 이용

``` javascript
// 컴포넌트 선언
function Hello({name, isSpecial}){
  return (
    <div> 
      {isSpecial && <b>*</b>}
      안녕하세요 {name} 
    </div>
  );
}
```
props 설정 시, 값 설정을 하지않으면 true로 지정됨
``` javascript
// 컴포넌트 호출(props값 설정)
<Hello name="react" isSpecial />
```

---
## 07. useState를 통해 컴포넌트에게 바뀌는 값 관리하기
사용자 인터렉션에 따라 변하는 값을 구현하기 위해,  
React의 Hooks 중 하나인 useState에 대해 알아보자.

먼저 useState를 사용하기 위헤서는 import를 해야한다.
``` javascript
import React, { useState } from 'react'
```
useState를 사용할때는 상태의 기본값을 파라미터로 넣어서 호출해야한다.  
호출하게 되면, 배열이 반환되는데 첫번째 값은 현재상태(파라미터), 두번째 값은 `Setter` 함수가 반환된다.
``` javascript
const numberState = useState(0);
const number = numberState[0];
const setNumber = numberState[1];

// 이를 배열 비구조와 할당을 통해서 아래와 같이 사용할 수 있다.
const [number, setNumber] = useState(0);
```
위의 내용을 이용해서 카운터 컴포넌트를 생성해보았다.
``` javascript
// 컴포넌트 선언
function Counter(){
  const [number, setNumber] = useState(0);
  const onIncrease = () => {
    setNumber(number + 1)
  }
  const onDecrease = () => {
    setNumber(number - 1)
  }
  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  )
}
// 컴포넌트 호출
<Counter />
```
### 주의할 점
JSX에서 함수 호출이 아래 사항을 주의해야된다.
1. `onclick` 속성 사용시, 카멜케이스 방식 유지
     - `onClick` 으로 사용해야된다.
2. 함수 호출시 `()`는 생략한다.
     - `onClick="onIncrease()"` 로 지정하게 되면, 랜더링과 동시에 함수가 실행된다. 인터렉션에 따라 함수가 호출되기 원하면 `()`는 생략

---
## 08. input 상태 관리하기

위에서 사용한 useState를 이용해서 input의 값을 초기화 해주는 컴포넌트를 구현해 보자

``` javascript
function InputSample(){
  const [text, setText] = useState('');
  const onChange = (e) =>{
    setText(e.target.value)
  }
  const onReset = () => {
    setText('');
  }
  return(
    <div>
      <input onChange={onChange} value={text} />
      <button onClick={onReset}>reset</button>
      <div>* value : </div> {text}
    </div>
  )
} 
```
위 코드를 자세히 해석하면 아래와 같다  
``` javascript
  const onChange = (e) =>{
    // e는 이벤트 e.target은 이벤트 객체를 의미
    setText(e.target.value)
  }
```
파라미터  `e`는 이벤트, `e.target`은 이벤트가 이루어 지는 객체 즉, input을 의미한다. input에 적혀지는 값을 가져오기 위해서는 `input의 value`를 가져오면 된다.

input의 경우, useState를 사용할 때 반드시 value를 지정해주어야 한다. 그렇지 않으면 사용자의 인터렉션에 따라 데이터를 관리할 수 없기 때문이다.

---
## 09. 여러개의 input 상태 관리하기
여러개의 인풋을 관리하기 위해서는 input에 name을 부여해서 참조해서 사용하게끔 해야한다.
``` javascript
function InputSample(){
  return(
    <div>
      <input name="name" />
      <input name="nickname" />
      <button>reset</button>
      <div>* value : </div>
    </div>
  )
} 
```
이렇게 여러개의 input의 데이터를 관리할 때는 useState를 객체상태로 하여 관리한다. 
``` javascript
function InputSample(){
  const [inputs, setInput] = useState({
    title = '',
    nickname = ''
  })
  const { title , nickname} = inputs // 비구조화 할당
  // ''' 생략
} 
```
객체상태를 업데이트 할 때는 불변성을 지키기 위해서 spread 문법을 이용해서 특정 값을 덮어씌워서 해야한다.

아래의 내용은 `[name]`의 키값을 가진 값을 `value` 로 설정한다.
이 경우, `[name]`에는 title 혹은 nickname이 들어가며, value는 input의 적힌 값이 설정된다.
``` javascript
function InputSample(){
  const [inputs, setInput] = useState({
    title = '',
    nickname = ''
  })
  const { title , nickname} = inputs
  const onChange = (e) => {
    const {value, name} = e.target; // e.target에서 value와 name을 추출

    setInput({
      ...inputs, // spread
      [name] : value // 값 업데이트
    })
  }
  // ''' 생략
} 
```
spread 문법을 이용해 불변성을 지키는 이유는 리액트가 데이터가 
기준값이 있어야 상태가 업데이트 됨을 확인할 수 있고 이에따라 필요한 랜더링을 진행하기 때문이다.

예시로 위의 코드를 아래와 같이하면, 상태값이 다름을 파악할 수 없어 작동되지 않는다.
``` javascript
function InputSample(){
  const [inputs, setInput] = useState({
    title = '',
    nickname = ''
  })
  const { title , nickname} = inputs
  const onChange = (e) => {
    const {value, name} = e.target; // e.target에서 value와 name을 추출

    setInput({
      inputs[name] = value;
    })

    // setInput({
    //   ...inputs, // spread
    //   [name] : value // 값 업데이트
    // })
  }
  // ''' 생략
} 
```

---
## 10. useRef로 특정 DOM 선택하기

---
## 11. 배열 랜더링하기

---
## 12. useRef로 컴포넌트 안의 변수만들기 

---
## 13. 배열에 항목 추가하기

---
## 14. 배열에 항목 제거하기

---
## 15. 배열에 항목 수정하기

---