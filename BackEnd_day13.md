# 로그인 기능

## 페이지 구성

### top.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>Top</title>
        <link rel="stylesheet" href="/css/common.css" type="text/css">
        <link rel="stylesheet" href="/css/index.css" type="text/css">
        <link rel="stylesheet" href="/css/menu.css" type="text/css">
        <link rel="stylesheet" href="/css/slideShow.css" type="text/css">
        <link rel="stylesheet" href="/css/tabMenu.css" type="text/css">
        <link rel="stylesheet" href="/css/product.css" type="text/css">
        <script src="/js/jquery-3.6.0.min.js"></script>
        <script src="/js/subMenu.js"></script>
        <script src="/js/slideShow.js"></script>
        <script src="/js/tabMenu.js"></script>
        <script src="/js/index.js"></script>
    </head>
    <body>
    <div id="wrap">
            <header>
                <div id="headerBox">
                    <div id="logoBox"><a href="index.html"><img src="/images/logo.png" id="logoImg"></a></div>
                    <div id="topMenuBox">로그인 이벤트 장바구니 고객센터 회원가입</div>
                </div>
            </header>
            <nav>
                <div id="mainMenuBox">
                    <ul id="menuItem">
                        <li><a href="#">SPECIAL</a></li>
                        <li><a href="#">메뉴 항목1</a></li>
                        <li><a href="#">메뉴 항목2</a></li>
                        <li><a href="#">메뉴 항목3</a></li>
                        <li><a href="#">메뉴 항목4</a></li>
                        <li><a href="#" id="showAllMenu">전체 보기</a></li>
                    </ul>
                </div>
                <!-- mainMenuBox 끝 -->
                <div id="subMenuBox">
                    <div class="subMenuItem" id="subMenuItem1">
                        <ul>
                            <li><a href="#">subMenuItem 1-1</a></li>
                            <li><a href="#">subMenuItem 1-2</a></li>
                            <li><a href="#">subMenuItem 1-3</a></li>
                            <li><a href="#">subMenuItem 1-4</a></li>
                        </ul>
                    </div>
                    <div class="subMenuItem" id="subMenuItem2">
                        <ul>
                            <li><a href="#">subMenuItem 2-1</a></li>
                            <li><a href="#">subMenuItem 2-2</a></li>
                            <li><a href="#">subMenuItem 2-3</a></li>
                            <li><a href="#">subMenuItem 2-4</a></li>
                        </ul>
                    </div>
                    <div class="subMenuItem" id="subMenuItem3">
                        <ul>
                            <li><a href="#">subMenuItem 3-1</a></li>
                            <li><a href="#">subMenuItem 3-2</a></li>
                            <li><a href="#">subMenuItem 3-3</a></li>
                            <li><a href="#">subMenuItem 3-4</a></li>
                        </ul>
                    </div>
                    <div class="subMenuItem" id="subMenuItem4">
                        <ul>
                            <li><a href="#">subMenuItem 4-1</a></li>
                            <li><a href="#">subMenuItem 4-2</a></li>
                            <li><a href="#">subMenuItem 4-3</a></li>
                            <li><a href="#">subMenuItem 4-4</a></li>
                        </ul>
                    </div>
                    <div class="subMenuItem" id="subMenuItem5">
                        <ul>
                            <li><a href="#">subMenuItem 5-1</a></li>
                            <li><a href="#">subMenuItem 5-2</a></li>
                            <li><a href="#">subMenuItem 5-3</a></li>
                            <li><a href="#">subMenuItem 5-4</a></li>
                        </ul>
                    </div>
                    <div class="subMenuItem" id="subMenuItem6">
                        <ul>
                            <li><a href="#">subMenuItem 6-1</a></li>
                            <li><a href="#">subMenuItem 6-2</a></li>
                            <li><a href="#">subMenuItem 6-3</a></li>
                            <li><a href="#">subMenuItem 6-4</a></li>
                        </ul>
                    </div>
                </div>
                <!-- subMenuBox 끝 -->
            </nav>
        </div>
        </body>
</html>

~~~

### index.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>프로젝트 : index</title>
    <link rel="stylesheet" href="/css/common.css" type="text/css">
    <link rel="stylesheet" href="/css/index.css" type="text/css">
    <link rel="stylesheet" href="/css/menu.css" type="text/css">
    <link rel="stylesheet" href="/css/slideShow.css" type="text/css">
    <link rel="stylesheet" href="/css/tabMenu.css" type="text/css">
    <link rel="stylesheet" href="/css/product.css" type="text/css">
    <script src="/js/jquery-3.6.0.min.js"></script>
    <script src="/js/subMenu.js"></script>
    <script src="/js/slideShow.js"></script>
    <script src="/js/tabMenu.js"></script>
    <script src="/js/index.js"></script>
</head>
<body>
    <div id="wrap">
<!--    TOP    -->
        <jsp:include page="layout/top.jsp" flush="true" />
        <section>
            <article id="slideShow">
                <!-- 이전, 다음 버튼 -->
                <div id="prevNextButtonBox">
                    <img src="/images/prevButton.png" id="prevButton">
                    <img src="/images/nextButton.png" id="nextButton">
                </div>
                <div id="slideShowBox">
                    <div id="slidePanel">
                        <img src="/images/slide_img_01.jpg" class="slideImage">
                        <img src="/images/slide_img_02.jpg" class="slideImage">
                        <img src="/images/slide_img_03.jpg" class="slideImage">
                        <img src="/images/slide_img_04.jpg" class="slideImage">
                        <img src="/images/slide_img_05.jpg" class="slideImage">
                    </div>
                </div>
                <!-- slideShowBox 끝 -->
                <div id="controlPanel">
                    <img src="/images/controlButton1.png" class="controlButton">
                    <img src="/images/controlButton1.png" class="controlButton">
                    <img src="/images/controlButton1.png" class="controlButton">
                    <img src="/images/controlButton1.png" class="controlButton">
                    <img src="/images/controlButton1.png" class="controlButton">
                </div>
            </article>

            <article id="content1"> <!-- 텝 메뉴 -->
                <div id="tabMenuBox">
                    <div id="tabMenu">
                        <ul id="tab">
                            <li><img src="/images/tab1.png"></li>
                            <li><img src="/images/tab2.png"></li>
                            <li><img src="/images/tab3.png"></li>
                            <li><img src="/images/tab4.png"></li>
                        </ul>
                    </div>
                    <div id="tabContent">
                        <div><a href="#"><img src="/images/tab_img_01.jpg"></a></div>
                        <div><a href="#"><img src="/images/tab_img_02.jpg"></a></div>
                        <div><a href="#"><img src="/images/tab_img_03.jpg"></a></div>
                        <div><a href="#"><img src="/images/tab_img_04.jpg"></a></div>
                    </div>
                </div>
            </article>

            <article id="content2"> <!-- 베스트 상품 -->
                <div id="productBox">
                    <h3>베스트 상품</h3>
                    <div class="product">
                        <div><a href=""><img src="/images/prd01.jpg"></a></div>
                        <div><a href=""><img src="/images/prd02.jpg"></a></div>
                        <div><a href=""><img src="/images/prd03.jpg"></a></div>
                    </div>
                    <div class="product">
                        <div><a href=""><img src="/images/prd04.jpg"></a></div>
                        <div><a href=""><img src="/images/prd05.jpg"></a></div>
                        <div><a href=""><img src="/images/prd06.jpg"></a></div>
                    </div>
                </div>
            </article>
        </section>
<!--  BOTTOM  -->
        <jsp:include page="layout/bottom.jsp" flush="true" />
    </div>
</body>
</html>
~~~

### bottom.jsp

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>Bottom</title>
      <link rel="stylesheet" href="/css/common.css" type="text/css">
      <link rel="stylesheet" href="/css/index.css" type="text/css">
      <link rel="stylesheet" href="/css/menu.css" type="text/css">
      <link rel="stylesheet" href="/css/slideShow.css" type="text/css">
      <link rel="stylesheet" href="/css/tabMenu.css" type="text/css">
      <link rel="stylesheet" href="/css/product.css" type="text/css">
      <script src="/js/jquery-3.6.0.min.js"></script>
      <script src="/js/subMenu.js"></script>
      <script src="/js/slideShow.js"></script>
      <script src="/js/tabMenu.js"></script>
      <script src="/js/index.js"></script>
  </head>
  <body>
    <div id="wrap">
        <footer>
            <div id="footerBox">
                <div id="bottomMenuBox">
                    <ul id="bottomMenuItem">
                        <li><a href="#">회사소개</a></li>
                        <li><a href="#">이용약관</a></li>
                        <li><a href="#">개인정보 처리방침</a></li>
                        <li><a href="#">전자금융거래약관</a></li>
                        <li><a href="#">보안센터</a></li>
                        <li><a href="#">채용정보</a></li>
                    </ul>
                </div>
                <div id="companuInfo"><img src="/images/footer.png"></div>
                <div id="moveToTopBox"><img src="/images/moveToTop.png" id="moveToTop"></div>
            </div>
        </footer>
    </div>
  </body>
</html>
~~~

## 서버 구성
- MemberVO
- IMemberService
- MemberService
- IMemberDAO
- MemberController
- MemberMapper.xml