# spring-boot-mongodb-crud

This project explains CRUD (**C**reate, **R**ead, **U**pdate, **D**elete) operations using MongoTemplate and MongoRepository using spring boot and mongo DB.
In this app we are using Spring Data JPA for built-in methods to do CRUD operations and Mongo queries using MongoTemplate.     
`@EnableMongoRepositories` annotation is used on main class to Enable Mongo related configuration, which will read properties from `application.properties` file.

SET PATH=E:\apache-maven-3.8.6\bin;%PATH%

SET PATH=<Maven bin directory>;%PATH% (Install maven)

mvn spring-boot:run (Build and Run application)

mvn clean install (Build application and create **jar** file under target directory)

Run jar file from below path with given command

java -jar target/spring-boot-mongodb-0.0.1-SNAPSHOT.jar (Run jar application)

Or

> run main method from `SpringBootMongoDBApplication.java` as spring boot application.  

3. #### References:

    - https://github.com/bezkoder/spring-boot-data-mongodb
    - https://github.com/rahul-ghadge/spring-boot-mongodb-crud
    - https://github.com/scbushan05/spring-boot-mongodb

4. #### CRUD operation for Super Heroes

    In **com.spring.mongo.demo.controller.SuperHeroController.java** class, 
    we have exposed 5 endpoints for basic CRUD operations
    - GET All Super Heroes
    - GET by ID
    - POST to store Super Hero in DB
    - PUT to update Super Hero
    - DELETE by ID
    
    ```
    @RestController
    @RequestMapping("/super-hero")
    public class SuperHeroController {
        
        @GetMapping
        public ResponseEntity<List<?>> findAll();
    
        @GetMapping("/{id}")
        public ResponseEntity<?> findById(@PathVariable String id);
    
        @PostMapping
        public ResponseEntity<?> save(@RequestBody SuperHero superHero);
    
        @PutMapping
        public ResponseEntity<?> update(@RequestBody SuperHero superHero);
    
        @DeleteMapping("/{id}")
        public ResponseEntity<?> delete(@PathVariable String id);
    }
    ```
   
    In **com.spring.mongo.demo.repository.SuperHeroRepository.java**, we are extending `MongoRepository<Class, ID>` interface which enables CRUD related methods.
    ```
    public interface SuperHeroRepository extends MongoRepository<SuperHero, String> {
    }
    ```
   
   In **com.spring.mongo.demo.service.impl.SuperHeroServiceImpl.java**, we are autowiring above interface using `@Autowired` annotation and doing CRUD operation.



5. #### JPA And Query operation for Employee
    In **com.spring.mongo.demo.controller.EmployeeController.java** class JPA related queries API Endpoints are placed.
    In **com.spring.mongo.demo.controller.EmployeeQueryController.java** class Mongo queries API Endpoints are placed.
    
 
 
    
### API Endpoints

- #### Super Hero CRUD Operations
    > **GET Mapping** http://localhost:8080/super-hero  - Get all Super Heroes
    
    > **GET Mapping** http://localhost:8080/super-hero/5f380dece02f053eff29b986  - Get Super Hero by ID
       
    > **POST Mapping** http://localhost:8080/super-hero  - Add new Super Hero in DB  
    
      Request Body  
      ```
        {
            "name": "Tony",
            "superName": "Iron Man",
            "profession": "Business",
            "age": 50,
            "canFly": true
        }
      ```
    
    > **PUT Mapping** http://localhost:8080/super-hero  - Update existing Super Hero for given ID 
                                                       
      Request Body  
      ```
        {
            "id": "5f380dece02f053eff29b986"
            "name": "Tony",
            "superName": "Iron Man",
            "profession": "Business",
            "age": 50,
            "canFly": true
        }
      ```
    
    > **DELETE Mapping** http://localhost:8080/super-hero/5f380dece02f053eff29b986  - Delete Super Hero by ID

- #### Employee Get Operations using JPA
    > **GET Mapping** http://localhost:8080/employee-jpa  - Get all Employees 
    
    > **GET Mapping** http://localhost:8080/employee-jpa/5f380dece02f053eff29b986  - Get Employee by ID
    
    > **GET Mapping** http://localhost:8080/employee-jpa/firstName/Rahul  - Get All Employees with firstname as Rahul 
    
    > **GET Mapping** http://localhost:8080/employee-jpa/one-by-firstName/Rahul  - Get **ONE** Employee with firstname as Rahul 
    
    > **GET Mapping** http://localhost:8080/employee-jpa/firstName-like/Rahul  - Get All Employees which contains Rahul in their firstname 
    
    > **GET Mapping** http://localhost:8080/employee-jpa/one-by-lastName/Ghadage  - Get **ONE** Employee with lastname as Ghadage 
    
    > **GET Mapping** http://localhost:8080/employee-jpa/salary-greater-than/10000  - Get All Employees whose salary is grater than 1000 
    
    > **POST Mapping** http://localhost:8080/employee-jpa/get-by-condition  - Get All Employees with multiple condition 
                                                           
    Request Body  
    ```
    {
        "id": "5f380dece02f053eff29b986"
        "empId": "1",
        "firstName": "Rahul",
        "lastName": "Khan",
        "salary": 5000
    }
    ``` 

- #### Employee Get Operations using Queries
    > **GET Mapping** http://localhost:8080/employee-query  - Get all Employees 
    
    > **GET Mapping** http://localhost:8080/employee-query/firstName/Rahul  - Get All Employees with firstname as Rahul 
    
    > **GET Mapping** http://localhost:8080/employee-query/one-by-firstName/Rahul  - Get **ONE** Employee with firstname as Rahul 
    
    > **GET Mapping** http://localhost:8080/employee-query/firstName-like/Rahul  - Get All Employees which contains Rahul in their firstname 
    
    > **GET Mapping** http://localhost:8080/employee-query/one-by-lastName/Ghadage  - Get **ONE** Employee with lastname as Ghadage 
    
    > **GET Mapping** http://localhost:8080/employee-query/salary-greater-than/10000  - Get All Employees whose salary is grater than 1000 
    
    > **POST Mapping** http://localhost:8080/employee-query/get-by-condition  - Get All Employees with multiple condition 
                                                           
    Request Body  
    ```
    {
        "id": "5f380dece02f053eff29b986"
        "empId": "1",
        "firstName": "Rahul",
        "lastName": "Khan",
        "salary": 5000
    }
    ``` 
