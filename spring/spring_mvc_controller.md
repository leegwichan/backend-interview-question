# Spring Controller

### `@Controller` vs `@RestController`
- `@RestController` = `@Controller` + `@ResponseBody`
- `@Controller`: 주로 View(화면)를 반환하기 위해 사용, `ViewResolver`에서 반환한 문자열에 해당하는 View를 찾아 랜더링 한다.
- `@RestController` : 주로 REST API 용 Data(JSON/XML)를 반환하기 위해 사용, `HttpMessageConverter`에서 객체를 JSON이나 XML 형태의 데이터로 변환하여 HTTP Body에 담는다.

| 특징 | `@Controller` | `@RestController` |
| :--- | :--- | :--- |
| 주 용도 | 전통적인 Spring MVC (화면 렌더링) | RESTful API (데이터 제공) |
| 리턴 값 | View의 이름 (String) | Data 그 자체 (객체, 문자열 등) |
| 핵심 처리자 | `ViewResolver` | `HttpMessageConverter` |
| 동작 방식 | 리턴된 문자열을 파일 경로로 인식하여 HTML을 찾음 | 리턴된 객체를 JSON/XML로 변환하여 HTTP Body에 씀 |
| @ResponseBody | 데이터를 리턴하려면 메서드마다 붙여야 함 | 기본적으로 모든 메서드에 적용됨 |
