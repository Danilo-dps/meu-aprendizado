# Singleton - Padrão de Projeto Criacional

## Introdução
O Singleton é um padrão de projeto (design pattern) criacional que garante que uma classe tenha apenas uma instância e fornece um ponto de acesso global a essa instância. Ele é útil quando você precisa garantir que um recurso ou objeto seja compartilhado em toda a aplicação, como conexões de banco de dados, configurações globais ou caches.

## O que é o Singleton?
- **Objetivo**: Garantir que uma classe tenha apenas uma instância durante todo o ciclo de vida da aplicação.
- **Uso comum**: Quando você precisa controlar o acesso a recursos compartilhados ou evitar a criação desnecessária de múltiplas instâncias de um objeto.

### Características
- A classe Singleton tem um **construtor privado** para evitar que outras classes criem instâncias dela.
- A classe Singleton fornece um **método estático** (por exemplo, `getInstance()`) para acessar a única instância.

## Como usar o Singleton?
### Implementação Básica
```java
public class Singleton {
    // Instância única da classe
    private static Singleton instance;

    // Construtor privado para evitar instanciação externa
    private Singleton() {
        // Inicializações, se necessário
    }

    // Método estático para acessar a instância única
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    // Métodos da classe
    public void doSomething() {
        System.out.println("Singleton está fazendo algo!");
    }
}
```

### Uso do Singleton
```java
public class Main {
    public static void main(String[] args) {
        // Obtém a instância única do Singleton
        Singleton singleton = Singleton.getInstance();

        // Usa a instância
        singleton.doSomething();
    }
}
```

## Variações do Singleton
### Singleton com Inicialização Preguiçosa (Lazy Initialization)
A instância é criada apenas quando necessário (no primeiro uso).
```java
public static Singleton getInstance() {
    if (instance == null) {
        instance = new Singleton();
    }
    return instance;
}
```

### Singleton com Inicialização Eager (Eager Initialization)
A instância é criada no momento em que a classe é carregada.
```java
private static final Singleton instance = new Singleton();

public static Singleton getInstance() {
    return instance;
}
```

### Singleton Thread-Safe
Garante que a instância seja criada corretamente em ambientes multithread.
#### Com `synchronized`:
```java
public static synchronized Singleton getInstance() {
    if (instance == null) {
        instance = new Singleton();
    }
    return instance;
}
```

#### Com Double-Checked Locking (mais eficiente):
```java
private static volatile Singleton instance;

public static Singleton getInstance() {
    if (instance == null) {
        synchronized (Singleton.class) {
            if (instance == null) {
                instance = new Singleton();
            }
        }
    }
    return instance;
}
```

## Singleton no Spring Boot
No Spring Boot, o padrão Singleton é implementado naturalmente pelo próprio framework. Quando você define um **bean** usando anotações como `@Component`, `@Service`, ou `@Repository`, o Spring gerencia o ciclo de vida do objeto e garante que apenas uma instância seja criada e compartilhada em todo o contexto da aplicação.

### Exemplo no Spring Boot
```java
@Service // O Spring gerencia essa classe como um Singleton
public class MyService {
    public void doSomething() {
        System.out.println("Fazendo algo no serviço!");
    }
}
```

### Uso no Controller
```java
@RestController
public class MyController {
    private final MyService myService;

    @Autowired // Injeção de dependência do Singleton
    public MyController(MyService myService) {
        this.myService = myService;
    }

    @GetMapping("/do-something")
    public String doSomething() {
        myService.doSomething();
        return "Feito!";
    }
}
```

## Vantagens do Singleton
- **Controle de instâncias**: Garante que apenas uma instância seja criada.
- **Acesso global**: Facilita o acesso a recursos compartilhados.
- **Economia de recursos**: Evita a criação desnecessária de múltiplas instâncias.

## Desvantagens do Singleton
- **Testabilidade**: Pode dificultar testes unitários, pois o estado é compartilhado globalmente.
- **Acoplamento**: Pode aumentar o acoplamento entre classes.
- **Violação do Princípio de Responsabilidade Única**: O Singleton pode acabar acumulando muitas responsabilidades.

## Quando usar o Singleton?
- Quando você precisa de uma única instância de uma classe em toda a aplicação.
- Para gerenciar recursos compartilhados, como conexões de banco de dados, caches ou configurações globais.

## Conclusão
O Singleton é um padrão poderoso, mas deve ser usado com cuidado para evitar problemas de design e manutenção. Em aplicações Spring Boot, o próprio framework já gerencia a maioria dos casos de uso do Singleton.



# Feign - Cliente HTTP Declarativo para Spring Boot

## Introdução
Feign é uma biblioteca Java que simplifica a criação de clientes HTTP em aplicações Spring Boot. Com o Feign, é possível fazer chamadas a APIs RESTful de forma declarativa, sem a necessidade de escrever código boilerplate para configurar e executar requisições HTTP manualmente.

## Principais Características

### Simplificação de Chamadas HTTP
O Feign permite definir uma interface com métodos que representam endpoints de uma API REST. Ele cuida automaticamente da implementação desses métodos, transformando-os em chamadas HTTP.

### Integração com Spring Cloud
Amplamente utilizado em projetos que empregam Spring Cloud para microservices, o Feign se integra com:
- **Eureka** - para descoberta de serviços.
- **Ribbon** - para balanceamento de carga.

### Suporte a Anotações
Utiliza anotações como `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc., tornando o código mais legível e de fácil manutenção.

### Serialização e Desserialização Automática
O Feign integra-se com bibliotecas como Jackson para converter automaticamente objetos Java em JSON e vice-versa durante chamadas HTTP.

### Tratamento de Erros
Permite a personalização do tratamento de erros (respostas 4xx ou 5xx) através da interface `ErrorDecoder`.

### Interoperabilidade com Outras Ferramentas
O Feign pode ser combinado com outras bibliotecas, como:
- **Hystrix** - para tolerância a falhas.
- **Spring Retry** - para tentativas de chamadas automáticas.

### Configuração Personalizada
Permite configurar diversos aspectos como timeouts, loggers e interceptadores para atender às necessidades do projeto.

## Exemplo de Uso

### 1. Adicionar Dependência ao `pom.xml` (Maven)
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

### 2. Habilitar Feign no Aplicativo Spring Boot
```java
@SpringBootApplication
@EnableFeignClients
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

### 3. Definir Interface para Cliente Feign
```java
@FeignClient(name = "example-client", url = "https://api.example.com")
public interface ExampleClient {
    @GetMapping("/users/{id}")
    User getUserById(@PathVariable("id") Long id);
}
```

### 4. Utilizar o Cliente Feign em um Serviço
```java
@Service
public class UserService {
    private final ExampleClient exampleClient;

    @Autowired
    public UserService(ExampleClient exampleClient) {
        this.exampleClient = exampleClient;
    }

    public User fetchUser(Long id) {
        return exampleClient.getUserById(id);
    }
}
```

## Resumo
O Feign é uma ferramenta poderosa que simplifica a comunicação HTTP em aplicações Spring Boot, especialmente em arquiteturas de microservices. Ele reduz a complexidade do código e facilita a integração com outras bibliotecas e serviços do ecossistema Spring.

