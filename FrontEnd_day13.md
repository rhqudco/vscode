## state
- 컴포넌트에서 내부에서 변경될 수 있는 값
- 이 값이 변경될 때마다 리 렌더링 됨
- 값을 변경할 때는 반드시 setState() 함수(메소드) 사용
- setState() 함수 사용하지 않고 직접 변경하면 리 렌더링 하지 않음
- state 선언
  - state = { number:0 }
- state 사용
  - { this.state.number }
  - 반드시 __this__ 붙임
- setState() 함수 사용해서 변경
  - this.setState( { number: this.state.number + 1 } );
- props와 state 비교
  - props : 부모 컴포넌트가 자식 컴포넌트에게 넘겨주는 값, 읽거 전용
  - state : 컴포넌트 자신이 갖고 있는 값, 변경 가능

### state 예제 - Counter.js, App.js

~~~js
class Counter extends Component {
    state = {
        number : 0
    }
    // 여기에 이벤트 핸들러 삽입
    increaseCounter = () => {
        // state 값 1 증가
        // state 값 변경할 때는 this.setState() 사용
        this.setState({
            number : this.state.number + 1
        });
    };
    decreaseCounter = () => {
        // state 값 1 감소
        this.setState({
            number : this.state.number - 1
        });
    };
    render() {
        return (
            <div>
                <h2>카운터</h2>
                <div>값 : {this.state.number}</div>
                <button onClick={this.increaseCounter}> + </button> &nbsp;
                <button onClick={this.decreaseCounter}> - </button> &nbsp;
                {/* 버튼에 직접 함수 포함 가능 */}
                <button
                onClick = { () => {
                    this.setState({
                        number : this.state.number + 10
                    })
                }}>
                 + 10 </button> &nbsp;
                <button
                onClick = { () => {
                    this.setState({
                        number : this.state.number - 10
                    })
                }}>
                 - 10 </button>
            </div>
        );
    }
}
~~~

~~~js
class App extends Component {
  render() {
    return (
      <div className='App'>
        <h1>State 연습</h1>
        <Counter></Counter>
      </div>
    );
  }
}
~~~

====================================================================================================================================

## 이미지 출력 \<img>
- 방법 1 : import
  - src 안에 images 폴더 생성 후 이미지 저장
  - 이미지를 사용하는 컴포넌트에서 이미지 import
    - import imgApple from '../images/apple.png';
  - 이미지 출력
    - \<img src={imgApple} ... />
- 방법 2 : public 내에 assets 폴더 만들고 그 안에 이미지 파일 저장
  - 이 방법은 import가 되지 않는다.
  - 이미지 출력
    - \<img src='/assets/apple.png' />
- 방법 3 : state를 활용한 변수로의 이미지 출력
  - state 변수에 이미지를 저장하고 출력한다.

### 방법 1 : import - Image.js

~~~js
import React, { Component } from 'react';
import imgApple from '../images/apple.png';
import imgBanana from '../images/banana.png';

class Image extends Component {
    render() {
        return (
            <div>
                <img src={imgApple} /> <br />
                <img src={imgBanana} />
            </div>
        );
    }
}
~~~

### 방법 2 : public 내에 assets 폴더 만들고 그 안에 이미지 파일 저장 - Image.js

~~~js
import React, { Component } from 'react';

class Image extends Component {
    render() {
        return (
            <div>
                <img src="/assets/black.png" alt="black" /> 
                <img src="/assets/pink.png" alt="black" /> <br />
            </div>
        );
    }
}
~~~

### 방법 3 : state를 활용한 변수로의 이미지 출력 - Image.js

~~~js
import React, { Component } from 'react';

import imgLizard from '../images/lizard.png';
import imgLizardon from '../images/lizardon.png';

class Image extends Component {
    state = {
        imgA : imgLizard,
        imgB : imgLizardon
    }
    render() {
        return (
            <div>
                <img src={this.state.imgA} alt="lizard" />
                <img src={this.state.imgB} alt="lizardon" /><br />
            </div>
        );
    }
}
~~~

====================================================================================================================================

## 함수형 컴포넌트에서 state 사용하기
- React 버전 16.8 이전 버전에서는 함수형 컴포넌트에서 state를 사용할 수 없었다.
- 이후 버전에서 useState()를 통해 state 사용 가능
  - 이 과정에서 Hooks라는 것을 사용
- Hooks
  - 16.8 버전에서 새로 도입된 기능
  - 기존의 함수형 컴포넌트에서 할 수 없었던 다양한 기능 제공
  - useState() : 상태 관리
  - useEffect() : 렌더링 직후 작업 설정
- 배열의 비구조화 할당
  - 배열의 요소 값을 쉽게 추출하기 위한 문법
  - 기존 방법
    - const array = [1, 2];
    - const one = array[0];
    - const two = array[1];
  - 배열의 비구조화 할당 방법
    - const array = [1, 2];
    - const [one, two] = araay;
- useState() 사용해서 함수형 컴포넌트에서 state 사용
  - useState(초기값)
    - 초기값으로 숫자, 문자, 객체, 배열 가능
    - 배열 반환 : [현재 상태, setter 함수]
    - setter 함수
      - 상태를 변경(설정)하는 함수
      - 이름은 임의로 사용 가능
    - 사용 예 1
      - const [message. steMessage] = useState(''); (message에 초기 값 없음.)
      - steMessage('안녕하세요'); (message 값을 '안녕하세요'로 변경(설정))
    - 사용 예 2
      - const[color, setColor] = useState('black'); (color 초기 값은 'black');
      - setColor('green'); (color 값을 'green' 으로 변경(설정))

### useState() 사용해서 함수형 컴포넌트에서 state 사용 - Message.js

~~~js
import React, {useState} from 'react';
// { Component } 클래스 없음.
// { useState } 포함 (모듈을 import 했음)

const Message = () => {
    const [message, setMessage] = useState('');
    // 이벤트 핸들러 추가
    // lambda 식 한 줄이라 { } 생략
    const onClickEnter = () => setMessage('안녕하세요!');
    const onClickLeave = () => setMessage('안녕히 가세요!');
    const onClickClear = () => setMessage('');
    // 색상 변경 state
    const [color, setColor] = useState('black');
    // 이벤트 핸들러 추가
    const onClickGreen = () => setColor('green');
    const onClickRed = () => setColor('red');
    const onClickBlue = () => setColor('blue');
    return (
        <div>
            <p></p>
            {/* 출력되는 message 문자열 변경 버튼 */}
            <button onClick={onClickEnter}> 입장 </button> &nbsp;
            <button onClick={onClickLeave}> 퇴장 </button> &nbsp;
            <button onClick={onClickClear}> 지우기 </button>
            {/* 출력되는 message 색상 변경 버튼 추가 : green, red, blue */}
            <br /><br />
            <button style={ {color : 'green'} } onClick={onClickGreen}> Green </button> &nbsp;
            <button style={ {color : 'red'} } onClick={onClickRed}> Red </button> &nbsp;
            <button style={ {color : 'blue'} } onClick={onClickBlue}> Blue </button> &nbsp;
            <button onClick={ () => setColor('black') }> Black </button>
            {/* style={ {color} } {color}를 감싸는 {}는 style 적용을 위한 {}이고, color를 감싸는 {}는 변수 처리를 위한 {}이다. */}
            <h1 style={ {color} }> {message} </h1>
            <br /><br /><br /><br /><br />
        </div>
    );
};
export default Message;
~~~

====================================================================================================================================

## 이벤트 처리 시 주의점
- 이벤트 이름은 카멜 표기법 사용 : onClick@@@, onKeyUp@@@, onChange@@@
- 이벤트에 이벤트 핸들러 함수 형태의 값 전달
  - onClick = {onClickEnter}
  - onClick = { () => setColor('green') }
- 이벤트는 DOM 요소에만 설정 가능
  - 사용자가 만든 컴포넌트에는 이벤트 설정 불가
  - onClick을 props로 전달해서 컴포넌트 내부의 DOM 이벤트로 설정 가능
  - 예 : MyComponent에 onClick 설정 시
    - \<MyComponent onClick = {eventHandler} /> 했을 때 클릭 시 __eventHandler()__ 함수를 실행하는 것이 아니라 이름이 onClick인 props를 MyComponent에 전달하는 것
    - 전달받은 props를 컴포넌트 내부의 DOM 이벤트로 설정 가능
      - \<div onClick = {this.props.onClick} >\</div>

### onChange 이벤트 - Event.js, App.js
- 클래스형 컴포넌트 Event 생성
- state 선언 / setState() 사용해서 state 변경
- 이벤트 객체 받아와서 이벤트가 발생한 대상의 값으로 state 값 변경

~~~js
import React, { Component } from 'react';

class Event extends Component {
    state = {
        message: ''
    }
    // 이벤트 핸들러
    onChange = e => {
        this.setState({
            message: e.target.value
        })
    };
    render() {
        return (
            <div>
                <hr />
                <h3>이벤트 연습</h3>
                <input type="text" name='message'
                        onChange={this.onChange} />
                <h3>{this.state.message}</h3>
            </div>
        );
    }
}

export default Event;
~~~

~~~js
import React, { Component } from 'react';
import './App.css'
import Counter from './components/Counter';
import Image from './components/Image';
import Message from './components/Message';
import Event from './components/Event';

class App extends Component {
  render() {
    return (
      <div className='App'>
        <h1>State 연습</h1>
        <Counter></Counter>
        <Image></Image>
        <Message></Message>
        <Event></Event>
      </div>
    );
  }
}

export default App;
~~~

### onChange 이벤트 로그인 연습문제 - Login.js, App.js

~~~js
import React, { Component } from 'react';

class Login extends Component {
    state = {
        id : '',
        pass : ''
    }
    onIdChange = e => {
        this.setState({
            id: e.target.value
        })
    };
    onPassChange = e => {
        this.setState({
            pass: e.target.value
        })
    };

    onShow = () => {
        if(this.state.id == 'abcd' && this.state.pass == '1234') {
            alert("로그인 성공")
        }
        else {
            alert("로그인 실패")
        }
    };
    render() {
        return (
            <div>
                아이디 : <input type='text' name='id' size='10'
                    value={this.state.id}
                    onChange={this.onIdChange} /> &nbsp;
                    <br />
                비밀번호 : <input type='password' name='pass' size='10'
                    value={this.state.pass}
                    onChange={this.onPassChange} /> &nbsp;

                <button onClick={this.onShow}> 완료 </button>
            </div>
        );
    }
}

export default Login;
~~~

~~~js
import React, { Component } from 'react';
// ... // 
import Login from './components/Login';

class App extends Component {
  render() {
    return (
      <div className='App'>
        <h1>State 연습</h1>
        <Counter></Counter>
        <Image></Image>
        <Message></Message>
        <Event></Event>
        <Login></Login>
      </div>
    );
  }
}
~~~

====================================================================================================================================

## Router
- MPA(Multiple Page Application)
  - 기존 웹페이지 작동 원리
  - Server Side Rendering
  - 사용자가 다른 페이지로 이동할 때(\<a> 태그 사용) 마다 새로운 HTML을 받아오고 페이지를 로딩할 때 마다 서버에서 리소스 전달 받아 해석한 뒤 화면에 출력
  - 사용자에게 보이는 화면을 서버에서 준비하여 전달
  - 웹 출력 내용이 많은 경우 새로운 하면을 보여줄 때 마다 서버 측에서 모든 뷰를 준비
    - 성능 문제 발생
      - 사용하고 있는 상태 유지하는 작업이 번거로움
      - 변경되지 않은 부분까지 새로 불러와야 하므로 불필요한 로딩이 있어 비효율적
      - 캐싱과 압축 기능으로 최적화는 가능.
      - 사용자와의 인터렉션이 자주 발생하는 모던 웹 애플리케이션에서는 부적합
- SPA(Single Page Application)
  - Client Side Rendering
  - 리액트 등과 같은 라이브러리 또는 프레임워크에서 뷰 렌더링을 사용자의 웹 브라우저가 담당하도록 하고 먼저 애플리케이션을 브라우저에서 불러와 실행
  - 사용자와의 인터렉션이 발생할 경우 필요한 부분만 자바스크립트를 사용하여 업데이트 함
  - 새로운 데이터가 필요한 경우 서버 API를 호출하여 필요한 데이터만 새로 불러와 애플리케이션에서 사용
  - SPA의 경우 서버에서 사용자에게 제공하는 페이지는 한 종류이지만 해당 페이지에서 로딩된 자바스크립트와 현재 사용자 브라우저 주소 상태에 따라 다양한 화면 출력
  - 단점
    - 웹의 규모가 커지면 자바스크립트 파일도 너무 커진다는 문제
      - 코드 스플리팅 사용하면 라우트별로 파일들을 나누어 트래픽과 로딩 속도 개선 가능
    - 크롤링 문제
      - 브라우저에서 자바스크립트를 사용하여 라우팅을 관리하는 경우 자바스크립트를 실행하지 않는 일반 크롤러에서 페이지 정보를 제대로 수집하지 못 함
      - 자바스크립트 부분만 있고 컨텐츠가 페이지에 보이지 않음
      - 검색 엔진(구글, 네이버, 다음 등..)에 따라 검색 결과에 페이지가 잘 나타나지 않을 수 있다.
    - 보안 문제
      - Server Side Rendering인 경우 사용자에 대한 정보를 서버측에서 세션으로 관리하지만, Client Side Rendering인 경우 클라이언트 측 쿠키 외에는 사용자에 대한 정보를 저장할 공간이 마땅하지 않다.
- 라우팅(Routing)
  - 다른 URL 주소에 따라 다른 화면을 보여 주는 것 (페이지 이동)
  - 이전 : 새 페이지로 이동 (상태 정보 잃음)
  - SPA : 현재 페이지로 삽입 해서 보여 줌 (상태 정보 유지)
  - 리액트 라이브러리 자체에 라우팅 기능이 내장되어 있지 않고 라우터 라이브러리 설치해서 쉽게 구현 가능
  - react-router-dom 라이브러리 설치 필요 (현재 V6)
    - V6로 바뀐지 오래되지 않았지만 공식버전으로 채택
- 라우팅 기능 추가
1. react-router-dom 라이브러리 설치
2. index.js 
   - import { BrowserRouter } from ‘react-router-dom’
        ~~~js
        <BrowserRouter> 
        <App /> 
        </BrowserRouter>
        ~~~
3. Route 컴포넌트로 특정 주소에 연결

    ~~~js
    import { Link, Routes, Route } from ‘react-router-dom’
    <Routes>
    <Route path=’/’ element={ <Home />} />
    <Route path=’/about’ element={<About />} />
    </Routes>
    ~~~
  
4. 라우터 설치
   - 설치할 프로젝트 경로에서 npm install react-router-dom

- Link 컴포넌트를 사용하여 다른 주소로 이동
  - 리액트 라우터를 사용할 때는 \<a> 태그 사용하지 않음
    - 완전 새로운 페이지로 이동할 때는 사용
    - \<a> 태그는 페이지를 전환하는 과정에서 페이지를 새로 불러오기 때문에 애플리케이션이 갖고 있던 상태들이 모두 없어짐
  - \<Link> 태그 사용
  - 페이지를 새로 불러오지 않고 애플리케이션은 그대로 유지한 상태에서 페이지의 주소만 변경
  - 페이지 전환 기능이 내장되어 있음
  - \<Link to=’주소’>홈 화면 보기\</Link>

### 라우트로 사용 컴포넌트 페이지 index.js, App.js, Home.js, About.js, Content.js

~~~js
ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
~~~

~~~js
import { Link, Routes, Route } from 'react-router-dom';
import About from './components/About';
import Home from './components/Home';
import Content from './components/Content';

function App() {
  return (
    <div className="App">
      <ul>
        <li>
          <Link to="/">홈 화면 보기</Link>
        </li>
        <li>
          <Link to="/about">About 화면 보기</Link>
        </li>
        <li>
          <Link to="/Content">전체 도서 정보 출력</Link>
        </li>
      </ul>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/content" element={<Content />} />
      </Routes>
    </div>
  );
}

export default App;
~~~

~~~js
function Home() {
    return (
      <div className="App">
        <h1>홈 입니다</h1>
        <h3>방문을 환영합니다</h3>
      </div>
    );
  }
  
  export default Home;
~~~

~~~js
function About() {
    return (
      <div className="App">
          <h1>브라우저 설명</h1>
      </div>
    );
  }
  
  export default About;
~~~

~~~js
unction Content() {
    return (
        <div>
            <hr />
            <h2>책 정보</h2>
            <table border='1'>
                <tr><th>제목</th><th>저자</th><th>평점</th></tr>
                <th>출간일</th><th>장르</th>
                <tr><td>개미</td>
                <td>베르나르 베르베르</td><td>5.0점</td>
                <td>1991년</td><td>소설</td></tr>
                <tr><td>데미안</td>
                <td>헤르만 헤세</td><td>4.8점</td>
                <td>1919년</td><td>소설</td></tr>
            </table>
        </div>
    )
}
export default Content;
~~~

### URL 파라미터 사용하기 : path를 통해 파라미터 전달 - App.js, Book.js

~~~js
import { Link, Routes, Route } from 'react-router-dom';
import About from './components/About';
import Home from './components/Home';
import Content from './components/Content';
import Book from './components/Book';

function App() {
  return (
    <div className="App">
      <ul>
        <li>
          <Link to="/">홈 화면 보기</Link>
        </li>
        <li>
          <Link to="/Book/ant">개미</Link>
        </li>
        <li>
          <Link to="/Book/demian">데미안</Link>
        </li>
        <li>
          <Link to="/Book/threeKingdoms">삼국지</Link>
        </li>
      </ul>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/book/:keyword" element={<Book />} />
      </Routes>
    </div>
  );
}

export default App;
~~~

~~~js
import { useParams } from "react-router-dom";

const data = {
    ant : {
        title : '개미',
        director : '베르나르 베르베르',
        score : '5.0',
        date : '1991년',
        genre : '소설'
    },
    demian : {
        title : '데미안',
        director : '헤르만 헤세',
        score : '4.8점',
        date : '1919년',
        genre : '소설'
    }
}

function Book() {
    const params = useParams();
    const book = data[params.keyword];

    if(!book) {
        return <div><hr /><div>책 정보가 없습니다.</div></div>;
    }
    return (
        <div>
            <hr />
            <h3> 
                {params.keyword} : {book.title} 
            </h3>
            <p> 저자 : {book.director} </p>
            <p> 평점 : {book.score} </p>
            <p> 출간일 : {book.date} </p>
            <p> 장르 : {book.genre} </p>
        </div>
    )
}
export default Book;
~~~