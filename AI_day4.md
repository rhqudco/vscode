## CLOVA Chatbot
- 챗봇 제작 API 서비스
- 사용자의 질문 의도를 이해하여 고객 대응 등 다양한 서비스에 활용할 수 있는 Chatbot 제작 지원
- (1) 도메인 생성
  - Products & Services / CLOVA Chatbot
- (2) 빌더 실행하기
- (3) 대화 생성
- (4) 챗봇 빌드
- (5) 챗봇 테스트
- (6) 우측 상단에서 [서비스 배포]
  - [Custom API Gateway와 End-point 연결이필요합니다] / [연동]
  - APIGW 연동 설정
    - [자동 연동] / [확인]
    - [주소 복사]
  - 메신저 연동 설정
    - Secret Key [생성] / [복사]
  - 연동 완료
- (7) 스프링에서 작업

### 스프링에서 챗봇 서비스 구현 실습
- (1) 질문 메시지 전달하고 콘솔창에서 응답 메시지 출력 확인

~~~java
@Service
public class ChatbotService {
    public static String main(String voiceMessage) {
        String secretKey = "";
        String apiURL = "";

        String chatbotMessage = ""; // 응답 메세지
        try {
            //String apiURL = "https://ex9av8bv0e.apigw.ntruss.com/custom_chatbot/prod/";

            URL url = new URL(apiURL);

            String message = getReqMessage(voiceMessage);
            System.out.println("##" + message);

            String encodeBase64String = makeSignature(message, secretKey);

            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Content-Type", "application/json;UTF-8");
            con.setRequestProperty("X-NCP-CHATBOT_SIGNATURE", encodeBase64String);

            // post request
            con.setDoOutput(true);
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            wr.write(message.getBytes("UTF-8"));
            wr.flush();
            wr.close();
            int responseCode = con.getResponseCode();

            BufferedReader br;

            if(responseCode==200) { // Normal call
                System.out.println(con.getResponseMessage());

                BufferedReader in = new BufferedReader(
                        new InputStreamReader(
                                con.getInputStream()));
                String decodedString;
                while ((decodedString = in.readLine()) != null) {
                    chatbotMessage = decodedString;
                }
                //chatbotMessage = decodedString;
                in.close();
                // 응답 메세지 출력
                System.out.println(chatbotMessage);
            } else {  // Error occurred
                chatbotMessage = con.getResponseMessage();
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return chatbotMessage;
    }

    public static String makeSignature(String message, String secretKey) {

        String encodeBase64String = "";

        try {
            byte[] secrete_key_bytes = secretKey.getBytes("UTF-8");

            SecretKeySpec signingKey = new SecretKeySpec(secrete_key_bytes, "HmacSHA256");
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(signingKey);

            byte[] rawHmac = mac.doFinal(message.getBytes("UTF-8"));
//            encodeBase64String = Base64.encodeToString(rawHmac, Base64.NO_WRAP);
            encodeBase64String = Base64.getEncoder().encodeToString(rawHmac);

            return encodeBase64String;

        } catch (Exception e){
            System.out.println(e);
        }

        return encodeBase64String;

    }

    public static String getReqMessage(String voiceMessage) {

        String requestBody = "";

        try {

            JSONObject obj = new JSONObject();

            long timestamp = new Date().getTime();

            System.out.println("##"+timestamp);

            obj.put("version", "v2");
            obj.put("userId", "U47b00b58c90f8e47428af8b7bddc1231heo2");
//=> userId is a unique code for each chat user, not a fixed value, recommend use UUID. use different id for each user could help you to split chat history for users.

            obj.put("timestamp", timestamp);

            JSONObject bubbles_obj = new JSONObject();

            bubbles_obj.put("type", "text");

            JSONObject data_obj = new JSONObject();
            data_obj.put("description", voiceMessage);

            bubbles_obj.put("type", "text");
            bubbles_obj.put("data", data_obj);

            JSONArray bubbles_array = new JSONArray();
            bubbles_array.put(bubbles_obj);

            obj.put("bubbles", bubbles_array);
            obj.put("event", "send");

            requestBody = obj.toString();

        } catch (Exception e){
            System.out.println("## Exception : " + e);
        }
        return requestBody;
    }
}
~~~

~~~java
	// 챗봇 질문 전송하고 결과 받아서 출력
	@RequestMapping("/chatbot")
	public void chatbot() {
		String result = ChatbotService.main("넌 누구니"); // 메소드가 static이라 클래스로 호출해야 함
		System.out.println(result);
	}
~~~

- (2) APIRestController 사용
  - 뷰 페이지 폼 입력란에서 질문 메시지 입력하고 응답 메시지 출력

~~~java
@Service
public class ChatbotService {
//    public static String main(String voiceMessage) {
    public String main(String voiceMessage) {
        String secretKey = "";
        String apiURL = "";

        String chatbotMessage = ""; // 응답 메세지
        try {
            //String apiURL = "https://ex9av8bv0e.apigw.ntruss.com/custom_chatbot/prod/";

            URL url = new URL(apiURL);

            String message = getReqMessage(voiceMessage);
            System.out.println("##" + message);

            String encodeBase64String = makeSignature(message, secretKey);

            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Content-Type", "application/json;UTF-8");
            con.setRequestProperty("X-NCP-CHATBOT_SIGNATURE", encodeBase64String);

            // post request
            con.setDoOutput(true);
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            wr.write(message.getBytes("UTF-8"));
            wr.flush();
            wr.close();
            int responseCode = con.getResponseCode();

            BufferedReader br;

            if(responseCode==200) { // Normal call
                System.out.println(con.getResponseMessage());

                BufferedReader in = new BufferedReader(
                        new InputStreamReader(
                                con.getInputStream()));
                String decodedString;
                while ((decodedString = in.readLine()) != null) {
                    chatbotMessage = decodedString;
                }
                //chatbotMessage = decodedString;
                in.close();
                // 응답 메세지 출력
                System.out.println(chatbotMessage);
                chatbotMessage = jsonToString(chatbotMessage);
            } else {  // Error occurred
                chatbotMessage = con.getResponseMessage();
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return chatbotMessage;
    }

    public static String makeSignature(String message, String secretKey) {

        String encodeBase64String = "";

        try {
            byte[] secrete_key_bytes = secretKey.getBytes("UTF-8");

            SecretKeySpec signingKey = new SecretKeySpec(secrete_key_bytes, "HmacSHA256");
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(signingKey);

            byte[] rawHmac = mac.doFinal(message.getBytes("UTF-8"));
//            encodeBase64String = Base64.encodeToString(rawHmac, Base64.NO_WRAP);
            encodeBase64String = Base64.getEncoder().encodeToString(rawHmac);

            return encodeBase64String;

        } catch (Exception e){
            System.out.println(e);
        }

        return encodeBase64String;

    }

    public static String getReqMessage(String voiceMessage) {

        String requestBody = "";

        try {

            JSONObject obj = new JSONObject();

            long timestamp = new Date().getTime();

            System.out.println("##"+timestamp);

            obj.put("version", "v2");
            obj.put("userId", "U47b00b58c90f8e47428af8b7bddc1231heo2");
//=> userId is a unique code for each chat user, not a fixed value, recommend use UUID. use different id for each user could help you to split chat history for users.

            obj.put("timestamp", timestamp);

            JSONObject bubbles_obj = new JSONObject();

            bubbles_obj.put("type", "text");

            JSONObject data_obj = new JSONObject();
            data_obj.put("description", voiceMessage);

            bubbles_obj.put("type", "text");
            bubbles_obj.put("data", data_obj);

            JSONArray bubbles_array = new JSONArray();
            bubbles_array.put(bubbles_obj);

            obj.put("bubbles", bubbles_array);
            obj.put("event", "send");

            requestBody = obj.toString();

        } catch (Exception e){
            System.out.println("## Exception : " + e);
        }
        return requestBody;
    }
    public String jsonToString(String jsonResultStr) {
        String resultText = "";
        // API 호출 결과 받은 JSON 형태 문자열에서 텍스트 추출
        // JSONParser  사용하지 않음
        JSONObject jsonObj = new JSONObject(jsonResultStr);
        JSONArray chatArray = (JSONArray) jsonObj.get("bubbles");
        if(chatArray != null) {
            JSONObject tempObj = (JSONObject) chatArray.get(0);
            JSONObject dataObj = (JSONObject) tempObj.get("data");
            if(dataObj != null) {
//                tempObj = (JSONObject) dataObj.get("description");
                resultText += (String) dataObj.get("description");
            }
        } else {
            System.out.println("없음");
        }
        return resultText;
    }
}
~~~

~~~java
@RequestMapping("/chatbotSend")
    public String chatbotSend(@RequestParam("inputText") String inputText) {
        String msg = "";
        msg = chatbotService.main(inputText);
        return msg;
    }
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>chatbotForm</title>
    <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    <script src="js/chatForm.js"></script>
  </head>
  <body>
    <!--  채팅 -->
    <h3>채팅 입력</h3>
    <form id="chatForm" enctype="multipart/form-data">
      내용 : <input type="text" id="inputText" name="inputText">
      <input type="submit" value="결과 확인">
    </form>
    <br><br>

    <!-- 결과 출력 (텍스트) -->
    <h3>응답 결과</h3>
    <div id="resultDiv"></div>
    <br><br>
  </body>
</html>
~~~

~~~js
$(function () {
    // submit 했을 때 처리
    $('#chatForm').on('submit', function (event) {
        event.preventDefault();
        var formData = new FormData($('#chatForm')[0]);
        $.ajax({
            type : "post",
            enctype : "multipart/form-data",
            url : "chatbotSend",
            data : formData,
            processData : false, // 필수
            contentType : false, // 필수
            success:function (result) {
                $('#resultDiv').text(result);
            },
            error:function (e) {
                alert("오류 발생" + e);
            }
        });
    })
})
~~~


- (3) 채팅 창 작성
  - 채팅 폼 사용
  - 웰컴 메세지 추가
    - 공통 메시지 추가
    - 답변 입력 / 답변 저장

~~~java
@Service
public class ChatbotService {
//    public static String main(String voiceMessage) {
    public String main(String voiceMessage) {
        String secretKey = "";
        String apiURL = "";

        String chatbotMessage = ""; // 응답 메세지
        try {
            //String apiURL = "https://ex9av8bv0e.apigw.ntruss.com/custom_chatbot/prod/";

            URL url = new URL(apiURL);

            String message = getReqMessage(voiceMessage);
            System.out.println("##" + message);

            String encodeBase64String = makeSignature(message, secretKey);

            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("Content-Type", "application/json;UTF-8");
            con.setRequestProperty("X-NCP-CHATBOT_SIGNATURE", encodeBase64String);

            // post request
            con.setDoOutput(true);
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            wr.write(message.getBytes("UTF-8"));
            wr.flush();
            wr.close();
            int responseCode = con.getResponseCode();

            BufferedReader br;

            if(responseCode==200) { // Normal call
                System.out.println(con.getResponseMessage());

                BufferedReader in = new BufferedReader(
                        new InputStreamReader(
                                con.getInputStream()));
                String decodedString;
                while ((decodedString = in.readLine()) != null) {
                    chatbotMessage = decodedString;
                }
                //chatbotMessage = decodedString;
                in.close();
                // 응답 메세지 출력
                System.out.println(chatbotMessage);
                chatbotMessage = jsonToString(chatbotMessage);
            } else {  // Error occurred
                chatbotMessage = con.getResponseMessage();
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return chatbotMessage;
    }

    public static String makeSignature(String message, String secretKey) {

        String encodeBase64String = "";

        try {
            byte[] secrete_key_bytes = secretKey.getBytes("UTF-8");

            SecretKeySpec signingKey = new SecretKeySpec(secrete_key_bytes, "HmacSHA256");
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(signingKey);

            byte[] rawHmac = mac.doFinal(message.getBytes("UTF-8"));
//            encodeBase64String = Base64.encodeToString(rawHmac, Base64.NO_WRAP);
            encodeBase64String = Base64.getEncoder().encodeToString(rawHmac);

            return encodeBase64String;

        } catch (Exception e){
            System.out.println(e);
        }

        return encodeBase64String;

    }

    public static String getReqMessage(String voiceMessage) {

        String requestBody = "";

        try {

            JSONObject obj = new JSONObject();

            long timestamp = new Date().getTime();

            System.out.println("##"+timestamp);

            obj.put("version", "v2");
            obj.put("userId", "U47b00b58c90f8e47428af8b7bddc1231heo2");
//=> userId is a unique code for each chat user, not a fixed value, recommend use UUID. use different id for each user could help you to split chat history for users.

            obj.put("timestamp", timestamp);

            JSONObject bubbles_obj = new JSONObject();

            bubbles_obj.put("type", "text");

            JSONObject data_obj = new JSONObject();
            data_obj.put("description", voiceMessage);

            bubbles_obj.put("type", "text");
            bubbles_obj.put("data", data_obj);

            JSONArray bubbles_array = new JSONArray();
            bubbles_array.put(bubbles_obj);

            obj.put("bubbles", bubbles_array);
//            obj.put("event", "send");

            if(Objects.equals(voiceMessage, "")) {
                obj.put("event", "open"); // 월컴 메세지
            } else {
                obj.put("event", "send");
            }
            requestBody = obj.toString();
            // 웰컴 메세지 출력


        } catch (Exception e){
            System.out.println("## Exception : " + e);
        }
        return requestBody;
    }
    public String jsonToString(String jsonResultStr) {
        String resultText = "";
        // API 호출 결과 받은 JSON 형태 문자열에서 텍스트 추출
        // JSONParser  사용하지 않음
        // images / 0 / fields / inferText 추출
        JSONObject jsonObj = new JSONObject(jsonResultStr);
        JSONArray chatArray = (JSONArray) jsonObj.get("bubbles");
        JSONObject tempObj = (JSONObject) chatArray.get(0);
        JSONObject dataObj = (JSONObject) tempObj.get("data");
//      tempObj = (JSONObject) dataObj.get("description");
        resultText += (String) dataObj.get("description");
        return resultText;
    }
}
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>chatbotForm</title>
    <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    <script src="js/chatForm2.js"></script>
    <link rel="stylesheet" type="text/css" href="css/chatbot.css">
  </head>
  <body>
    <div id="wrap">
      <!-- Header -->
      <div id="chatHeader">
        <span>챗봇</span>
        <button id="btnClose">X</button>
      </div>
    <h3>챗봇 서비스</h3>

    <!-- 응답 메시지 출력  -->
    <div id="chatBox"></div><br>

    <!-- 질문 메시지 입력 폼 -->
    <form id="chatForm">
      <input type="text" id="message" name="message" size="30" placeholder="질문을 입력하세요">
      <input type="submit" value="전송">
    </form>

    <br><br>
    <a href="/">index 페이지로 이동</a>
    </div>
  </body>
</html>
~~~

~~~js
$(function(){
    // 웰컴메시지를 받기 위해 message 입력 받기 전 빈 값으로 서버에 전송해서 웰컴메세지 받음
    callAjax();
    $('#chatForm').on('submit', function(event){
        event.preventDefault();
        if($('#message').val() == "") { // 질문을 입력하지 않고 전송 버튼 누를 때 웰컴 메세지 뜨지 않게
            alert("질문을 입력하세요");
            return false;
        }
        if($('#message').val() != ""){
            $('#chatBox').append('<div class="msgBox send"><span id="in"><span>' +
                $('#message').val() + '</span></span></div><br>');
        }
        callAjax();
        /* 입력란 비우기*/
        $('#message').val('');
    }); // submit 끝
    // 별도의 ajax 생성
    function callAjax() {
        $.ajax({
            url:"chatbotSend2",
            type:"post",
            data:{message: $('#message').val()},
            success:function(result){
                /* chatBox에 받은 메시지 추가 */
                $('#chatBox').append('<div class="msgBox receive"><span id="in"><span>챗봇</span><br><span>' +
                    result +'</span></span></div><br><br>');
                // 스크롤해서 올리기
                $("#chatBox").scrollTop($("#chatBox").prop("scrollHeight"));
            },
            error:function(){
                alert("오류가 발생했습니다.")
            }
        });
    }
});
~~~

~~~css
@charset "UTF-8";

#wrap { margin:0 auto; width: 500px; 	height: 800px; }

#chatHeader {padding: 10px 15px; border-bottom: 1px solid #95a6b4;}
#btnClose {border: none; background: none; float: right;}

#chatBox {height: 600px; width: 500px; overflow-y:scroll; padding:10px 15px; background:#9bbbd4;}

#message {width: 440px;}

#btnSubmit {float: right; background:#eeeeee; height: 28px; padding-right:0;}

.msgBox  span {padding:3px 5px; word-break:break-all; display:block;
    max-width:300px; margin-bottom: 10px; border-radius: 10px;}

.msgBox.send  span {background:#fef01b; float:right; }

.msgBox #in {width:480px; background:#9bbbd4;}
.msgBox.receive  span {background:#ffffff; float:left; }
~~~

- (4) 음성 메시지로 챗봇에 질문하기 (답변 : 텍스트)
  - 질문을 녹음해서 mp3 파일로 저장
  - mp3 파일을 텍스트로 변환 : STT 서비스 사용
  - 변환된 텍스트를 질문으로 챗봇 서버로 전송해서 답변 받아서 출력
  - ChatbotService 사용
  - STTService 사용
  - TTSService 수정

~~~java
public String clovaTextToSpeech2(String message) {
        String clientId = "";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "";//애플리케이션 클라이언트 시크릿값";
        String voiceFileName = "";
        try {
            String text = URLEncoder.encode(message, "UTF-8"); // 13자
            String apiURL = "https://naveropenapi.apigw.ntruss.com/tts-premium/v1/tts";
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setRequestMethod("POST");
            con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
            // post request
            String postParams = "speaker=nara&volume=0&speed=0&pitch=0&format=mp3&text=" + text;
            con.setDoOutput(true);
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            wr.writeBytes(postParams);
            wr.flush();
            wr.close();
            int responseCode = con.getResponseCode();
            BufferedReader br;
            if(responseCode==200) { // 정상 호출
                InputStream is = con.getInputStream();
                int read = 0;
                byte[] bytes = new byte[1024];
                // 랜덤한 이름으로 mp3 파일 생성
                String tempname = Long.valueOf(new Date().getTime()).toString();
                voiceFileName = "tts_" + tempname + ".mp3";
                File f = new File("/Users/gobyeongchae/Desktop/" + voiceFileName);
                f.createNewFile();
                OutputStream outputStream = new FileOutputStream(f);
                while ((read =is.read(bytes)) != -1) {
                    outputStream.write(bytes, 0, read);
                }
                is.close();
            } else {  // 오류 발생
                br = new BufferedReader(new InputStreamReader(con.getErrorStream()));
                String inputLine;
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return voiceFileName;
    }
~~~

~~~java
@RequestMapping("/chatbotSend3")
    public String chatbotSend3(@RequestParam("message") String inputText) {
        String msg = "";
        msg = chatbotService.main(inputText);
        return msg;
    }
    @RequestMapping("/chatbotTTS")
    public String chatbotTTS(@RequestParam("message") String message) {
        String tts = "";
        tts = ttsService.clovaTextToSpeech2(message);
        return tts;
    }
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>chatbotForm</title>
    <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    <script src="js/chatForm3.js"></script>
    <link rel="stylesheet" type="text/css" href="css/chatbot.css">
  </head>
  <body>
    <div id="wrap">
      <!-- Header -->
      <div id="chatHeader">
        <span>챗봇</span>
        <button id="btnClose">X</button>
      </div>
    <h3>챗봇 서비스</h3>

    <!-- 응답 메시지 출력  -->
    <div id="chatBox"></div><br>

      <div>
        <!-- 질문 메시지 입력 폼 -->
        <form id="chatForm">
          <input type="text" id="message" name="message" size="30" placeholder="질문을 입력하세요">
          <input type="submit" value="전송">
        </form>
      </div><br>

      <div>
      <!-- 음성 녹음 -->
      음성 메세지 : <button id="record">녹음</button>
                    <button id="stop">정지</button>
                    <div id="sound-clips"></div><br>
      </div>
      <div hidden>
        <audio preload="auto" controls></audio>
      </div>
    <br><br>
    <a href="/">index 페이지로 이동</a>
    </div>
  </body>
</html>
~~~

~~~js
$(function(){
    // 웰컴메시지를 받기 위해 message 입력 받기 전 빈 값으로 서버에 전송해서 웰컴메세지 받음
    callAjax();
    ////////////////////////////////////////////////////////
    // 음성으로 질문하기
    const record = document.getElementById("record");
    const stop = document.getElementById("stop");
    const soundClips = document.getElementById("sound-clips");

    const audioCtx = new(window.AudioContext || window.webkitAudioContext)(); // 오디오 컨텍스트 정의

    if (navigator.mediaDevices) {
        var constraints = {
            audio: true
        }
        let chunks = [];

        navigator.mediaDevices.getUserMedia(constraints)
            .then(stream => {
                const  mediaRecorder = new MediaRecorder(stream);

                record.onclick = () => {
                    mediaRecorder.start();
                    record.style.background = "red";
                    record.style.color = "black";
                }

                stop.onclick = () => {//정지 버튼 클릭 시
                    mediaRecorder.stop();//녹음 정지
                    record.style.background = "";
                    record.style.color = "";
                }

                mediaRecorder.onstop = e => {

                    const clipName = "voiceMsg";
                    //태그 3개 생성
                    const clipContainer = document.createElement('article');
                    const audio = document.createElement('audio');
                    const a = document.createElement('a');

                    clipContainer.appendChild(a);
                    soundClips.appendChild(clipContainer);

                    //chunks에 저장된 녹음 데이터를 audio 양식으로 설정
                    //audio.controls = true;
                    const blob = new Blob(chunks, {
                        'type': 'audio/mp3 codecs=opus'
                    }) ;
                    chunks = [];
                    const audioURL = URL.createObjectURL(blob);
                    // audio.src = audioURL;
                    //blob:http://localhost:8011/6377d19d-2ca8-49b1-a37f-068d602ceb60
                    a.href=audioURL;
                    a.download = clipName;
                    //a.innerHTML = "DOWN"
                    a.click(); // 다운로드 폴더에 저장하도록 클릭 이벤트 발생

                    fileUpload(blob, clipName);

                }//mediaRecorder.onstop

                //녹음 시작시킨 상태가 되면 chunks에 녹음 데이터를 저장하라
                mediaRecorder.ondataavailable = e => {
                    chunks.push(e.data)
                }

            })
            .catch(err => {
                console.log('The following error occurred: ' + err)
            })
    }
    // 서버에 업로드
    function fileUpload(blob, clipName){

        var formData = new FormData();
        formData.append('uploadFile', blob, clipName+".mp3");

        //녹음된 mp3파일 전송하고 반환된 텍스트(result)를 챗봇 서버에 전달
        $.ajax({
            type:"post",
            enctype: 'multipart/form-data',
            url: "stt", //통신할 url
            data: formData, //전송할 데이타	: 파일명 :voiceMsg.mp3
            processData: false,
            contentType: false,
            success: function(result) {
                $('#chatBox').append('<div class="msgBox send"><span id="in"><span>' +
                    result + '</span></span></div><br>');
                // 챗봇에게 전달
                $('#message').val(result);
                callAjax();
                $('#message').val('');
            },
            error: function(e) {
                alert("에러가 발생했습니다 : " + e);
            }
        });
    }
    ////////////////////////////////////////////////////////
    // 질문하고 음답 받기(텍스트)
    $('#chatForm').on('submit', function(event){
        event.preventDefault();
        if($('#message').val() == "") { // 질문을 입력하지 않고 전송 버튼 누를 때 웰컴 메세지 뜨지 않게
            alert("질문을 입력하세요");
            return false;
        }
        if($('#message').val() != ""){
            $('#chatBox').append('<div class="msgBox send"><span id="in"><span>' +
                $('#message').val() + '</span></span></div><br>');
        }
        callAjax();
        /* 입력란 비우기*/
        $('#message').val('');
    }); // submit 끝
    // 별도의 ajax 생성
    function callAjax() {
        $.ajax({
            url:"chatbotSend3",
            type:"post",
            data:{message: $('#message').val()},
            success:function(result){
                /* chatBox에 받은 메시지 추가 */
                $('#chatBox').append('<div class="msgBox receive"><span id="in"><span>챗봇</span><br><span>' +
                    result +'</span></span></div><br><br>');
                // 스크롤해서 올리기
                $("#chatBox").scrollTop($("#chatBox").prop("scrollHeight"));
                callAjaxTTS(result);
            },
            error:function(){
                alert("오류가 발생했습니다.")
            }
        });
    }
    function callAjaxTTS(result){
        $.ajax({
            type:"post",
            url:"chatbotTTS",
            data:{message : result},
            dataType :'text',
            success:function (result){ //음성 파일 이름 받음
                /* chatBox에 받은 음성 메시지 플레이 */
                $('audio').prop("src", '/images/'+ result)[0].play();
                $('audio').hide();
            },
            error:function(data){
                alert("에러 발생");
            }
        });
    }
});
~~~