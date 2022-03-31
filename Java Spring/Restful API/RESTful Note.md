# RESTful Web Service
- **REpresentational State Transfer**: an architecture that defines principles to design Web Service: resource configuration, method through HTTP

## 1. 4 principles: 
- HTTP methods: POST, GET, PUT, DELETE
- Stateless: each request must contain all of the information necessary to be understood by the server, rather than be dependent on the server remembering prior requests.
- Displays project path as URLs
- JSON and XML: client can change mime type as its desirer: `JSON - application/json`, `XML - application/xml`, `XHTML - application/xhtml+xml`

## 2. Annotations
- `@RestController` = `ResponseBody` + `@Controller` (the return string can be a domain object instead of a view)
- `@RequestParam(defaultValue="", name="", required="true/false", value="")`: to get the value of parameters in URL
- `@ResponseBody`: notify this method return an object that will be converted to JSON
- `@RequestBody`: notify Spring to convert JSON data to Object
- `ResponseEntity`: similar to @ResponseBody but with more info: status code, headers, body
- `@PathVariable`: get value in URL
- `MediaType`: parameters' filter, return data that have the same type as MediaType.
- `@ControllerAdvice`: handle exception
 



