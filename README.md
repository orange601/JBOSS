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

1. 1차적인 해결방법은 http://localhost:9990/console/ 에 접속해서 JBOSS가 생성한 war파일이 deploy돼 있지만   
이걸 제거하고 STS에서 생성한 WAR파일을 재 배포해야 한다. 혹은 멀티모듈 jar파일을 lib폴더에 직접 옮겨도 상관은 없다.   
하지만 문제가 있다. 빌드를 할때마다 재 배포해야한다. ( JBOSS가 멀티모듈로 인식하게 만들어야함 )   

2. standalone\configuration\standalone.xml 설정을 변경한다.
중간 부분에 deployment-scanner에서 path 부분에 war파일 위치를 full path로 지정하면 된다.
````xml
<deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" runtime-failure-causes-rollback="${jboss.deployment.scanner.rollback.on.failure:false}"/>
````

