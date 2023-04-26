# WEB_Redux
## 2023.04.26 ~ 2023.04.27
***
* 하나의 상태를 갖는다 = 상태를 바꿈에 따라서 애플리케이션 모습이 바뀐다고 생각!
* 하나의 상태를 유지하여 복잡성을 낮춘다
* UNDO/REDO를 굉장히 쉽게 할 수 있다
* 현재 상태 뿐만 아니라 이전 상태도 꼼꼼히 기록하여 문제 상황 파악 쉽게 가능하다
* Redux의 핵심은 "store" <- 모든 정보가 저장된다
* reducer 함수를 어떻게 작성하는 지가 매우 중요하다
* 직접 state 값에 접근 할 수는 없다
* render라는 함수는 언제나 state 값을 참조(getState)해서 UI를 만든다
* subscribe에 render를 등록해 놓으면 state 값이 바뀔 때마다 render 함수가 호출되면서 UI가 갱신된다
* dispatch는 reducer를 호출, reducer가 리턴하는 값은 새로운 state
* reducer를 통해 state 값을 변경한다
* 크롬 확장 기능 사용해서 Redux 탭 -> 애플리케이션 상태 변화 보관하기 때문에 과거~현재 상태 볼 수 있다
***
* reducer(state, action)로 약속
* store를 만들면, 그 내부적으로 state 값이 생기고, state 값을 가져올 때는 getState() 사용
* reducer를 통해 state 값을 만들어줘야 하는데, 그 때 reducer의 기존 state 값이 undefined라면 이는 초기화를 위해 최초로 실행되는 reducer에 대한 호출이기 때문에 원하는 초기값을 return해주면 redux의 store에는 그 초기값이 지정된다
***
* store.dispatch({type:    ... } => type이라는 객체는 반드시 있어야 함! 약속!
* dispatch가 reducer를 호출하고, 이 때 이전의 state 값과 전달된 action 값을 인자로 전달한다
* state를 직접적으로 변경하지 말고, Object.assign으로 복제한 후에 변경하기
* reducer는 store의 state 값을 변경하고, return하는 값은 원본을 바꾸는 것이 아니라 이전의 있던 값을 복제한 결과를 return
***
* redux라는 중개자를 통해 상태를 중앙집중적으로 관리를 할 수 있다 => 각 부품은 다른 부품에 대해 알고 있을 필요가 없어짐(내부에 다른 부품과 관련 코드 없어짐)
***
* redux-dectools 사용하면 페이지 검사에서 Redux 탭으로 state 추적 가능
* redux는 단 하나의 store를 유지되고, 그 store는 reducer를 통해 가공되기 때문에 애플리케이션의 어떤 상태가 궁금하면 reducer를 이용 (코드 하나하나에 console.log 찍을 필요 X)
=> reducer 함수 안에 콘솔 하나 찍어서 확인하면 과거, 현재 등등 원하는 상태나 action 확인 가능
 * #subject라고 입력하면 id가 "subject"인 div 태그 자동 생성됨
***
* 기존의 정적인 코드를 모듈화하여 사용하기
=> 각각의 id와 함수를 정의해서 사용하면 됨!
***
* redux 사용 순서
1. reducer(state, action) 함수 정의
2. 전역변수 store를 만들어 reducer 주입 => var store = Redux.createStore(reducer);
***
* state 사용하는 법
1. 초기값 설정하기
2. store에서 getState()로 현재 state 값 가져오기
3. 그 state 값 기반으로 원하는 코드 생성하기
=> 해당 state에 따라 만들어지는 웹페이지 생성 가능!
***
* state 값 변경하는 법
1. action을 발생시킨다
2. 그 action이 dispatch를 통해 reducer를 실행시킨다
3. 그러면 reducer가 state에 새로운 값을 준다
4. 그리고 state 값이 바뀌면 그 state가 subscribe하고 있는 함수들을 호출해 UI가 업데이트된다
※ action에서 필수적인 property는 "type" !!!
※ reducer에 if문 사용해서 action.type === ooo일 경우에 어떻게 동작해야 하는지 정의해서 return 하면 됨 !!!
※ if 문에서 원본 상태를 그대로 사용해서 코드 쓰면 안되고, 꼭! 복제본(newState) 만들어서 사용해야 함 !!!
***
* 배열 복제할 때는 Object.assign 말고 concat 사용
