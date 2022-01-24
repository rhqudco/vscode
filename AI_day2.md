## CLOVA OCR (Optical Character Recognition)
- 광학 문자 인식 API 서비스
- 사진 속에서 텍스트 정보를 찾고 의미를 판별하는 기술
- 언어와 이미지 데이터를 입력 받아서, 그에 맞는 인식 결과를 텍스트로 반환
- 결과를 콘솔에 출력
  - 텍스트가 포함된 이미지 파일을 전송하고
  - JSON 형태의 결과 받아서 콘솔에 출력
  - OCRService 클래스 생성
    - clovaOCRService() 메소드 추가 : 결과 콘솔에 출력
    - jsonToString() 메소드 추가 : 결과로 추출된 텍스트 반환

~~~java
@Service
public class OCRService {
    public void clovaOCRService() {
        String apiURL = "";
        String secretKey = "";
        String imageFile = "/Users/gobyeongchae/Desktop/ocr1.PNG";
        String result = "";

        try {
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setUseCaches(false);
            con.setDoInput(true);
            con.setDoOutput(true);
            con.setReadTimeout(30000);
            con.setRequestMethod("POST");
            String boundary = "----" + UUID.randomUUID().toString().replaceAll("-", "");
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
            con.setRequestProperty("X-OCR-SECRET", secretKey);

            JSONObject json = new JSONObject();
            json.put("version", "V2");
            json.put("requestId", UUID.randomUUID().toString());
            json.put("timestamp", System.currentTimeMillis());
            JSONObject image = new JSONObject();
            image.put("format", "jpg");
            image.put("name", "demo");
            JSONArray images = new JSONArray();
            images.put(image);
            json.put("images", images);
            String postParams = json.toString();

            con.connect();
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            long start = System.currentTimeMillis();
            File file = new File(imageFile);
            writeMultiPart(wr, postParams, file, boundary);
            wr.close();

            int responseCode = con.getResponseCode();
            BufferedReader br;
            if (responseCode == 200) {
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            } else {
                br = new BufferedReader(new InputStreamReader(con.getErrorStream()));
            }
            String inputLine;
            StringBuffer response = new StringBuffer();
            while ((inputLine = br.readLine()) != null) {
                response.append(inputLine);
            }
            br.close();

            System.out.println(response);
            result = jsonToString(response.toString());
            System.out.println(result);
        } catch (Exception e) {
            System.out.println(e);
        }
    }
    private static void writeMultiPart(OutputStream out, String jsonMessage, File file, String boundary) throws
            IOException {
        StringBuilder sb = new StringBuilder();
        sb.append("--").append(boundary).append("\r\n");
        sb.append("Content-Disposition:form-data; name=\"message\"\r\n\r\n");
        sb.append(jsonMessage);
        sb.append("\r\n");

        out.write(sb.toString().getBytes("UTF-8"));
        out.flush();

        if (file != null && file.isFile()) {
            out.write(("--" + boundary + "\r\n").getBytes("UTF-8"));
            StringBuilder fileString = new StringBuilder();
            fileString
                    .append("Content-Disposition:form-data; name=\"file\"; filename=");
            fileString.append("\"" + file.getName() + "\"\r\n");
            fileString.append("Content-Type: application/octet-stream\r\n\r\n");
            out.write(fileString.toString().getBytes("UTF-8"));
            out.flush();

            try (FileInputStream fis = new FileInputStream(file)) {
                byte[] buffer = new byte[8192];
                int count;
                while ((count = fis.read(buffer)) != -1) {
                    out.write(buffer, 0, count);
                }
                out.write("\r\n".getBytes());
            }

            out.write(("--" + boundary + "--\r\n").getBytes("UTF-8"));
        }
        out.flush();
    }
    public String jsonToString(String jsonResultStr) {
        String resultText = "";
        // API 호출 결과 받은 JSON 형태 문자열에서 텍스트 추출
        // JSONParser  사용하지 않음
        // images / 0 / fields / inferText 추출
        JSONObject jsonObj = new JSONObject(jsonResultStr);
        JSONArray imageArray = (JSONArray) jsonObj.get("images");
        if(imageArray != null) {
            JSONObject tempObj = (JSONObject) imageArray.get(0);
            JSONArray fieldArray = (JSONArray) tempObj.get("fields");
            if(fieldArray != null) {
                for(int i=0; i<fieldArray.length(); i++) {
                    tempObj = (JSONObject) fieldArray.get(i);
                    resultText += (String) tempObj.get("inferText") + " ";
                }
            }
        } else {
            System.out.println("없음");
        }
        return resultText;
    }
}
~~~

~~~java
	// ocr 페이지 호출
	@RequestMapping("/clovaOCR")
	public void clovaOCR() {
		ocrService.clovaOCRService();
	}
~~~

- 서비스에서 결과 반환하고 컨트롤러에서 뷰 페이지로 출력
  - REST API 방법 : @RestController 사용
  - 파일 업로드
  - Ajax 사용해서 서버로 전달하고 결과 받아서 현재 페이지에 출력
  - APIRestController 클래스 추가 : @RestController
    - 서비스 클래스의 메소드 호출하고 결과 받아서 반환
  - ocr.js
    - Ajax 사용해서 파일 전송하고 결과 받아서 현재 페이지에 출력

~~~java
@Service
public class OCRService {
    public String clovaOCRService(String filePathName) {
        String apiURL = "";
        String secretKey = "";
        String imageFile = filePathName;
        String result = "";
        try {
            URL url = new URL(apiURL);
            HttpURLConnection con = (HttpURLConnection)url.openConnection();
            con.setUseCaches(false);
            con.setDoInput(true);
            con.setDoOutput(true);
            con.setReadTimeout(30000);
            con.setRequestMethod("POST");
            String boundary = "----" + UUID.randomUUID().toString().replaceAll("-", "");
            con.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
            con.setRequestProperty("X-OCR-SECRET", secretKey);
            JSONObject json = new JSONObject();
            json.put("version", "V2");
            json.put("requestId", UUID.randomUUID().toString());
            json.put("timestamp", System.currentTimeMillis());
            JSONObject image = new JSONObject();
            image.put("format", "jpg");
            image.put("name", "demo");
            JSONArray images = new JSONArray();
            images.put(image);
            json.put("images", images);
            String postParams = json.toString();
            con.connect();
            DataOutputStream wr = new DataOutputStream(con.getOutputStream());
            long start = System.currentTimeMillis();
            File file = new File(imageFile);
            writeMultiPart(wr, postParams, file, boundary);
            wr.close();
            int responseCode = con.getResponseCode();
            BufferedReader br;
            if (responseCode == 200) {
                br = new BufferedReader(new InputStreamReader(con.getInputStream()));
            } else {
                br = new BufferedReader(new InputStreamReader(con.getErrorStream()));
            }
            String inputLine;
            StringBuffer response = new StringBuffer();
            while ((inputLine = br.readLine()) != null) {
                response.append(inputLine);
            }
            br.close();
            System.out.println(response); // API 호출 결과를 콘솔에 출력
            // jsonToString() 메소드 호출하고 결과 받아옴
            result = jsonToString(response.toString());
            System.out.println(result); // 뭔가가 있는 줄 알았어요

        } catch (Exception e) {
            System.out.println(e);
        }
        return result;
    }
    private static void writeMultiPart(OutputStream out, String jsonMessage, File file, String boundary) throws
            IOException {
        StringBuilder sb = new StringBuilder();
        sb.append("--").append(boundary).append("\r\n");
        sb.append("Content-Disposition:form-data; name=\"message\"\r\n\r\n");
        sb.append(jsonMessage);
        sb.append("\r\n");

        out.write(sb.toString().getBytes("UTF-8"));
        out.flush();

        if (file != null && file.isFile()) {
            out.write(("--" + boundary + "\r\n").getBytes("UTF-8"));
            StringBuilder fileString = new StringBuilder();
            fileString
                    .append("Content-Disposition:form-data; name=\"file\"; filename=");
            fileString.append("\"" + file.getName() + "\"\r\n");
            fileString.append("Content-Type: application/octet-stream\r\n\r\n");
            out.write(fileString.toString().getBytes("UTF-8"));
            out.flush();

            try (FileInputStream fis = new FileInputStream(file)) {
                byte[] buffer = new byte[8192];
                int count;
                while ((count = fis.read(buffer)) != -1) {
                    out.write(buffer, 0, count);
                }
                out.write("\r\n".getBytes());
            }

            out.write(("--" + boundary + "--\r\n").getBytes("UTF-8"));
        }
        out.flush();
    }
    public String jsonToString(String jsonResultStr) {
        String resultText = "";
        // API 호출 결과 받은 JSON 형태 문자열에서 텍스트 추출
        // JSONParser  사용하지 않음
        // images / 0 / fields / inferText 추출
        JSONObject jsonObj = new JSONObject(jsonResultStr);
        JSONArray imageArray = (JSONArray) jsonObj.get("images");
        if(imageArray != null) {
            JSONObject tempObj = (JSONObject) imageArray.get(0);
            JSONArray fieldArray = (JSONArray) tempObj.get("fields");
            if(fieldArray != null) {
                for(int i=0; i<fieldArray.length(); i++) {
                    tempObj = (JSONObject) fieldArray.get(i);
                    resultText += (String) tempObj.get("inferText") + " ";
                }
            }
        } else {
            System.out.println("없음");
        }
        return resultText;
    }
}
~~~

~~~java
@RestController
public class APIRestController {
    @Autowired
    private OCRService ocrService;
    @RequestMapping("/clovaOCR")
    public String clovaOCR(@RequestParam("uploadFile") MultipartFile file){
        String result = "";
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
            // 서비스에서 반환된 텍스트를 result에 저장
            result = ocrService.clovaOCRService(filePathName);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return result;
    }
}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
 <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>OCR</title>
		<script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
		<script src="/js/ocr.js"></script>
	</head>
	<body>
		<!--  파일 업로드 -->
		<h3>OCR : 텍스트 추출</h3>
		<form id="ocrForm" enctype="multipart/form-data">
			파일 : <input type="file" id="uploadFile" name="uploadFile"> 
			<input type="submit" value="결과 확인">		
		</form>
		<br><br>
		
		<!-- 결과 출력 (텍스트) -->
		<h3>OCR : 텍스트 추출 결과</h3>
		<div id="resultDiv"></div>
		<br><br>
		
		<!-- 이미지 출력 (새로운 방법으로 알려줄 것임)  -->
		<h3>OCR : 원본 이미지 파일</h3>
		<div id="resultImg"></div>

		<br><br>
		<a href="/">index 페이지로 이동</a>
	</body>
</html>
~~~

~~~js
$(function () {
    // submit 했을 때 처리
    $('#ocrForm').on('submit', function (event) {
        event.preventDefault();
        var formData = new FormData($('#ocrForm')[0]);
        var fileName = $('#uploadFile').val().split("\\").pop();
        $.ajax({
            type : "post",
            enctype : "multipart/form-data",
            url : "clovaOCR",
            data : formData,
            processData : false, // 필수
            contentType : false, // 필수
            success:function (result) {
                $('#resultDiv').text(result);
                // 이미지 출력 (div에 append)
                $('#resultImg').empty();
                $('#resultImg').append('<img src="/images/'+fileName+'"/>');
            },
            error:function (e) {
                alert("오류 발생" + e);
            }
        });
    })
})
~~~

## Pose Estimation (포즈 인식)
- 입력된 비전 데이터를 통해 사람을 인식하고 포즈 분석 API 서비스
- 이미지 속의 사람을 감지하고 주요 신체부위(18개)의 좌표 정보와 정확도를 반환
- 포즈를 취하고 있는 사람이 포함된 이미지 파일 전송
- JSON 형태로 반환 : JSON 데이터 추출해서 이미지상 신체 각 부위에 인식 결과 출력

~~~java
@Service
public class PoseEstimationService {
    public ArrayList<PoseVO> poseEstimation(String filePathName) {

        StringBuffer reqStr = new StringBuffer();
        String clientId = "";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "";//애플리케이션 클라이언트 시크릿값";
        ArrayList<PoseVO> poseList = new ArrayList<PoseVO>();

        try {
            String paramName = "image"; // 파라미터명은 image로 지정
            String imgFile = filePathName;
            File uploadFile = new File(imgFile);
            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision-pose/v1/estimate"; // 사람 인식
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
                // JSON 문자열 추출 결과 받음
                poseList = jsonToVoList(response.toString());
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }
        return poseList;
    }
    // API 서버로부터 받은 JSON 형태의 결과 데이터를 전달받아서 index, x, y 추출하고
    // PoseVO 리스트 만들어 반환하는 함수
    public ArrayList<PoseVO> jsonToVoList(String jsonResultStr){
        ArrayList<PoseVO> poseList = new ArrayList<PoseVO>();
        double x, y;

        try {
            // JSON 형태의 문자열에서 JSON 오브젝트 "predictions" 추출해서 JSONArray에 저장
            // x, y 추출
            JSONParser jsonParser = new JSONParser();
            JSONObject jsonObj = (JSONObject) jsonParser.parse(jsonResultStr);
            JSONArray poseArray = (JSONArray) jsonObj.get("predictions");
            JSONObject obj0 = (JSONObject) poseArray.get(0);

            for(int i=0; i<18; i++) {
                // 신체 각 부위 이름이 "0", "1", 문자이므로  정수 i를 문자열로 변환
                // String.valueOf(i) 사용해서 문자열로 변환
                if(obj0.get(String.valueOf(i)) != null) {
                    JSONObject tempObj = (JSONObject) obj0.get(String.valueOf(i));
                    x = (double) tempObj.get("x");
                    y = (double) tempObj.get("y");
                } else {
                    x = 0;
                    y = 0;
                }
                // VO에 저장하고
                PoseVO vo = new PoseVO();
                vo.setIndex(i);
                vo.setX(x);
                vo.setY(y);
                // 리스트에 추가
                poseList.add(vo);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
        return poseList;
    }
}
~~~

~~~java
 @RequestMapping("/poseDetect")
    public ArrayList<PoseVO>  poseDetect(@RequestParam("uploadFile") MultipartFile file) {
        ArrayList<PoseVO> poseList = null;
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
            poseList = poseEstimationService.poseEstimation(filePathName);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return poseList;
    }
~~~

~~~java
public class PoseVO {
    private int index;
    private double x;
    private double y;

    public int getIndex() {
        return index;
    }
    public void setIndex(int index) {
        this.index = index;
    }
    public double getX() {
        return x;
    }
    public void setX(double x) {
        this.x = x;
    }
    public double getY() {
        return y;
    }
    public void setY(double y) {
        this.y = y;
    }
}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
 <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>OCR</title>
		<script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
		<script src="/js/pose.js"></script>
	</head>
	<body>
		<!--  파일 업로드 -->
		<h3>포즈 인식</h3>
		<form id="poseForm" enctype="multipart/form-data">
			파일 : <input type="file" id="uploadFile" name="uploadFile"> 
			<input type="submit" value="결과 확인">		
		</form>
		<br><br>
		
		<!-- 결과 출력  -->
		<h3>포즈 인식 결과를 이미지에 좌표로 표시</h3>
		<canvas id="poseCanvas" width="600" height="600"></canvas>
		<br><br>
		
		<!-- 각 신체 부위와 좌표 값 출력 -->
		<div id="resultDiv"></div>
		
		<br><br>
		<a href="/">index 페이지로 이동</a>
		
	</body>
</html>
~~~

~~~js
$(function(){
    $('#poseForm').on('submit', function(event){
        event.preventDefault();
        var formData = new FormData($('#poseForm')[0]);
        // 업로드된 파일명 알아오기
        var fileName = $('#uploadFile').val().split("\\").pop();
        //alert(fileName);
        $.ajax({
            url:"poseDetect",
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
            var canvas = document.getElementById("poseCanvas");
            var context = canvas.getContext("2d");

            var poseImage = new Image();
            poseImage.src ="/images/" + fileName;
            poseImage.width = canvas.width;
            poseImage.height = canvas.height;

            poseImage.onload = function(){
                context.drawImage(poseImage,0, 0, poseImage.width, poseImage.height );

                var colors = ["red", "blue", "yellow", "yellow","yellow","green", "green",
                    "green", "skyblue","skyblue","skyblue","black","black","black",
                    "pink","gold", "orange","brown"];

                var position = ["코", "목", "오른쪽 어깨", "오른쪽 팔굼치", "오른쪽 손목",
                    "왼쪽 어깨", "왼쪽 팔굼치", "왼쪽 손목", "오른쪽 엉덩이", "오른쪽 무릎",
                    "오른쪽 발목", "왼쪽 엉덩이", "왼쪽 무릎", "왼쪽 발목", "오른쪽 눈",
                    "왼쪽 눈", "오른쪽 귀", "왼쪽 귀"];

                var values = "";

                $.each(result, function(i){
                    if(this.x !=0 || this.y !=0){
                        context.strokeStyle=colors[i];//선색상
                        context.strokeRect(this.x * poseImage.width, this.y*poseImage.height, 2, 2);
                        var text = this.x.toFixed(2) + "," + this.y.toFixed(2);
                        context.font = '10px serif';
                        context.strokeText(text, this.x * poseImage.width, this.y*poseImage.height);
                    }
                    values += position[i] + "(" + this.x + ", " + this.y + ") <br>";
                });

                $('#resultDiv').html(values);
            };
        }	// function 끝
    });
});
~~~