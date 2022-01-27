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
- (5) Json 형식 자바스크립트에서 파싱, 링크, 멀티링크, 이미지 안내 구현
  - jsp는 그대로 사용

~~~java
public String chatbotArtineer(String voiceMessage) {
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
//                chatbotMessage = jsonToString(chatbotMessage);
//                서비스에서 JSON 파싱하지 않고 자바스크립트로 전송하여 자바스크립트에서 파싱
            } else {  // Error occurred
                chatbotMessage = con.getResponseMessage();
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return chatbotMessage;
    }
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
            type:"post",
            url:"chatbotArtineer",
            data:{message : $('#message').val()},
            dataType :'json',
            success:function (result){
                //JSON 형식 그대로 반환 받음
                var bubbles = result.bubbles;
                for(var b in bubbles){
                    if(bubbles[b].type == 'text'){ // 기본 답변인 경우
                        /* chatBox에 받은 메시지 추가 */
                        $('#chatBox').append('<div class="msgBox receive"><span id="in"><span>챗봇</span><br><span>' +
                            bubbles[b].data.description +'</span></span></div><br><br>');

                        // 챗봇으로 부터 받은 텍스트 답변을 음성으로 변환하기 위해 TTS 호출
                        callAjaxTTS(bubbles[b].data.description);
                    }	else if(bubbles[b].type == 'template'){//이미지 답변 또는 멀티링크 답변 시작
                        if(bubbles[b].data.cover.type=="image"){//이미지 이면
                            $("#chatBox").append("<img src='" + bubbles[b].data.cover.data.imageUrl +
                                "' alt='이미지 없음'>");
                            if(bubbles[b].data.contentTable == null){
                                $("#chatBox").append
                                ("<a href='"+bubbles[b].data.cover.data.action.data.url+"' target='_blank'>" +
                                    bubbles[b].data.cover.data.action.data.url+ "</a><br>");
                            } else {
                                $("#chatBox").append("<div class=\"msgBox receive\"><span id=\"in\"><span>챗봇</span><br><span>" + bubbles[b].data.cover.data.description+ "</p>");
                                // 챗봇으로 부터 받은 텍스트 답변을 음성으로 변환하기 위해 TTS 호출
                                callAjaxTTS(bubbles[b].data.cover.data.description);
                            }
                        } 	else if(bubbles[b].data.cover.type=="text"){//멀티링크 답변이면
                            $("#chatBox").append("<div class=\"msgBox receive\"><span id=\"in\"><span>챗봇</span><br><span>" + bubbles[b].data.cover.data.description+ "</p>");
                            // 챗봇으로 부터 받은 텍스트 답변을 음성으로 변환하기 위해 TTS 호출
                            callAjaxTTS(bubbles[b].data.cover.data.description);
                        }

                        // 이미지 / 멀티링크 답변 공통 (contentTable 포함)
                        for(var ct in bubbles[b].data.contentTable){
                            var ct_data = bubbles[ct].data.contentTable[ct];
                            for(var ct_d in ct_data){
                                $("#chatBox").append
                                ("<a href='"+ct_data[ct_d].data.data.action.data.url+"' target='_blank'>" +
                                    ct_data[ct_d].data.data.action.data.url+ "</a><br>");
                            }
                        }// contentTable for문 끝
                    }//template 끝
                }//bubbles for문 종료

                // 스크롤해서 올리기
                $("#chatBox").scrollTop($("#chatBox").prop("scrollHeight"));

            },
            error:function(data){
                alert("오류가 발생했습니다.");
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