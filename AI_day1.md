## AI 플랫폼

## Naver AI Platform (네이버 인공지능 플랫폼)
- Naver CLOVA
- 네이버에서 개발한 인공지능 기술로 AI Service를 제공
- API 형태로 이용 가능 (코드 제공)
  - 요청 방식 / 응답 방식(결과) 지정
  - 지정된 규칙대로 요청하고 응답 받아서 사용 (AI 서비스 제공)
- 네이버 클라우드 플랫폼에서 이용할 수 있는 서비스

## Naver AI API 서비스
- CLOVA Face Recognition (CFR)
- CLOVA OCR (Optical Character Recognition)
- CLOVA Speech Recognition (CSR)
- CLOVA Voice - Premium
- CLOVA Chatbot
- Pose estimation
- Object Detection

### CLOVA Face Recognition (CFR)
- 이미지 속의 얼굴을 감지하고 인식하여 얻은 다양한 정보를 제공하는 API 서비스
- 입력된 비전 데이터(사진 파일)를 통해 얼굴을 인식하거나 얼굴을 감지
- 유명인 얼굴 인식 API 서비스
  - 닮은 유명인 이름, 닮은 정보 (정확도)
- 얼굴 감지 API 서비스
  - 감지된 얼굴을 분석한 정보
  - 성별, 추정 나이, 감정, 얼굴 방향 등

### CLOVA OCR (Optical Character Recognition)
- 광학 문자 인식 API 서비스
- 사진 속에서 텍스트 정보를 찾고 의미를 판별하는 기술
- 언어와 이미지 데이터를 입력 받아서, 그에 맞는 인식 결과를 텍스트로 반환

### CLOVA Speech Recognition (CSR)
- 음성 인식 API 서비스
- 사람의 목소리를 텍스트로 변환 
- 음성을 텍스트로 변환 : STT(Speech-To-Text)
- 음성 파일을 입력 받아서 변환된 텍스트로 반환
- 언어 선택 가능

### CLOVA Voice - Premium
- 챗봇 제작 API 서비스
- 사용자의 질문 의도를 이해하여 고객 대응 등 다양한 서비스에 활용할 수 있는 Chatbot 제작 지원

### Pose estimation
- 이미지 내 사람, 동물, 사물 등 객체의 타입과 위치를 감지하여 정보를 제공하는 API 서비스
- 탐지된 객체명, 객체의 수, 바운딩 박스용 좌표, 객체별 확률값

### AI API 사용 방법
- AI 플랫폼 활용한 지능형 웹 서비스 제공
  - 뷰 페이지 (서비스 요청) -> 컨트롤러 -> 서비스(API 요청) -> 결과반환 -> 컨트롤러 -> 뷰 페이지로 결과 출력
  - API 요청 : 네이버 서버에 요청
    - 서비스 클래스에서 메소드로 구현 (그대로 복사해서 요청에 필요한 항목들만 변경해서 서비스 요청)
      - 반환값 메소드이름() {
  		- 여기에 API 코드 복사;
  		- 변경;
          - }
    - 서버로부터 반환된 결과값을 추출해서 
    - 컨트롤러에게 반환

### 요청 / 응답 결과
- CLOVA Face Recognition (CFR)
  - 이미지(얼굴 사진) 파일 전송
  - JSON 형태로 반환 : JSON 데이터 추출해서 출력
    - 자바 코드로 JSON 추출
- CLOVA OCR (Optical Character Recognition)
  - 텍스트가 포함된 이미지 파일 전송
  - JSON 형태로 반환 : JSON 데이터 추출해서 출력
- CLOVA Speech Recognition (CSR)
  - 음성 파일 전송
  - JSON  형태로 반환 : JSON 데이터 추출해서 출력
- CLOVA Voice - Premium
  - 문자열 또는 텍스트 파일 전송
  - 스트림으로 반환 받아서 파일로 저장하고 웹 브라우저에서 음성 파일 PLAY
- CLOVA Chatbot
  - 텍스트 또는 음성 파일 전송
  - SON  형태로 반환 : JSON 데이터 추출해서 출력
- Pose estimation
  - 포즈를 취하고 있는 사람이 포함된 이미지 파일 전송
  - SON 형태로 반환 : JSON 데이터 추출해서 이미상 신체 각 부위에 인식 결과 출력
- Object Detection
  - 사람, 동물, 사물 등 객체가 포함된 이미지 파일 전송
  - SON  형태로 반환 : JSON 데이터 추출해서 출력

## CLOVA Face Recognition (CFR) 실습 (유명인 유사도 측정)
- 스프링 부트 프로젝트 생성
- JSON dependency  추가
  - json-simple
  - json
- CelebrityVO 생성
- CFRCelebrityService 클래스 추가
  - clovaFaceRecogCel() 메소드 추가
    - API Java 코드 복사해서 붙여넣기
- APIController에 추가
- celebrityView.jsp 생성
- index.jsp에 추가
- 콘솔에 JSON 형태의 결과 출력 확인
- JSON 데이터 추출
  - 결과로 받은 JSON 형식의 문자열에서 value와 confidence추출해서 CelebrityVO에 저장
  - CFRCelebrityService 클래스에 메소드로 추가
    - jsonToVo(String jsonResultStr)
      - 결과로 받은 JSON 문자열을 전달 받아, value와 confidence추출
      - CelebrityVO에 저장한 후 리스트(ArrayList)에 추가
      - CelebrityVO 리스트 반환
    - jsonToVoList(String jsonResultStr) 메소드 추가로 인한 변경 사항
      - clovaFaceRecogCel() 메소드에서 jsonToVoList() 호출하는 코드 추가
      - 서비스에서 컨트롤러에게 반환하기 위해 clovaFaceRecogCel() 메소드의 반환형 변경 및 return 값 추가
      - 컨트롤러에서는 서비스 호출하고 결과 받는 코드로 변경하고 Model 추가
      - celebrityView.jsp에 출력 부분 추가

~~~java
public class CelebrityVO {
    private String value;
    private double confidence;

    public String getValue() {
        return value;
    }
    public void setValue(String value) {
        this.value = value;
    }
    public double getConfidence() {
        return confidence;
    }
    public void setConfidence(double confidence) {
        this.confidence = confidence;
    }
}
~~~

~~~java
@Controller
public class APIController {
    @Autowired
    private CFRCelebrityService cfrserviceCel;

    @RequestMapping("/")
    public String index() {
        return "index";
    }
    @RequestMapping("/faceRecogCel")
    public String faceRecogCel() {
        cfrserviceCel.clovaFaceRecogCel();
        return "celebrityView";
    }
}
~~~

~~~java
package com.ai.ex.naver_ai_platform.service;

import com.ai.ex.naver_ai_platform.model.CelebrityVO;
import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.JSONParser;
import org.springframework.stereotype.Service;
import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLConnection;
import java.util.ArrayList;

@Service
public class CFRCelebrityService {
    public ArrayList<CelebrityVO> clovaFaceRecogCel(String filePathName) {
        //StringBuffer reqStr = new StringBuffer();
        String clientId = "";//애플리케이션 클라이언트 아이디값";
        String clientSecret = "";//애플리케이션 클라이언트 시크릿값";

        ArrayList<CelebrityVO> celList = new ArrayList<CelebrityVO>();

        try {
            String paramName = "image"; // 파라미터명은 image로 지정
            // String imgFile = "C:/ai/song.jpg";  // 전송할 이미지 파일
            String imgFile = filePathName;
            File uploadFile = new File(imgFile);
            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision/v1/celebrity"; // 유명인 얼굴 인식
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
                System.out.println(response.toString()); // 서버로부터 받은 결과를 콘솔에 출력 (JSON 형태)
                // jsonToVoList() 메소드 호출하면서 결과 json 문자열 전달
                celList = jsonToVoList(response.toString());
            } else {
                System.out.println("error !!!");
            }
        } catch (Exception e) {
            System.out.println(e);
        }

        // CelebrityVO 리스트 반환
        return celList;
    }

    // API 서버로부터 받은 JSON 형태의 결과 데이터를 전달받아서 value와 confidence 추출하고
    // VO 리스트 만들어 반환하는 함수
    public ArrayList<CelebrityVO> jsonToVoList(String jsonResultStr){
        ArrayList<CelebrityVO> celList = new ArrayList<CelebrityVO>();

        try {
            //JSON 형태의 문자열에서 JSON 오브젝트 "faces" 추출해서 JSONArray에 저장
            JSONParser jsonParser = new JSONParser();
            JSONObject jsonObj = (JSONObject) jsonParser.parse(jsonResultStr);
            JSONArray celebrityArray = (JSONArray) jsonObj.get("faces");

            // JSONArray의 각 요소에서 value와 confidence 추출하여
            // CelebrityVO 담아 리스트에 추가
            if(celebrityArray != null) {
                // value와 confidence 추출
                // JSONArray  각 요소에서 value와 confidence 추출
                for(int i=0; i < celebrityArray.size(); i++){
                    JSONObject tempObj = (JSONObject) celebrityArray.get(i);
                    tempObj = (JSONObject) tempObj.get("celebrity");
                    String value = (String) tempObj.get("value");
                    double confidence = (double) tempObj.get("confidence");

                    // VO에 저장해서 리스트에 추가
                    CelebrityVO vo = new CelebrityVO();
                    vo.setValue(value);
                    vo.setConfidence(confidence);

                    celList.add(vo);
                }
            } else {
                //유명인을 찾지 못한 경우 ("faces" : [])
                CelebrityVO vo = new CelebrityVO();
                vo.setValue("없음");
                vo.setConfidence(0);
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
        return celList;
    }
}
~~~

~~~jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <head>
        <title>결과</title>
    </head>
    <body>
        <h1>인식 결과</h1>
        <a href="/">인덱스 이동</a>
    </body>
</html>
~~~

- 첨부 파일로 변경
  - 현재 코드에서 파일명을 직접 적었는데, 파일을 서버에 올리는 기능 추가
  - 서버의 특정 폴더에 이미지 저장
  - 외부 폴더 지정
  - 결과 페이지에서 서버로 올린 이미지 출력
  - celebrityView.jsp에 파일 업로드 부분 추가
  - 컨트롤러에 추가

~~~java
public class CelebrityVO {
    private String value;
    private double confidence;

    public String getValue() {
        return value;
    }
    public void setValue(String value) {
        this.value = value;
    }
    public double getConfidence() {
        return confidence;
    }
    public void setConfidence(double confidence) {
        this.confidence = confidence;
    }
}
~~~

~~~java
@Controller
public class APIController {
	@Autowired
	private CFRCelebrityService cfrServiceCel;
	
	// index 페이지로 이동
	@RequestMapping("/")
	public String index() {
		return "index";
	}
	
	@RequestMapping("/faceRecogCelForm")
	public String faceRecogCelForm() {
		return "celebrityView";
	}

	// (1) 유명인 얼굴인식 API 호출 : 결과를 콘솔에 출력
	// 변경  -> 
	// (2) 유명인 얼굴인식 API 호출 결과 CelebrityVO 리스트 받아서 Model에 담아 celebrityView.jsp 뷰 페이지로 전달
	@RequestMapping("/faceRecogCel")
	public String  faceRecogCel(@RequestParam("uploadFile") MultipartFile file,			
													 Model model) throws IOException {
		// 1. 파일 저장 경로 설정 : 실제 서비스되는 위치 (프로젝트 외부에 저장)
		String uploadPath = "/Users/gobyeongchae/Desktop/productImages";
		// 2. 원본 파일 이름 알아오기
		String originalFileName = file.getOriginalFilename();
		String filePathName = uploadPath + originalFileName;
		// 3. 파일 생성
		File file1 = new File(filePathName);
		// 4. 서버로 전송
		file.transferTo(file1);
		ArrayList<CelebrityVO> celList = new ArrayList<CelebrityVO>();
		// 서비스에 파일 path와 파일명 전달  -> 서비스 메소드에서 변경
		// 서비스에서 반환된 CelebrityVO 리스트 저장
		celList = cfrServiceCel.clovaFaceRecogCel(filePathName);
		//Model에 "celList" 이름으로 저장 -> view 페이지로 전달
		model.addAttribute("celList", celList);
		model.addAttribute("fileName", originalFileName);
		return "celebrityView";
	}

~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>유명인 얼굴 인식</title>
	</head>
	<body>
		<!-- 서버로 파일 전송  -->
		<h3>유명인 얼굴 인식</h3>
		<form id="celebrityForm" method="post" action="<c:url value='/faceRecogCel'/>" enctype="multipart/form-data">
			파일 : <input type="file" id="uploadFile" name="uploadFile"> 
			<input type="submit" value="결과 확인">		
		</form>
		<hr>
		<c:if test="${not empty celList }">
		<h3>유명인 얼굴 인식 결과</h3>
			<table border="1" width="400">
				<tr><th>유명인</th><th>정확도</th></tr>
				<c:forEach items="${celList}" var="cel">
					<tr>
						<td>${cel.value }</td>
						<td><fmt:formatNumber value="${cel.confidence }" pattern="0.0000" /></td>
					</tr>
				</c:forEach>				
			</table>
		</c:if>
		<br><br>
		<c:if test="${not empty fileName }">
			<img src="<c:url value='/images/${fileName}' />">
		</c:if>
		<br><br>
		<a href="/">index 페이지로 이동</a>
	</body>
</html>
~~~

## CLOVA Face Recognition(CFR) (얼굴 감지)
- CFRFaceRecogService 클래스 생성
- faceRecog() 메소드 추가
  - faceRecog() 메소드 추가
  - Client ID / Client Secret 
  - 파일 경로 및 파일명  직접 입력 
  - 반환된 결과 콘솔 출력 확인
- 컨트롤러에 추가
- faceRecogView.jsp 추가
- index.jsp에 추가
- JSON 데이터 출력 / 파일 업로드 기능 추가
  - gender / age / emotion / pose
  - value와 confidence 출력
  - jsonToVoList(String jsonResultStr) 메소드 추가로 인한 변경 사항
    - faceRecog() 메소드에서 jsonToVoList() 호출하는 코드 추가
    - 서비스에서 컨트롤러에게 반환하기 위해 faceRecog() 메소드의 반환형 변경 및 return 값 추가
    - 컨트롤러에서는 서비스 호출하고 결과 받는 코드로 변경하고 Model 추가
    - faceRecogView.jsp에 출력 부분 추가
- 파일 업로드 기능 추가
  - 파일을 서버에 올리는 기능 추가
  - 서버의 특정 폴더에 이미지 저장
  - 외부 폴더 지정
  - 결과 페이지에서 서버로 올린 이미지 출력
  - faceRecogView.jsp에 파일 업로드 부분 추가
  - 컨트롤러에 추가

~~~java
public class FaceVO {
	private String gender;
	private double genderConf;
	private String age;
	private double ageConf;
	private String emotion;
	private double emotionConf;
	private String pose;
	private double poseConf;
	
	public String getGender() {
		return gender;
	}
	public void setGender(String gender) {
		this.gender = gender;
	}
	public double getGenderConf() {
		return genderConf;
	}
	public void setGenderConf(double genderConf) {
		this.genderConf = genderConf;
	}
	public String getAge() {
		return age;
	}
	public void setAge(String age) {
		this.age = age;
	}
	public double getAgeConf() {
		return ageConf;
	}
	public void setAgeConf(double ageConf) {
		this.ageConf = ageConf;
	}
	public String getEmotion() {
		return emotion;
	}
	public void setEmotion(String emotion) {
		this.emotion = emotion;
	}
	public double getEmotionConf() {
		return emotionConf;
	}
	public void setEmotionConf(double emotionConf) {
		this.emotionConf = emotionConf;
	}
	public String getPose() {
		return pose;
	}
	public void setPose(String pose) {
		this.pose = pose;
	}
	public double getPoseConf() {
		return poseConf;
	}
	public void setPoseConf(double poseConf) {
		this.poseConf = poseConf;
	}
}
~~~

~~~java
@ Service 
public class CFRFaceRecogService {
	public ArrayList<FaceVO> faceRecog(String filePathName) {
		 StringBuffer reqStr = new StringBuffer();
	        String clientId = "";//애플리케이션 클라이언트 아이디값";
	        String clientSecret = "";//애플리케이션 클라이언트 시크릿값";
	        
	        ArrayList<FaceVO> faceList = faceList = new ArrayList<FaceVO>();

	        try {
	            String paramName = "image"; // 파라미터명은 image로 지정
	            //String imgFile = "C:/ai/family.jpg";
	            String imgFile = filePathName;
	            File uploadFile = new File(imgFile);
	            String apiURL = "https://naveropenapi.apigw.ntruss.com/vision/v1/face"; // 얼굴 감지
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
	                System.out.println(response.toString()); // 서버로부터 반환된 결과 출력 (JSON 형태)
	                faceList = jsonToVoList(response.toString());
	            } else {
	                System.out.println("error !!!");
	            }
	        } catch (Exception e) {
	            System.out.println(e);
	        }
	        
	        return faceList;
	}
	
	// API 서버로부터 받은 JSON 형태의 데이톨부터 value와 confidence 추출해서
	// VO 리스트 만들어 반환
	public ArrayList<FaceVO> jsonToVoList(String jsonResultStr){
		ArrayList<FaceVO> faceList = faceList = new ArrayList<FaceVO>();
		
		try {			
			JSONParser jsonParser = new JSONParser();
			JSONObject jsonObj = (JSONObject) jsonParser.parse(jsonResultStr);
			JSONArray faceArray = (JSONArray) jsonObj.get("faces");
			
			//JSON 형태의 문자열에서 JSON 오브젝트 "faces" 추출해서 JSONArray에 저장
			if(faceArray != null) {
				// JSONArray의 각 요소에서 value와 confidence 추출
				for(int i=0; i < faceArray.size(); i++) {
					FaceVO vo = new FaceVO();
					JSONObject tempObj = (JSONObject) faceArray.get(i);
					
					String value = "";
					double confidence = 0;
					
					// gender  추출
					JSONObject genObj = (JSONObject) tempObj.get("gender");
					value = (String) genObj.get("value");
					confidence = (double) genObj.get("confidence");
					// vo gender 값 설정
					vo.setGender(value);
					vo.setGenderConf(confidence);					
					
					// age  추출
					JSONObject ageObj = (JSONObject) tempObj.get("age");
					value = (String) ageObj.get("value");
					confidence = (double) ageObj.get("confidence");
					// vo age 값 설정
					vo.setAge(value);
					vo.setAgeConf(confidence);					
					
					// emotion  추출
					JSONObject emotObj = (JSONObject) tempObj.get("emotion");
					value = (String) emotObj.get("value");
					confidence = (double) emotObj.get("confidence");
					// vo emotion 값 설정
					vo.setEmotion(value);
					vo.setEmotionConf(confidence);					
					
					// pose  추출
					JSONObject poseObj = (JSONObject) tempObj.get("pose");
					value = (String) poseObj.get("value");
					confidence = (double) poseObj.get("confidence");
					// vo pose 값 설정
					vo.setPose(value);
					vo.setPoseConf(confidence);
					// FaceVO에 담아 리스트에 추가
					faceList.add(vo);
				}
			} else {
				//감지한 얼굴이 없는 경우 ("faces":[])
				FaceVO vo = new FaceVO();
				vo.setGender("없음");
				vo.setGenderConf(0);
				vo.setAge("없음");
				vo.setAgeConf(0);
				vo.setEmotion("없음");
				vo.setEmotionConf(0);
				vo.setPose("없음");
				vo.setPoseConf(0);				
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
		return faceList;
	}	
}
~~~

~~~java
@Controller
public class APIController {
	@Autowired
	private CFRCelebrityService cfrServiceCel;
	
	@Autowired
	private CFRFaceRecogService cfrRecogService;
	
	@RequestMapping("/faceRecogForm")
		public String faceRecogForm() {
			return "faceRecogView";
		}
	// (1) 얼굴 감지 API 호출 : 결과를 콘솔에 출력
	@RequestMapping("/faceRecog")
	public String faceRecog(@RequestParam("uploadFile") MultipartFile file,
			Model model) throws IOException {
		// 1. 파일 저장 경로 설정 : 실제 서비스되는 위치 (프로젝트 외부에 저장)
		String uploadPath = "/Users/gobyeongchae/Desktop/productImages";
		// 2. 원본 파일 이름 알아오기
		String originalFileName = file.getOriginalFilename();
		String filePathName = uploadPath + originalFileName;
		// 3. 파일 생성
		File file1 = new File(filePathName);
		// 4. 서버로 전송
		file.transferTo(file1);
		ArrayList<FaceVO> faceList = new ArrayList<FaceVO>();
		faceList = cfrRecogService.faceRecog(filePathName);
		model.addAttribute("faceList", faceList);
		System.out.println(faceList+"ee");
		model.addAttribute("fileName", originalFileName);
		return "faceRecogView";
	}
}
~~~

~~~jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h3>얼굴 감지</h3>
	<!-- 서버로 파일 전송 -->
	<form id="faceRecogForm" method="post"
		action="<c:url value='/faceRecog'/>" enctype="multipart/form-data">
		파일 : <input type="file" id="uploadFile" name="uploadFile">  
		<input type="submit" value="결과 확인">
	</form>
	<c:if test="${not empty faceList}">
		<h3>얼굴 감지 결과</h3>
		<table border="1" width="800">
			<tr>
				<th>성별</th>
				<th>성별 정확도</th>
				<th>나이</th>
				<th>나이 정확도</th>
				<th>감정</th>
				<th>감정 정확도</th>
				<th>포즈</th>
				<th>포즈 정확도</th>
			</tr>
			<c:forEach items="${faceList }" var="face">
				<tr>
					<td>${face.gender }</td>
					<td><fmt:formatNumber value="${face.genderConf }"
							pattern="0.0000" /></td>
					<td>${face.age }</td>
					<td><fmt:formatNumber value="${face.ageConf }"
							pattern="0.0000" /></td>
					<td>${face.emotion }</td>
					<td><fmt:formatNumber value="${face.emotionConf }"
							pattern="0.0000" /></td>
					<td>${face.pose }</td>
					<td><fmt:formatNumber value="${face.poseConf }"
							pattern="0.0000" /></td>
				</tr>
			</c:forEach>
		</table>
	</c:if>
	<br><br>
	<c:if test="${not empty fileName}">
		<img src="<c:url value='/images/${fileName}'/>"/>
	</c:if>
	<br><br>
	<a href="/">index 페이지 이동</a>
</body>
</html>
~~~