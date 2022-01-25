## Object Detection (객체 탐지)
- 이미지 내 사람, 동물, 사물 등 객체의 타입과 위치를 감지하여 정보를 제공하는 API 서비스
- 탐지된 객체명, 객체의 수, 바운딩 박스용 좌표, 객체별 확률값
- ObjectDetectionService 클래스 생성
  - objectDetectService() 메소드 추가
- (1) 콘솔에 결과 출력

~~~java
@Service
public class ObjectDetectionService {
    public void objectDetect() {
        StringBuffer reqStr = new StringBuffer();
        String clientId = "";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "";//애플리케이션 클라이언트 시크릿값";

        try {
            String paramName = "image"; // 파라미터명은 image로 지정
            String imgFile = "/Users/gobyeongchae/Desktop/images/animal1.jpg";
            File uploadFile = new File(imgFile);
            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision-obj/v1/detect"; // 객체 인식
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setUseCaches(false);
            con.setDoOutput(true);
            con.setDoInput(true);
            // multipart request
            String boundary = "---" + System.currentTimeMillis() + "---";
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
            con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
            OutputStream outputStream = con.getOutputStream();
            PrintWriter writer = new PrintWriter(new OutputStreamWriter(outputStream, "UTF-8"), true);
            String LINE_FEED = "\r\n";
            // file 추가
            String fileName = uploadFile.getName();
            writer.append("--" + boundary).append(LINE_FEED);
            writer.append("Content-Disposition: form-data; name=\"" + paramName + "\"; filename=\"" + fileName + "\"").append(LINE_FEED);
            writer.append("Content-Type: "  + URLConnection.guessContentTypeFromName(fileName)).append(LINE_FEED);
            writer.append(LINE_FEED);
            writer.flush();
            FileInputStream inputStream = new FileInputStream(uploadFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            writer.append(LINE_FEED).flush();
            writer.append("--" + boundary + "--").append(LINE_FEED);
            writer.close();
            BufferedReader br = null;
            int responseCode = con.getResponseCode();
            if(responseCode==200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            } else {  // 오류 발생
                System.out.println("error!!!!!!! responseCode= " + responseCode);
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
~~~

~~~java
@RequestMapping("/objDetect")
	public void objDetect() {
		objectDetectionService.objectDetect();
	}
~~~

- (2) JSON 형태에서 결과에서 이름, 박스 좌표 추출해서 반환
  - ObjectVO 생성
  - jsonToVoList() 메소드 추가
  - 파일 업로드 기능
  - @RestController 사용

~~~java
// 포즈 인식
    @RequestMapping("/objDetect")
    public ArrayList<ObjectVO>  objectDetect(@RequestParam("uploadFile") MultipartFile file) {
        ArrayList<ObjectVO>objectList = null;
        try {
            // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치 (프로젝트 외부에 저장)
            String uploadPath = "/Users/gobyeongchae/Desktop/productImages";
            // 2. 원본 파일 이름 알아오기
            String originalFileName = file.getOriginalFilename();
            String filePathName = uploadPath + originalFileName;
            // 3. 파일 생성
            File file1 = new File(filePathName);
            // 4. 서버로 전송
            file.transferTo(file1);
            // 서비스에 파일 path와 파일명 전달  -> 서비스 메소드에서 변경
            // 서비스에서 반환된 PoseVO 리스트 저장
            objectList = objectDetectionService.objectDetect(filePathName);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return objectList;
    }
~~~

~~~java
@Service
public class ObjectDetectionService {
    public  ArrayList<ObjectVO> objectDetect(String filePathName) {
        StringBuffer reqStr = new StringBuffer();
        String clientId = "";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "";//애플리케이션 클라이언트 시크릿값";

        ArrayList<ObjectVO> objectList = new ArrayList<ObjectVO>();

        try {
            String paramName = "image"; // 파라미터명은 image로 지정
            String imgFile = filePathName;
            File uploadFile = new File(imgFile);
            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision-obj/v1/detect"; // 객체 인식
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setUseCaches(false);
            con.setDoOutput(true);
            con.setDoInput(true);
            // multipart request
            String boundary = "---" + System.currentTimeMillis() + "---";
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
            con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
            OutputStream outputStream = con.getOutputStream();
            PrintWriter writer = new PrintWriter(new OutputStreamWriter(outputStream, "UTF-8"), true);
            String LINE_FEED = "\r\n";
            // file 추가
            String fileName = uploadFile.getName();
            writer.append("--" + boundary).append(LINE_FEED);
            writer.append("Content-Disposition: form-data; name=\"" + paramName + "\"; filename=\"" + fileName + "\"").append(LINE_FEED);
            writer.append("Content-Type: "  + URLConnection.guessContentTypeFromName(fileName)).append(LINE_FEED);
            writer.append(LINE_FEED);
            writer.flush();
            FileInputStream inputStream = new FileInputStream(uploadFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            writer.append(LINE_FEED).flush();
            writer.append("--" + boundary + "--").append(LINE_FEED);
            writer.close();
            BufferedReader br = null;
            int responseCode = con.getResponseCode();
            if(responseCode==200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            } else {  // 오류 발생
                System.out.println("error!!!!!!! responseCode= " + responseCode);
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
                objectList = jsonToVoList(response.toString());
            }
			/*   else {
			    System.out.println("error !!!");
			}*/
        } catch (Exception e) {
            System.out.println(e);
        }
        return objectList;
    }
    // API 서버로부터 받은 JSON 형태의 테이블부터 names와 x1, x2, y1, y2 추출 후 VO 리스트 만들어 반환
    public ArrayList<ObjectVO> jsonToVoList(String jsonResultStr){
        ArrayList<ObjectVO> objectList = new ArrayList<ObjectVO>();

        try {
            // JSON 형태의 문자열에서 JSON 오브젝트 "predictions" 추출해서 JSONArray에 저장
            JSONParser jsonParser = new JSONParser();
            JSONObject jsonObj = (JSONObject) jsonParser.parse(jsonResultStr);
            JSONArray objArray = (JSONArray) jsonObj.get("predictions");
            JSONObject obj0 = (JSONObject) objArray.get(0);

            JSONArray nameArray = (JSONArray) obj0.get("detection_names");
            JSONArray boxArray = (JSONArray) obj0.get("detection_boxes");

            for(int i=0; i<nameArray.size(); i++) {
                // name 추출
                String name = (String) nameArray.get(i);

                //x1, y1, x2, y2 추출
                JSONArray box = (JSONArray) boxArray.get(i);
                double x1 =(double) box.get(0);
                double y1 =(double) box.get(1);
                double x2 =(double) box.get(2);
                double y2 =(double) box.get(3);

                // VO에 저장
                ObjectVO vo = new ObjectVO();
                vo.setName(name);
                vo.setX1(x1);
                vo.setY1(y1);
                vo.setX2(x2);
                vo.setY2(y2);

                //리스트에 추가
                objectList.add(vo);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        return objectList;
    }
}
~~~

~~~jsp
<html>
	<head>
		<meta charset="UTF-8">
		<title>Object Detect</title>
		<script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
		<script src="js/objDetect.js"></script>
	</head>
	<body>
		<!--  파일 업로드 -->
		<h3>포즈 인식</h3>
		<form id="objectForm" enctype="multipart/form-data">
			파일 : <input type="file" id="uploadFile" name="uploadFile">
			<input type="submit" value="결과 확인">
		</form>
		<br><br>
		<!-- 결과 출력  -->
		<h3>포즈 인식 결과를 이미지에 좌표로 표시</h3>
		<canvas id="objectCanvas" width="600" height="600"></canvas>
		<br><br>
		<!-- 객체와 좌표 값 출력 -->
		<div id="resultDiv"></div>
		<br><br>
		<a href="/">index 페이지로 이동</a>
	</body>
</html>
~~~

~~~js
$(function () {
    $('#objectForm').on('submit', function(event){
        event.preventDefault();
        var formData = new FormData($('#objectForm')[0]);

        // 업로드된 파일명 알아오기
        var fileName = $('#uploadFile').val().split("\\").pop();
        //alert(fileName);

        $.ajax({
            url:"objDetect",
            enctype:'multipart/form-data',
            type:"post",
            data:formData,
            processData: false,  // 필수
            contentType: false,  // 필스
            success:function(result){
                drawCanvas(result, fileName);
            },
            error:function(e){
                alert("오류가 발생했습니다." + e)
            }
        });

        function drawCanvas(result, fileName){
            //mycanvas 캔버스 태그 객체로 생성
            var canvas = document.getElementById("objectCanvas");
            var context = canvas.getContext("2d");

            var objectImage = new Image();
            objectImage.src ="/objimages/" + fileName;
            objectImage.width = canvas.width;
            objectImage.height = canvas.height;

            objectImage.onload = function(){
                context.drawImage(objectImage,0, 0, objectImage.width, objectImage.height );
                var values = "";
                $.each(result, function(){
                    // 사각형 좌표
                    var x1 = this.x1 * objectImage.width;
                    var y1 = this.y1 * objectImage.height;
                    var x2 = this.x2 * objectImage.width;
                    var y2 = this.y2 * objectImage.height;

                    context.font = '15px batang';
                    context.fillStyle = "rgb(255, 0, 255)";

                    context.strokeStyle = "red";//선색상
                    context.lineWidth = 2; // 선 굵기

                    context.fillText(this.name, y1, x1);
                    context.strokeRect(y1, x1, y2-y1, x2-x1);
                    values += this.name + "(" + this.x1 + ", " + this.y1 + ", " + this.x2 + ", " + this.y2 + ") <br>";
                });
                $('#resultDiv').html(values);
            };
        }	// function 끝
    });
});
~~~

## CLOVA Speech Recognition (CSR) : 음성 인식
- 음성 인식 API 서비스
- 사람의 목소리를 텍스트로 변환 
- 음성을 텍스트로 변환 : STT(Speech-To-Text)
- 음성 파일을 입력 받아서 변환된 텍스트로 반환
- 언어 선택 가능
- (1) 결과를 콘솔에 출력
  - STTService 클래스 생성
  - clovaSpeechToText() 메소드 추가
  - 콘솔 창에 텍스트 출력

~~~java
@Service
public class STTService {
    public void clovaSpeechToText() {
        String clientId = "";             // Application Client ID";
        String clientSecret = "";     // Application Client Secret";

        try {
            String imgFile = "/Users/gobyeongchae/Desktop/voice/kor1.mp3";
            File voiceFile = new File(imgFile);

            String language = "Kor";        // 언어 코드 ( Kor, Jpn, Eng, Chn )
            String apiURL = "https://naveropenapi.apigw.ntruss.com/recog/v1/stt?lang=" + language;
            URL url = new URL(apiURL);

            HttpURLConnection conn = (HttpURLConnection)url.openConnection();
            conn.setUseCaches(false);
            conn.setDoOutput(true);
            conn.setDoInput(true);
            conn.setRequestProperty("Content-Type", "application/octet-stream");
            conn.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            conn.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);

            OutputStream outputStream = conn.getOutputStream();
            FileInputStream inputStream = new FileInputStream(voiceFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            BufferedReader br = null;
            int responseCode = conn.getResponseCode();
            if(responseCode == 200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            } else {  // 오류 발생
                System.out.println("error!!!!!!! responseCode= " + responseCode);
                br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
~~~

~~~java
@RequestMapping("/sttService")
	public void sttService() {
		sttService.clovaSpeechToText();
	}
~~~

- (2) 파일 업로드 / 추출된 텍스트 출력
  - sttView.jsp
  - stt.js
  - APIRestController에 추가
  - <audio> play
  - 추출된 텍스트를 파일로 저장
    - resultToFileSave() 메소드 추가

~~~java
@RequestMapping("/stt")
    public String sttService(@RequestParam("uploadFile") MultipartFile file) {
        String stt = "";
        try {
            // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치 (프로젝트 외부에 저장)
            String uploadPath = "/Users/gobyeongchae/Desktop/productImages";
            // 2. 원본 파일 이름 알아오기
            String originalFileName = file.getOriginalFilename();
            String filePathName = uploadPath + originalFileName;
            // 3. 파일 생성
            File file1 = new File(filePathName);
            // 4. 서버로 전송
            file.transferTo(file1);
            // 서비스에 파일 path와 파일명 전달  -> 서비스 메소드에서 변경
            // 서비스에서 반환된 PoseVO 리스트 저장
            stt = sttService.clovaSpeechToText(filePathName);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return stt;
    }
~~~

~~~java
@Service
public class STTService {
    public String clovaSpeechToText(String filePathName) {
        String clientId = "";             // Application Client ID";
        String clientSecret = "";     // Application Client Secret";
        String resultText = "";
        try {
            String imgFile = filePathName;
            File voiceFile = new File(imgFile);

            String language = "Kor";        // 언어 코드 ( Kor, Jpn, Eng, Chn )
            String apiURL = "https://naveropenapi.apigw.ntruss.com/recog/v1/stt?lang=" + language;
            URL url = new URL(apiURL);

            HttpURLConnection conn = (HttpURLConnection)url.openConnection();
            conn.setUseCaches(false);
            conn.setDoOutput(true);
            conn.setDoInput(true);
            conn.setRequestProperty("Content-Type", "application/octet-stream");
            conn.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            conn.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);

            OutputStream outputStream = conn.getOutputStream();
            FileInputStream inputStream = new FileInputStream(voiceFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            BufferedReader br = null;
            int responseCode = conn.getResponseCode();
            if(responseCode == 200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            } else {  // 오류 발생
                System.out.println("error!!!!!!! responseCode= " + responseCode);
                br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
                resultText = jsonToString(response.toString());
                resultToFileSave(resultText); // 파일로 저장
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return resultText;
    }

    public String jsonToString(String jsonResultStr) {
        String resultText = "";
        try {
            JSONObject jsonObject = new JSONObject(jsonResultStr);
            resultText = (String)jsonObject.get("text");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return resultText;
    }
    // 음성 파일에서 추출한 텍스트 파일로 저장
    public void resultToFileSave(String result) {
        try {
            String fileName = Long.valueOf(new Date().getTime()).toString();
            String filePathName = "/Users/gobyeongchae/Desktop/voice/" + "stt_" + fileName + ".txt";

            FileWriter fw = new FileWriter(filePathName);
            fw.write(result);
            fw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
~~~

~~~jsp
<html>
  <head>
      <title>STT Form</title>
  </head>
  <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
  <script src="js/stt.js"></script>
  <body>
      <!--  파일 업로드 -->
      <h3>음석 인식</h3>
      <form id="sttForm" enctype="multipart/form-data">
          파일 : <input type="file" id="uploadFile" name="uploadFile">
          <input type="submit" value="결과 확인">
      </form>
      <br><br>
      <!-- 객체와 좌표 값 출력 -->
      STT 결과 : <div id="resultDiv"></div>
      <br><br>
      <div><audio preload="auto" controls></audio></div>
      <a href="/">index 페이지로 이동</a>
  </body>
</html>
~~~

~~~js
$(function () {
    // submit 했을 때 처리
    $('#sttForm').on('submit', function (event) {
        event.preventDefault();
        var formData = new FormData($('#sttForm')[0]);
        var fileName = $('#uploadFile').val().split("\\").pop();
        $('audio').prop("src", '/voice/' + fileName);
        $.ajax({
            type : "post",
            enctype : "multipart/form-data",
            url : "stt",
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

- (3) 언어 선택 \<select name=”language”> 추가
  - sst2.jsp
  - sst2.js

~~~java
// 언어 선택
    @RequestMapping("/stt2")
    public String sttService2(@RequestParam("uploadFile") MultipartFile file, @RequestParam("language") String language) {
        String stt = "";
        try {
            // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치 (프로젝트 외부에 저장)
            String uploadPath = "/Users/gobyeongchae/Desktop/productImages";
            // 2. 원본 파일 이름 알아오기
            String originalFileName = file.getOriginalFilename();
            String filePathName = uploadPath + originalFileName;
            // 3. 파일 생성
            File file1 = new File(filePathName);
            // 4. 서버로 전송
            file.transferTo(file1);
            // 서비스에 파일 path와 파일명 전달  -> 서비스 메소드에서 변경
            // 서비스에서 반환된 PoseVO 리스트 저장
            stt = sttService2.clovaSpeechToText(filePathName, language);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return stt;
    }
~~~

~~~java
@Service
public class STTService2 {
    public String clovaSpeechToText(String filePathName, String language) {
        String clientId = "";             // Application Client ID";
        String clientSecret = "";     // Application Client Secret";
        String resultText = "";
        try {
            String imgFile = filePathName;
            File voiceFile = new File(imgFile);

            //String language = SelLanguage;        // 언어 코드 ( Kor, Jpn, Eng, Chn )
            String apiURL = "https://naveropenapi.apigw.ntruss.com/recog/v1/stt?lang=" + language;
            URL url = new URL(apiURL);

            HttpURLConnection conn = (HttpURLConnection)url.openConnection();
            conn.setUseCaches(false);
            conn.setDoOutput(true);
            conn.setDoInput(true);
            conn.setRequestProperty("Content-Type", "application/octet-stream");
            conn.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
            conn.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);

            OutputStream outputStream = conn.getOutputStream();
            FileInputStream inputStream = new FileInputStream(voiceFile);
            byte[] buffer = new byte[4096];
            int bytesRead = -1;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            outputStream.flush();
            inputStream.close();
            BufferedReader br = null;
            int responseCode = conn.getResponseCode();
            if(responseCode == 200) { // 정상 호출
                br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            } else {  // 오류 발생
                System.out.println("error!!!!!!! responseCode= " + responseCode);
                br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            }
            String inputLine;
            if(br != null) {
                StringBuffer response = new StringBuffer();
                while ((inputLine = br.readLine()) != null) {
                    response.append(inputLine);
                }
                br.close();
                System.out.println(response.toString());
                resultText = jsonToString(response.toString());
                resultToFileSave(resultText); // 파일로 저장
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return resultText;
    }

    public String jsonToString(String jsonResultStr) {
        String resultText = "";
        try {
            JSONObject jsonObject = new JSONObject(jsonResultStr);
            resultText = (String)jsonObject.get("text");
        } catch (Exception e) {
            e.printStackTrace();
        }
        return resultText;
    }
    // 음성 파일에서 추출한 텍스트 파일로 저장
    public void resultToFileSave(String result) {
        try {
            String fileName = Long.valueOf(new Date().getTime()).toString();
            String filePathName = "/Users/gobyeongchae/Desktop/voice/" + "stt2_" + fileName + ".txt";

            FileWriter fw = new FileWriter(filePathName);
            fw.write(result);
            fw.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
~~~

~~~jsp
<html>
  <head>
      <title>STT Service2</title>
    <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    <script src="js/stt2.js"></script>
  </head>
  <body>
    <!--  파일 업로드 -->
    <h3>음석 인식</h3>
    <form id="sttForm" enctype="multipart/form-data">
      파일 : <input type="file" id="uploadFile" name="uploadFile">
      <br>
      언어 선택 :
      <select name="language" id="language">
        <option value="">언어 선택</option>
        <option value="Kor">한국어</option>
        <option value="Jpn">일본어</option>
        <option value="Eng">영어</option>
        <option value="Chn">중국어</option>
      </select>
      <input type="submit" value="결과 확인">
    </form>
    <br><br>
    <!-- 객체와 좌표 값 출력 -->
    STT 결과 : <div id="resultDiv"></div>
    <br><br>
    <div><audio preload="auto" controls></audio></div>

    <a href="/">index 페이지로 이동</a>
  </body>
</html>
~~~

~~~js
$(function () {
    // submit 했을 때 처리
    $('#sttForm').on('submit', function (event) {
        event.preventDefault();
        var formData = new FormData($('#sttForm')[0]);
        var fileName = $('#uploadFile').val().split("\\").pop();
        $('audio').prop("src", '/voice/' + fileName);
        $.ajax({
            type : "post",
            enctype : "multipart/form-data",
            url : "stt2",
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

## CLOVA Voice - Premium (TTS)
- 음성 합성 API 서비스
- 텍스트를 음성으로 변환 : TTS(Text-To-Speech)
- 텍스트 파일을 입력 받아서 변환된 음성 파일(mp3/wav) 반환
- 언어, 음색 선택 가능

- (1) 반환된 데이터를 mp3 파일로 저장

~~~java
@Service
public class TTSService {
   public void clovaTextToSpeech() {
       String clientId = "";//애플리케이션 클라이언트 아이디값";
       String clientSecret = "";//애플리케이션 클라이언트 시크릿값";
       try {
           String text = URLEncoder.encode("Hello, nice to meet you", "UTF-8"); // 13자
           String apiURL = "https://naveropenapi.apigw.ntruss.com/tts-premium/v1/tts";
           URL url = new URL(apiURL);
           HttpURLConnection con = (HttpURLConnection)url.openConnection();
           con.setRequestMethod("POST");
           con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
           con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
           // post request
           String postParams = "speaker=clara&volume=0&speed=0&pitch=0&format=mp3&text=" + text;
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
               File f = new File("/Users/gobyeongchae/Desktop/" + tempname + ".mp3");
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
   }
}
~~~

~~~java
@RequestMapping("clovaTTS")
	public void ttsService() {
		ttsService.clovaTextToSpeech();
	}
~~~

- (2)  파일 업로드 / 결과 mp3파일 <audio> 플레이
  - <select> 태그 사용 : 언어 음색 선택

~~~java
@RequestMapping("/clovaTTS")
    public String clovaTTS(@RequestParam("uploadFile") MultipartFile file,
                            @RequestParam("country") String country) {
        String tts = "";
        try {
            // 1. 파일 저장 경로 설정 : 실제 서비스되는 위치 (프로젝트 외부에 저장)
            String uploadPath = "/Users/gobyeongchae/Desktop/productImages";
            // 2. 원본 파일 이름 알아오기
            String originalFileName = file.getOriginalFilename();
            String filePathName = uploadPath + originalFileName;
            // 3. 파일 생성
            File file1 = new File(filePathName);
            // 4. 서버로 전송
            file.transferTo(file1);
            // 서비스에 파일 path와 파일명 전달  -> 서비스 메소드에서 변경
            // 서비스에서 반환된 파일명 받아오기
            tts = ttsService.clovaTextToSpeech(filePathName, country);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return tts;
    }
~~~

~~~java
@Service
public class TTSService { // 파일 경로 및 언어 전달 받아서, 저장된 파일명 반환
   public String clovaTextToSpeech(String filePathName, String country) {
       String clientId = "";//애플리케이션 클라이언트 아이디값";
       String clientSecret = "";//애플리케이션 클라이언트 시크릿값";
       String voiceFileName = "";
       try {
           // 전달 받은 파일에서 텍스트를 추출하는 함수
           String fileContents = fileRead(filePathName);
           String text = URLEncoder.encode(fileContents, "UTF-8"); // 13자
           String apiURL = "https://naveropenapi.apigw.ntruss.com/tts-premium/v1/tts";
           URL url = new URL(apiURL);
           HttpURLConnection con = (HttpURLConnection)url.openConnection();
           con.setRequestMethod("POST");
           con.setRequestProperty("X-NCP-APIGW-API-KEY-ID", clientId);
           con.setRequestProperty("X-NCP-APIGW-API-KEY", clientSecret);
           // post request
           String postParams = "speaker=" + country + "&volume=0&speed=0&pitch=0&format=mp3&text=" + text;
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
   // 파일 경로 전달받아 파일 내용 읽어서 텍스트 반환
    public String fileRead(String filePathName) {
       String result = "";
        try {
            File file = new File(filePathName);
            FileReader fr = new FileReader(file);
            BufferedReader br = new BufferedReader(fr);
            String line = "";
            while ((line = br.readLine()) != null) {
                result += line;
            }
            br.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println(result);
        return result;
    }
}
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
      <title>STT Service2</title>
    <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    <script src="js/tts.js"></script>
  </head>
  <body>
    <!--  파일 업로드 -->
    <h3>음석 인식</h3>
    <form id="ttsForm" enctype="multipart/form-data">
      파일 : <input type="file" id="uploadFile" name="uploadFile">
      <br>
      <br>
      언어 선택 :
      <select name="country" id="country">
        <option value="nara" selected>한국어, 여성</option>
        <option value="jinho">한국어, 남성</option>
        <option value="nhajun">한국어, 아동(남)</option>
        <option value="ndain">한국어, 아동(여)</option>
        <option value="shinji">일본어, 남성</option>
        <option value="matt">영어, 남성</option>
        <option value="clara">영어, 여성</option>
        <option value="carmen">스페인어, 여성</option>
        <option value="meimei">중국어, 여성</option>
      </select>
      <input type="submit" value="결과 확인">
    </form>
    <br><br>
    <!-- 객체와 좌표 값 출력 -->
    TTS 결과 : <div id="resultDiv"></div>
    <br><br>
    <div><audio preload="auto" controls></audio></div>

    <a href="/">index 페이지로 이동</a>
  </body>
</html>
~~~

~~~js
$(function () {
    // submit 했을 때 처리
    $('#ttsForm').on('submit', function (event) {
        event.preventDefault();
        var formData = new FormData($('#ttsForm')[0]);
        var fileName = $('#uploadFile').val().split("\\").pop();

        $.ajax({
            type : "post",
            enctype : "multipart/form-data",
            url : "clovaTTS",
            data : formData,
            processData : false, // 필수
            contentType : false, // 필수
            success:function (result) {
                $('audio').prop("src", '/images/' + result);
                $('#resultDiv').text(result); // 저장된 음성 파일명
            },
            error:function (e) {
                alert("오류 발생" + e);
            }
        });
    })
})
~~~