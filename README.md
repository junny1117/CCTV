# Events-Detection-from-CCTV-Video
1. 프로젝트 개요
- CCTV 영상에서 특정 구역 내의 객체(사람, 자동차)를 실시간으로 검지하고, 침입자 발생과 같은 이벤트를 자동으로 인지하는 시스템 구축 
- 객체 검지 기술(YOLOv5)을 활용하여 영상을 분석하고, 발생한 이벤트를 실시간으로 웹을 통해 확인할 수 있도록 구현
- 사용자는 웹 인터페이스를 통해 관심 구역을 설정하고, 발생한 이벤트를 기록 및 관리 가능

2. 프로젝트 목적
- 실시간 객체 검지 및 이벤트 처리: CCTV 영상에서 사람과 자동차 실시간으로 검지하고, 특정 구역에서 발생하는 이벤트(침입자 발생)를 자동으로 인식하여 경고
- 웹 기반 관리: 이벤트 검지 및 기록을 웹 인터페이스를 통해 제공하여, 사용자가 실시간으로 모니터링하고 데이터 관리 가능

3. 주요 사용 기술
- 프레임워크: Flask 
- 객체 검지: YOLO V5
- 비디오 처리: OpenCV
- 데이터베이스 SQLite
- 웹 소켓 통신(실시간 알림) – Flask-SocketIO
- 프론트앤드(웹 인터페이스) – HTML, CSS

4. 데이터베이스 설계  
- 발생한 이벤트의 종류(침입자 발생 등), Confidence, 발생시간을 Event 테이블에 기록하도록 설계 
- 이벤트가 발생할 때마다 Event 테이블에 추가
- 웹 페이지의 결과조회 페이지를 통해 최신순으로 정렬하여 이벤트 로그를 확인할 수 있으며 Flask-SocketIO를 통해 메인 페이지에 실시간으로 표시 

5. 객체 검지 및 이벤트 처리
- 객체 검지는 YOLO V5 모델을 사용하여 진행되며 OpenCV 라이브러리를 이용해 가져온 CCTV 영상 또는 지정된 영상에서 객체(사람, 자동차)를 실시간으로 검지하고 정해진 로직에 따라 이벤트를 인식하고 처리
- 이벤트 인지 로직: 
- 침입: 사람이 설정된 구역에 들어올 경우 인지
- 불법주차: 차량이 설정된 구역에 들어올 경우 인지
- 배회: 특정 영역에 사람이 일정 시간 이상 머무를 경우 인지 
- 구역 설정은 OpenCV의 selectROI 메소드를 이용해 진행되며 관리자가 마우스를 이용해 원하는 지역을 드래그하여 설정 가능

6. 웹 애플리케이션 구조
- Flask를 사용하여 웹페이지와 기타 기능을 제공하며 아래와 같은 페이지들로 구성
로그인 페이지: 관리자 로그인 기능 제공. 로그인 상태가 아닌 상태에서 다른 페이지에 접근을 시도하면 로그인 페이지로 리다이렉트하도록 해 로그인 된 상태에서만 다른 페이지에 접근할 수 있도록 구현
- 메인페이지: 실시간 CCTV 영상을 표시하고 검지된 이벤트를 실시간으로 표시 및 결과조회, 구역 설정을 할 수 있는 버튼 제공 
- 결과 조회 페이지: 데이터베이스에 기록된 이벤트를 최신 순으로 조회가능 
설정 페이지: 위험구역, 제한구역 설정 가능

7. 주요 구현 흐름
![image](https://github.com/user-attachments/assets/37d9f36d-3647-431d-aaea-a3507d8dae52)
![image](https://github.com/user-attachments/assets/06d24b35-fd87-44fe-ba15-0dce611c7176)

8. 실행 결과 이미지
![image](https://github.com/user-attachments/assets/b2daba03-e1b1-4e2e-b719-f178453c172e)
![image](https://github.com/user-attachments/assets/bc5bf651-99d7-404f-9315-ed72ce1d7362)
![image](https://github.com/user-attachments/assets/1c6dc02d-1f9e-412f-b850-3247f98023c9)

