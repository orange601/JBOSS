# JBOSS + Spring Boot + Gradle + Multi Module 프로젝트
- JBOSS를 통한 Multi Module 프로젝트

#### 환경 ####
Spring Tool Suite 4 
- Version: 4.9.0.RELEASE

WAS
  - Red Hat JBoss EAP 7.3 ( STS PLUG-IN )

#### ISSUE ####
STS의 JBOSS를 통해 프로젝트 실행 시 자동으로 WAR가 생성이 되는데   
WAR의 위치가 \standalone\deployments에 위치하게 된다.    
문제는 STS프로젝트에서 생성된 war와 JBOSS가 생성한 war가 차이가 있는데   
JBOSS가 생성한 war에는 의존성이 있는 프로젝트가 lib폴더에 존재하지 않는다는것이다.    
( 의존성이 있는 프로젝트는 lib폴더에 생성돼야 함 )   
그래서 jboss가 생성한 war를 사용할 수 없고 현재 sts에서 생성한 war파일을 사용해야 멀티모듈 인식이 가능하다.    
http://localhost:9990/console/ 에 접속하게 되면 JBOSS가 생성된 war파일이 존재하는데 이걸 제거하고
STS에서 생성한 WAR파일을 재 배포해야 한다.

1. 문제점
- 빌드를 할때마다 재 배포해야한다. ( JBOSS가 멀티모듈로 인식하게 만들어야함 )

