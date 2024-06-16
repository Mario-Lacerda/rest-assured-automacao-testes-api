<h1 align="center">
  Explorando o Rest Assured Para a Automação de Testes de API - Json Server
</h1>





### **Projeto de Automação de Testes de API com Rest-Assured**

#### **Objetivo:**

O objetivo deste projeto é fornecer um guia completo para criar testes de automação de API usando a biblioteca Rest-Assured.



#### **Configuração:**

- Java 11 ou superior
- Maven
- Rest-Assured



#### **Estrutura do Projeto:**

plaintext



```plaintext
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com.example.restassuredautomation
│   │   │       ├── BaseTest.java
│   │   │       ├── GetRequestTest.java
│   │   │       └── PostRequestTest.java
│   │   └── resources
│   └── test
├── README.md
```



#### **pom.xml:**

xml



```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>rest-assured-automação-testes-api</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>rest-assured</artifactId>
            <version>5.2.1</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```



#### **BaseTest.java:**

java



```java
import io.restassured.RestAssured;
import org.junit.BeforeClass;

public class BaseTest {

    @BeforeClass
    public static void setup() {
        RestAssured.baseURI = "https://reqres.in/api";
    }
}
```



#### **GetRequestTest.java:**

java



```java
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.junit.Test;

import static io.restassured.matcher.RestAssuredMatchers.*;
import static org.hamcrest.Matchers.*;

public class GetRequestTest extends BaseTest {

    @Test
    public void deveRetornarTodosOsUsuarios() {
        Response response = RestAssured.get("/users");

        response.then()
                .statusCode(200)
                .body("page", equalTo(1))
                .body("per_page", equalTo(6))
                .body("total", greaterThan(12))
                .body("data", hasSize(6));
    }

    @Test
    public void deveRetornarUmUsuarioEspecifico() {
        Response response = RestAssured.get("/users/2");

        response.then()
                .statusCode(200)
                .body("data.id", equalTo(2))
                .body("data.email", equalTo("janet.weaver@reqres.in"));
    }
}
```



#### **PostRequestTest.java:**

java



```java
import io.restassured.RestAssured;
import io.restassured.response.Response;
import org.junit.Test;

import static io.restassured.matcher.RestAssuredMatchers.*;
import static org.hamcrest.Matchers.*;

public class PostRequestTest extends BaseTest {

    @Test
    public void deveCriarUmNovoUsuario() {
        String requestBody = "{\"name\": \"John Doe\", \"job\": \"QA Engineer\"}";

        Response response = RestAssured.given()
                .header("Content-Type", "application/json")
                .body(requestBody)
                .post("/users");

        response.then()
                .statusCode(201)
                .body("name", equalTo("John Doe"))
                .body("job", equalTo("QA Engineer"));
    }
}
```



#### **README.md:**

plaintext



```plaintext
# Automação de Testes de API com Rest-Assured

## Introdução

Este projeto fornece um guia completo para criar testes de automação de API usando a biblioteca Rest-Assured.

## Pré-requisitos

* Java 11 ou superior
* Maven

## Configuração

1. Clone o projeto do GitHub.
2. Abra o projeto no seu IDE favorito (por exemplo, IntelliJ IDEA).
3. Execute `mvn clean install` para compilar o projeto.

## Estrutura do Projeto

O projeto é organizado nas seguintes pastas:

* **src/main/java:** Contém as classes de teste.
* **src/main/resources:** Contém quaisquer recursos necessários para os testes.
* **src/test:** Contém classes de teste unitário.

## Executando os Testes

Para executar os testes, execute o seguinte comando:
```



#### mvn test

plaintext



~~~plaintext
## Exemplos de Testes

### Testes de Solicitação GET

Os testes de solicitação GET verificam se a API retorna os dados esperados para diferentes pontos de extremidade.

**GetRequestTest.java:**

```java
@Test
public void deveRetornarTodosOsUsuarios() {
    Response response = RestAssured.get("/users");

    response.then()
        .statusCode(200)
        .body("page", equalTo(1))
        .body("per_page", equalTo(6))
        .body("total", greaterThan(12))
        .body("data", hasSize(6));
}
~~~



### Testes de Solicitação POST

Os testes de solicitação POST verificam se a API cria novos recursos com sucesso.

**PostRequestTest.java:**

java



```java
@Test
public void deveCriarUmNovoUsuario() {
    String requestBody = "{\"name\": \"John Doe\", \"job\": \"QA Engineer\"}";

    Response response = RestAssured.given()
        .header("Content-Type", "application/json")
        .body(requestBody)
        .post("/users");

    response.then()
        .statusCode(201)
        .body("name", equalTo("John Doe"))
        .body("job", equalTo("QA Engineer"));
}
```



## Conclusão

Este projeto fornece um ponto de partida abrangente para criar testes de automação de API usando Rest-Assured. Ele inclui exemplos de testes de solicitação GET e POST e pode ser facilmente estendido para cobrir casos de teste adicionais.







## Conclusão



Este projeto fornece um ponto de partida abrangente para criar testes de automação de API usando Rest-Assured. Ele inclui exemplos de testes de solicitação GET, POST, PUT e DELETE e pode ser facilmente estendido para cobrir casos de teste adicionais.



##  License

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

