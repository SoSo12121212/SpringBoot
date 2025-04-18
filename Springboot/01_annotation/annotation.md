# 스프링부트 어노테이션 정리

## 어노테이션이란?

코드에 추가적인 정보와 의미를 부여하는 '주석'과 같은 특별한 표기 방식<br>
단순한 주석과는 달리, 컴파일러나 프레임 워크에 특정한 동작이나 처리 방식을 알려주는 역할을 함 <br>

컴퓨터에게 명령을 내리거나 정보를 전달하기 위해
@ 기호로 "이 클래스는 컨트롤러야!"<br>
"이 메소드는 데이터를 가져올 때 실행해!"<br>
"이 객체는 스프링이 대신 만들어줘!"<br>
라고 표시해두는 메모이자 자동 처리 지시서

   <br>

### 어노테이션을 사용하는 주요 이유<br>

**1.코드의 추가 정보 제공**<br>

- 클래스, 매서드, 변수 등에 대한 부가적인 정보를 표현할 수 있음
- 개발자의 의도를 명확하게 전달할 수 있음 <br>

**2.자동화된 작업 지원**<br>

- 컴파일러에게 특정 동작을 지시할 수 있음<br>
- 프레임워크가 코드를 자동으로 처리하거나 특별한 기능을 수행하도록 함<br>

**3.코드의 가독성 향상**<br>

- 복잡한 설정 파일 대신 코드 바로 위에 간단히 작성할 수 있음<br>
- 코드의 의미와 목적을 더 명확하게 표현할 수 있음 <br>

  - 프레임워크란? <br>
    개발에 필요한 기능을 미리 제공하는 코드 들 <br>
    코드를 더 쉽게 만들 수 있는 있도록 도와주는 틀<br>
    ex. 레고 블록 조립판

<br>

## 1. 컴포넌트 및 빈 관리 어노테이션 <br>

**@Component**
스프링에서 관리하는 일반 컴포넌트를 정의함<br>
클래스가 스프링 빈으로 등록<br>
스프링에게 "이 클래스는 스프링에서 관리해야 하는 객체야" 라고 알려주는 어노테이션 <br>

<br>

- **역할** <br>
  스프링이 해당 클래스의 인스턴스를 자동으로 생성하고 관리하는 역할을 함<br>

<Br>
여기서 궁금증! Q. 빈(bean)과 인스턴스(Instance)는 차이점이 뭐지?<br>
인스턴스는 클래스로부터 만들어진 객체 그 자체 <Br>
ex. 붕어빵 한개 , 레고 완성품<br>
<br>

User user=new User(); <br>

빈은 스프링이 자동 생성하고 관리하는 객체 <br>
ex.사물함안에 등록된 레고 완성품 <br>
@service<br>
public class UserService { <br>
User user=new User();
}
모든 빈은 인스턴스이지만, 모든 인스턴스가 빈은 아님<br>
빈은 클래스 위에 어노테이션을 꼭 붙여야 함!<br>
@Autowired로 자동 주입(의존성 주입) <br>
ex. @Autowired UserService userService;
<br>

@Component<Br>
public class UserService {<br>
public void hello() {<Br>
System.out.println("안녕하세요!");<Br>
}
}

  <br>
  @RestController<br>
public class MyController {<br>

@Autowired<br>
UserService userService;<br>

   <br>

@GetMapping("/hello")<Br>
public String hi() { <br>
userService.hello(); <br>
return "Hello!"; <br>
}<br>
}<br>
UserService는 인스턴스이면서 동시에 빈이야<br>

<br>

| 개념                   | 설명                                                                  | 역할                                         | 예시                                                                               |
| ---------------------- | --------------------------------------------------------------------- | -------------------------------------------- | ---------------------------------------------------------------------------------- |
| @SpringBootApplication | 스프링부트의 대표 어노테이션                                          | 설정 자동화, 부트스트랩 역할                 | -                                                                                  |
| @Component             | 클래스가 스프링 빈으로 등록됨. 스프링이 관리해야 하는 객체임을 나타냄 | 객체를 만들고 보관 (스프링 컨테이너)         | `@Service`, `@Repository`, `@Controller`                                           |
| @Autowired             | 의존성 자동 주입 어노테이션                                           | 객체를 자동으로 주입                         | `@Autowired HelloUtil helloUtil;`                                                  |
| @Service               | 내부적으로 `@Component` 포함, 비즈니스 로직 처리 용도                 | 서비스 계층                                  | -                                                                                  |
| @Repository            | 데이터베이스 연동 클래스에 사용                                       | DAO / 리포지토리 계층                        | -                                                                                  |
| @Controller            | 요청을 받아 view로 전달, Model 사용 시 HTML로 view 반환 가능          | 웹 요청 처리 (`@PostMapping`, `@GetMapping`) | -                                                                                  |
| @RestController        | JSON 반환을 위한 컨트롤러로 등록 (`@Controller + @ResponseBody`)      | REST API 응답 처리용 컨트롤러                | `@RestController public class HelloController { @Autowired HelloUtil helloUtil; }` |
