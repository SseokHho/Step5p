[스프링 웹 MVC]

(프로젝트 생성)

1. Maven Project
	war(Web Application Archive)
2. pom.xml
	- spring-webmvc
	- javax.servlet-api
	- java.servlet.jsp-api
	- jstl

3. web.xml
	- 패스 : src/main/webapp/WEB-INF
	
4. 빈등록 설정
	@Configuration
	@EnableWebMvc

(pom.xml)
	<dependencies>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>3.1.0</version>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>javax.servlet.jsp</groupId>
			<artifactId>javax.servlet.jsp-api</artifactId>
			<version>2.3.2-b02</version>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>

		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>5.0.2.RELEASE</version>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.7.0</version>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
					<encoding>utf-8</encoding>
				</configuration>
			</plugin>
		</plugins>
	</build>
	
----------------------------------------------------------------------
(실행)
http://localhost:8584/S09SpringMVC/index.html
http://localhost:8584/S09SpringMVC/hello?name=kim

(실행불가)
http://localhost:8584/S09SpringMVC/hello.jsp
http://localhost:8584/S09SpringMVC/WEB-INF/view/hello.jsp

(요청처리)
1. @Controller
	- 웹브라우저를 통해서 전송되는 요청을 처리 
2. @GetMapping
	- HTTP : GET 방식으로 요청을 받음
3. @RequestParam
	- request.getParameter("...")
	- required는 파라미터의 필수 유무 : true, false
4. HelloController.java
	- 요청 : http://localhost:8584/S09SpringMVC/hello?name=kim
	- 결과 : hello.jsp
	- 소스 : 
	@Controller
	public class HelloController {
		@GetMapping("/hello") // HTTP : GET 방식으로 요청을 받음
		public String hello(Model model,
				@RequestParam(value = "name", required = false) String name) {
			model.addAttribute("greeting", "안녕하세요, " + name);
			return "hello"; // 뷰이름 : hello.jsp
		}
	}




























