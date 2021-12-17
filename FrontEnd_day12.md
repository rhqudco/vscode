## 자바스크립트 라이브러리와 프레임워크 필요성
- 웹 애플리케이션에서 유저 인터페이스 동적 처리 시 각 DOM 요소 작업 필요
- getElementById()로 찾아와서 이벤트 처리하고 코드 작성
- 프로젝트 커지고 인터페이스도 다양해짐.
- 프로젝트 관리를 하기 위해 많은 DOM 요소나 코드를 관리하고 정리하는 일이 어려워짐
- 사용자 인터페이스에만 집중할 수 있는 라이브러리 또는 프레임워크 필요
- 많은 라이브러리나 프레임워크가 만들어지고 사용되며 생산성, 유지보수성 향상
- 대표적인 자바스크립트 라이브러리 / 프레임워크
  - Angular
  - React
  - Vue.js
- 프레임워크 / 라이브러리
  - 프레임워크
    - 뼈대(기반 구조를 의미)
    - 제어의 역전
    - 여러 클래스, 컴포넌트로 등으로 구성
    - 작업하는 방법이 정의되어 있다.
  - 라이브러리
    - 활용 가능한 도구의 집합
    - 사용자가 정의한 클래스를 호출해서 사용
  - 차이
    - 제어권이 누구에게 있는가?
    - 라이브러리 : 사용자(개발자)가 주도적으로 호출해서 사용
    - 프레임워크 : 제어권이 프레임워크에 있어, 정해진 틀 안에서 코드를 작성해야 함.
  - Angular
    - SPA(Single Page Application) 개발을 위한 구글의 클라이언트 즉, 자바스크립트 프레임워크
      - SPA : 웹 서비스를 요청할 때 마다 서버로부터 페이지 전체를 호출하는 방식이 아니라 최초 한 번만 페이지 전체를 로딩하고 이후부터는 변경된 데이터만 호출하는 방식
    - 많은 기능 내장
    - 타입스크립트 사용 기본
      - 자바스크립트 기반(자바스크립트의 상위 집합인 타입스크립트를 기반으로 함)
    - MVC 프레임워크를 이용해서 잘 설계되고 구조화된 웹 애플리케이션을 쉽게 구현할 수 있다.
    - Angular 버전
      - AngularJS : Angular 1.x 버전
        - JavaScript dnlwn
      - Angular : Angular 2.x 이상 버전(현재 버전 : 12)
        - JS가 빠짐 : JavaScript에 국한되지 않는 새로운 프레임워크 제공
  - React
    - UI를 집중적으로 잘 만들기 위해 (구)페이스북(현 메타)에서 만든 자바스크립트 라이브러리
    - 컴포넌트에 집중되어 있는 라이브러리
      - 컴포넌트
        - 동작 가능한 하나의 부품 개념으로 애플리케이션의 화면을 구성하는 뷰(View)를 생성하고 관리 
        - 여러 컴포넌트를 조립하여 하나의 완성된 애플리케이션 생성
        - 잘게 나누어진 컴포넌트 모듈들을 조합해서 애플리케이션을 개발하는 오늘날의 개발 접근 방법(Web Modularity / 컴포넌트 기반 개발)을 React가 보편화 시킴
    - Angular와 달리 뷰(UI)만 신경쓰고 나머지는 Third Party 라이브러리를 필요
    - 공식 라이브러리 개념이 없고, 여러 솔루션을 사용
    - 생태계가 넓고 활성화되어 있음
    - 특징
      - 제일 먼저 가상 돔을 성공적으로 사용
      - 이후 다른 많은 라이브러리에서 가상 돔 개념 채택
      - Virtual DOM
        - 브라우저 DOM 기반으로 데이터가 변경될 때 마다 페이지에서 새로운 뷰를 만들어 전체 DOM을 새로 넣기 때문에 성능상 문제
          - 변화가 있을 때 마다 실제 DOM에 변경된 내용을 넣는 것이 아니라 자바스크립트로 만들어진 가상의 DOM에 렌더링 후 기존의 돔과 비교해서 변경된 것만 업데이트하는 방법으로 해결
      - 생태계 조성(가치사슬, 협력관계)
        - 다양한 생태계를 가지고 있어 좋고 많은 라이브러리들이 많이 만들어지고 있음
  - Vue
    - 앵귤러와 리액트의 장점 포함
    - CDN 방식으로 불러 와서 사용
    - 공식 라우터와 상태관리 라이브러리 존재
    - 앵귤러처럼 디렉티브 기능 있고 리액트처럼 가상 돔(Virtual DOM) 기반 컴포넌트 있음
      - 디렉티브 : DOM을 통해 HTML의 태그에게 기능을 부여하거나 표현하는데 사용
  
## React 환경설정
- 설치 프로그램
  - Node.js
    - Chrome V8 JavaScript 엔진(V8 Engine)으로 빌드된 JavaScript 런타임
    - 자바스크립트를 웹 브라우저 영역 외에 서버, 모바일 애플리케이션, 데스크탑 애플리케이션 등의 영역에서 사용 가능하게 해 줌
    - React 애플리케이션은 웹 브라우저에서 실행되는 코드이므로 Node.js와 직접적인 연관은 없지만 프로젝트를 개발하는 데 필요한 도구들이 Node.js를 사용하기 때문에 설치 필요
    - Visual Studio Code
    - NPM (Node Package Manager)
      - 자바스크립트 패키지 매니저 도구
      - Node.js에서 사용할 수 있는 모듈들을 패키지화하여 모아둔 저장소 역할과 패키지 설치 및 관리
      - React 역시 하나의 패키지
  - Create-React-App
    - 리액트 프로젝트 생성 도구
    - CRA 사용하면 간편하게 리액트 개발 환경 구축
    - 자동으로 다수의 패키지들이 설치되고 WebPack 및 Babel 설정도 자동으로 설정(나중에 번들 옵션 사용 가능)
    - 초기 단계에서 WebPack과 Babel 직접 설정할 일 없음
      - WebPack
        - 모듈 번들러 (Module Bundler)
        - 모듈화된 코드를 하나의 파일로 합치고(번들링) 코드 수행할 때마다 웹 브라우저로 리로딩
        - 코딩할 때 편의를 위해 여러 개의 모듈로 나누어 작업
        - 그렇지만 브라우저에서 파일 단위 모듈 시스템을 이용하게 되면 많은 네트워크 비용 낭비됨
        - 웹 애플리케이션의 규모가 커지면서 많은 양의 파일들이 하나로 모여 구성되는데 여러 개의 모듈을 하나의 파일로 묶어서 보낼 모듈 번들러 필요
        - 리액트에서 웹팩(Webpack)이라는 모듈 번들러 사용
          - 파일들의 관계가 복잡하고 무겁기 때문에 브라우저에서 이해하고 처리하기 힘들어 지는 문제 해결
          - 파일들 간의 의존성 관계 정리 및 최적화, JSX 파일을 합쳐서 하나의 자바스크립트 파일로 만들어줌
      - Babel
        - 자바스크립트 변환 도구
        - Babel is a JavaScript Compiler
        - 자바스크립트 ES6 문법을 이전의 ES5로 변환
        - 최신 버전의 브라우저에서는 ES6 문법을 바로 실행 가능하지만, 구버전의 브라우저에서는 실행되지 않는 문제가 발생해서 변환이 필요
        - 리액트 컴포넌트에서 사용하는 JSX 문법도 정식 자바스크립트 문법이 아니기 때문에 변환 필요
        - Babel을 통해 React를 일반 브라우저에서 실행 가능하도록 변환 작업 수행

### 설치
- mac 기준
  - node.js 설치
  - npm 설치
  - terminal -> 원하는 디렉토리로 이동 -> create-react-app __원하는 프로젝트 이름__
  - 실행은 terminal에서 프로젝트가 있는 디렉토리로 이동 후 npm start
  - 종료는 Control + c

############################################################################################################

## React 프로젝트

~~~js
// App.js
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>안녕하세요</h1>
    </div>
  );
}

export default App;
~~~

~~~html
<div></div>
<div></div>
<!-- 있으면 안 되고 -->
<div>
    <div></div>
    <div></div>
</div>
~~~

- index.js : 앱의 진입점 역할
-  root에 렌더링 (화면에 출력) : index.html의 \<div id="root">\</div> 영역에 렌더링
- ReactDOM.render : 컴포넌트를 페이지에 렌더링 하는 역할
- 첫 번째 파라미터 : \<App />
  - 페이지에 렌더링 할 내용(JSX 형태)
- 두 번째 파라미터 : document.get.....
  - 렌더링할 document 내부 요소 설정(위치)
- 제한 기능 : 리액트 프로젝트에서 나중에 사라지게될 legacy 기능을 사용하지 못하게 제한하는 기능
  - \<React.StrictMode>
- export default App;
  - 컴포넌트를 외부에서 사용할 수 있도록 내보내는 역할
- 컴포넌트 (클래스) 이름은 대문자로 시작
- 중괄호 안에 작성
- 반드시 render() 함수포함
- render() 함수 내에는 반드시 하나의 최상위 태그로 시작해야 함
- 컴포넌트 유형
  - 클래스 기반 컴포넌트 : 클래스 기반
  - 함수 기반 컴포넌트 : 함수 기반
    - props : 부모 컴포넌트에서 자식 컴포넌트로 데이터 전달할 때 사용
    - 단순히 props만 받아와서 보여주는 경우 초기 마운트 속도가 미세하게 빠르고, 불필요한 기능도 없어서 메모리 자원 덜 사용
    - 단순히 값만 받아와서 보여줄 때 유용
    - 컴포넌트 수가 엄청 많을 때 효과적(수행속도 최적화 될 수 있음)
    - 컴포넌트 수가 많지 않을 경우 클래스로 만들어도 성능상 큰 차이 없음
    - 즉, 컴포넌트를 간단하고 빠르게 생성할 때 주로 사용

~~~js
import React, { Component } from 'react';

class JSX extends Component {
    render() {
        // 자바스크립트 코드 영역
        return (
            <div>
                {/* JSX 문법 영역 */}
            </div>
        );
    }
}
export default JSX;
~~~



### 함수 기반으로 되어 있는 컴포넌트를 클래스 기반 컴포넌트로 변경(한 파일에 모두) - /src/App.js

- import React, { Component } from "react"; 필수
  - from "react" 라는 라이브러리에서 { Component } 라는 클래스를 로딩한다는 의미
- export default App; 외부에서 이 클래스 사용 가능하도록 내보내기(export)

~~~js
import React, { Component } from "react";
import './App.css';
// 컴포넌트 생성
// 컴포넌트 : 사용자 정의 태그
class Subject extends Component {
  render() {
    return (
      <header>
        <h1>Web</h1>
        world wide Web!
      </header>
    )
  }
}
class NAV extends Component {
  render() {
    return (
      <nav>
        <ul>
          <li><a href="1.html">HTML</a></li>
          <li><a href="2.html">CSS</a></li>
          <li><a href="3.html">JavaScript</a></li>
        </ul>
      </nav>
    )
  }
}
class Content extends Component {
  render() {
    return (
      <article>
        <h2>HTML</h2>
        하이퍼 텍스트 기반 마크업 언어
      </article>
    )
  }
}
class App extends Component {
  render() {
    return (
      <div>
        <h3>안녕하세요.</h3>
        {/* 위에 추가한 컴포넌트 사용 : 태그 형식으로 사용한다. */}
        <Subject></Subject>
        <Subject></Subject>
        <NAV></NAV>
        <Content></Content>
      </div>
    )
  }
}
export default App;
~~~

### 3개의 각 컴포넌트를 js 파일로 분리 - App.js, Subject.js, NAV.js, Content.js
- 컴포넌트가 하나의 파일에 많아지면 복잡
- 컴포넌트마다 js 파일로 분리해서 생성
- 분리된 컴포넌트를 사용하기 위해 import 해서 사용

~~~js
import React, { Component } from "react";
import './App.css';
import Subject from './components/Subject';
import NAV from './components/NAV';
import Content from './components/Content';

class App extends Component {
  render() {
    return (
      <div>
        <h3>안녕하세요.</h3>
        {/* 위에 추가한 컴포넌트 사용 : 태그 형식으로 사용한다. */}
        <Subject></Subject>
        <Subject></Subject>
        <NAV></NAV>
        <Content></Content>
      </div>
    )
  }
}
export default App;
~~~

~~~js
import React, { Component } from "react";
import App from "../App";

class Subject extends Component {
    render() {
      return (
        <header>
          <h1>Web</h1>
          world wide Web!
        </header>
      )
    }
}
export default Subject;
~~~

~~~js
import React, { Component } from "react";
import App from "../App";

class NAV extends Component {
    render() {
      return (
        <nav>
          <ul>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.html">CSS</a></li>
            <li><a href="3.html">JavaScript</a></li>
          </ul>
        </nav>
      )
    }
  }
export default NAV;
~~~

~~~js
import React, { Component } from "react";
import App from "../App";

class Content extends Component {
    render() {
      return (
        <article>
          <h2>HTML</h2>
          하이퍼 텍스트 기반 마크업 언어
        </article>
      )
    }
  }
export default Content;
~~~

## JSX 문법
- 자바스크립트 표현 사용
- if문 대신 조건 연산자(3항 연산 사용(조건? true:false))
- AND 연산자 __&&__ 사용한 조건부 렌더링
  - 조건이 true면 expression 반환
  - 조건이 false면 expression 반환하지 않고 무시(아무것도 출력되지 않음)
- OR 연산자 __||__ 사용한 조건부 렌더링
  - 조건이 0 또는 false이면 expression 반환
  - 0이 아니면 해당 값 출력
    - const number = 100;
    - { number || '내용...' }
    - 결과 : 100 출력
- 인라인 스타일링 : 카멜 표기법
  - css 코드 사이에 '-' 말고 대문자로 표기
    - background-color => backgroundColor
- class 대신 className 사용
- 태그는 반드시 닫아야 함 : \<br />, \<p />
- JSX 내에 자바스크립트 if문 사용
  - 변수처럼 { } 안에 함수 작성
- JSX 함수 정의, 함수 사용
  - render() 영역에 함수 작성
  - JSX 내부에서는 변수처럼 {  } 안에 함수명 작성

~~~js
import React, { Component } from 'react';

class JSX extends Component {
    render() {
    // 자바스크립트 코드 영역
    const name = '홍길동';
    const num = 0;
    const value = 1;


 // 변수 : 사용자 정의 객체
    const person = {
        name:'성춘향',
        age:20
    };
 // 자바스크립트 내부 함수
    function getPerson() {
        return person.name + ", " + person.age;
    }
 return (
        <div>
            {/* JSX 문법 영역 */}
            <h2>JSX 입니다.</h2>
            <h2>{name} 안녕!</h2>
            {/* 조건(삼항) 연산자 */}
            {/* 조건? true : false */}
            { name === '홍길동' ? (
            <h3>홍길동입니다.</h3>
            ) : (
            <h3>홍길동이 아닙니다.</h3>
            )}
            { name === '이몽룡' ? (<h3>이몽룡 입니다.</h3>) : (<h3>이몽룡이 아닙니다.</h3>) }
            { name === '홍길동' && <h3>홍길동 입니다.</h3>}
            { num || '값이 undefined 입니다.'}
            {/* 인라인 스타일링 : 카멜 표기법 */}
            <div
                style= {{
                    width:'50%',
                    backgroundColor:'red',
                    color:'white',
                    fontSize:'36px',
                    fontWeight:'bold',
                    padding:10,
                    marginTop:'20px'
                }}
                >인라인 스타일 적용!</div>

                {/* class 대신 className 사용 */}
                <div className='rect'>class style 적용</div>

                {/* 태그는 반드시 닫아야 함 */}
                <br />
                주소 : 서울 <br />
                전화 : 010-1111-1111 <br />
                <input type="password" />

                {/* JSX 내에 자바스크립트 if문 사용 가능한 방법 */}
                <div>
                    {
                        (function() {
                            if(value == 1) return <div>1 입니다.</div>
                            if(value == 2) return <div>2 입니다.</div>
                            if(value == 3) return <div>3 입니다.</div>
                        })() // <= () 에서 함수 호출이 이루어짐. (함수 자동 호출 ( function () { .... })() )
                    }
                </div>
                {/* JSX 내에 자바스크립트 if문 사용 가능한 방법 화살표 함수 */}
                <div>
                    {
                        ( () => {
                            if(value == 1) return <div>1 입니다.</div>
                            if(value == 2) return <div>2 입니다.</div>
                            if(value == 3) return <div>3 입니다.</div>
                        })() // <= () 에서 함수 호출이 이루어짐. (함수 자동 호출 ( function () { .... })() )
                    }
                </div>
                {/* render 영역 함수 사용 법 */}
                {/* 얘는 안됨. */}
                <div>getPerson()</div> <br />
                {/* 얘는 된다. */}
                <div>{ getPerson() }</div> <br />
        </div>
        );
    }
}
export default JSX;
~~~

## props
- 컴포넌트의 속성(값 설정)
- 부모 컴포넌트에서 자식 컴포넌트로 값 정달할 때 사용(읽기 전용)
- 컴포넌트 렌더링 할 때 값을 전달해 주고 싶을 때 사용
- 부모 컴포넌트 : App.js
  - \<Subject title="제목" sub="부제목">\</Subject>
- 자식 컴포넌트 : Subject.js
  - {this.props.title}을 원하는 곳에 적으면 부모 컴포넌트 title에 있는 값이 출력 됨

~~~js
class App extends Component {
  render() {
    return (
      <div>
        {/* <h3>안녕하세요.</h3> */}
        {/* 위에 추가한 컴포넌트 사용 : 태그 형식으로 사용한다. */}
        {/* <Subject></Subject>
        <NAV></NAV>
        <Content></Content> */}
        <JSX></JSX>
        <Subject title="제목" sub="부제목"></Subject>
      </div>
    )
  }
}
~~~

~~~js
class Subject extends Component {
    render() {
      return (
        <header>
          <h1>{this.props.title}</h1>
          {this.props.sub} <br />
          world wide Web!
        </header>
      )
    }
}
~~~

### 디폴트 props
- 기본 값으로 디폴트 props 설정 : 자식 컴포넌트에 설정
- 방법1 : 상단에 static으로 설정 (더 최신 방법)
- 방법2 : 하단에 클래스.defaultProps = { } 설정
- 주의 ! 2개 다 설정한 경우 나중에(아래) 설정한 것만 적용됨

~~~js
class Subject extends Component {
  // 디폴트 props 설정
  static defaultProps = {
    date:'2021-12-17'
  }
    render() {
      return (
        <header>
          <h1>{this.props.title}</h1>
          {this.props.sub} <br />
          {this.props.date} <br /> {/* 밑에 디폴트 props를 설정했기 때문에 출력되지 않음. */}
          {this.props.year} <br />
        </header>
      )
    }
}
// 방법 2 : 디폴트 props 설정
Subject.defaultProps = {
  year:2021
}
export default Subject;
~~~

### 연습문제 - App.js, Student.js

~~~js
<Student name="홍길동" age="20" address="서울"></Student>
~~~

~~~js
class Student extends Component {
    static defaultProps = {
        year:4
      }
    render() {
        
        return (
            <div>
                {this.props.name} <br />
                {this.props.age} <br />
                {this.props.address} <br />
                {this.props.year} <br />
            </div>
        );
    }
}
~~~