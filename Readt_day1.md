## 리액트 기본 리뷰
- 컴포넌트
- state
- props
- event
- router
- JSX 문법
- 데이터 바인딩 { name } , { props.name }
- 이미지 출력

### 컴포넌트 (component)
- 모듈 (부품 : 조립해서 사용)
- 재사용하기 위한 코드
- 페이지로 분리하기 위한 코드 영역 (Header.js)
- 태그 형식으로 사용 : \<Header>\</Header>

### state
- 컴포넌트 내부에서 변경될 수 있는 값
- (변수에 해당 : 값을 변경 가능)
- 값 변경시 
  - 클래스형 컴포넌트 : state = { } / setState() 함수 
  - 함수형 컴포넌트 : useState() 함수 사용
  - const [message, setMessage] = useState(‘값’);
  - let [color, setColor] = useState(‘값’);

### props
- 컴포넌트 속성 (값 설정)
- 상위 컴포넌트에서 하위 컴포넌트로 값을 전달할 때 사용 (읽기 전용)
- 상위 -> 하위 -> 하위 -> 하위
- 상위(name=”홍길동”) -> 하위 ({ props.name })

### event
- onClick = { 함수명 }
- onClick = { () => onRemove(id) }

### router
- 페이지 이동
- SPA : 현재 페이지로 삽입해서 보여 줌 (상태 정보 유지)
- react-router-dom 라이브러리 설치
- 링크 : \<Link to=”/aboub”>
- path : \<Route path=’/about element={<About />}>
- 파라미터 전달 
  - \<Route path=’/move/:keyword element={<Movie />}>
  - useParams() 사용

### 애플리케이션 구조
- App.js : 내용
- index.js : App.js를 렌더링
- index.html : 화면에 출력
- App.js(내용) -> index.js(렌더링) -> index.html(화면에 출력)

### App.js (최상위 컴포넌트)
- 다른 컴포넌트를 태그 형태로 포함
- \<Header>\</Header>
- \<Nav>\</Nave>
- \<Footer>\</Footer>
- 하위 컴포넌트로 props 전달
  - \<Nav name={name}>\</Nave>

### 리뷰 예제
- 프로젝트 : review-app
  - npx create-react-app review-app
- 실행 : npm start

### useState() 함수
- state 값 설정 함수
- 배열 반환 : [현재 상태(state), setter함수(state변경 함수)]
- setter 함수
  - 상태(state)를 변경(설정)하는 함수
  - 함수명은 임의로 작성 가능
    - let [title, setTitle] = useState("초기값");

###  배열 내장 함수 map()
- 각 배열의 요소에 대해 처리된 새로운 결과를 새로운 배열에 담아 반환하는 함수
- map()을 사용하여 컴포넌트로 변환활 때는 key 값 전달
- key 값은 각 항모의 고유값인 id로 사용

### 이벤트 처리 : [항목 추가] 버튼
- onClick=”{ 함수명 }”>
- 또는 화살표 함수 : onClick=”{ () =}”>
- \<button onClick=”{ }”>항목 추가\</button>
- 버튼 클릭시 미리 정의된 값 추가
  - 입력한 값이 추가되도록 변경
- 배열에 항목 추가
  - concat("추가할 내용");
    - titles.concat("지옥")
    - setTitle(titles.concat(item));
  - 스프레드 연산자 사용 : ...titles
    - setTitle([...titles, item]);
    - 기존값 유지
    - 객체 또는 배열의 값 복제할 때 사용
    - [...기존배열, 새항목] -> 새로운 배열로 만들어짐

### 각 항목에 삭제 버튼 추가
- 버튼 추가
- 이벤트 설정
- 배열에서 삭제할 때 filter() 함수 사용

### 배열 내장 함수 filter()
- 컴포넌트에서 배열의 불변성을 유지하면서 배열 원소를 제거해야 할 경우 사용
- 기존의 배열은 그대로 둔 상태에서 특정 조건을 만족하는 원소들만 따로 추출(필터링)해서 새로운 배열 생성
- 조건을 확인하는 함수를 파라미터로 설정
- 이 함수에서 true를 반환할 경우에만 새로운 배열에 포함시킴

~~~js
import logo from './logo.svg';
import './App.css';
import React, { useEffect, useState } from "react";

function App() {
  // 변수 사용도 가능
  // let title = "지금 우리 학교는"
  // state 사용하는 경우 useState() 사용 가능
  // let [title, setTitle] = useState("오징어 게임");
  // 값이 여러 개인 경우 배열로 설정
  let [titles, setTitle] = useState([
    "지금 우리 학교는",
    "오징어 게임"
  ]);

  // titles에 항목 추가  : state 값 변경
  // state 값 변경 함수 : setTitle() 함수
  const onClickAdd = () => {
    if(item == "") {
      alert("제목을 입력하세요");
    }
    else{
    // 배열에 항목 추가
    // 1. concat("추가할 내용")
    // setTitle(titles.concat(item)); // 배열에 입력된 값 item 추가
    // setItem(''); // 입력란 지우기
    // 2. 스프레드 연산자 사용 : ...titles (객체 또는 배열의 값 복제할 때 사용)
    setTitle([...titles, item])
    setItem(''); // 입력란 지우기
    }
  }

  // 입력값 저장하기 위한 state 정의
  let [item, setItem] = useState('');

  const onItemChange = e => setItem(e.target.value);

  const onItemRemove = (title, index) => {
    // 전달 받은 인덱스에 해당하는 titles의 title이 동일한 것은 제외하고 새배열로 반환
    setTitle(titles.filter((title) => titles[index] != title));
  };
  
  return (
    <div className="App">
      <div className='header'>
        <h3>인기 컨텐츠</h3>
      </div>
      
      <div className='content'>
        {
          titles.map((title, index) => (
            <div>
              <p>{index} : {title}</p>
              <button title={title} index={index} onClick={ () => onItemRemove(title, index) }>삭제</button>
              <hr/>
            </div>
          ))
        }
        <input type="text" value={item} name="item" onChange={onItemChange} />
        <button onClick={onClickAdd}>항목 추가</button>
      </div>

      {/* <div className='content'>
        <p>{ titles[0] }</p>
        <hr/>
      </div>

      <div className='content'>
        <p>{ titles[1] }</p>
        <hr/>
      </div> */}
    </div>
  );
}
export default App;
~~~

### 컴포넌트로 분리
- App.js
- components 폴더 생성
  -  Header.js
  -  Content.js