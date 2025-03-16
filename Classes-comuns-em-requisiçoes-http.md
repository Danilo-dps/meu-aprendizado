# Guia de Referência para HTTP em Java

## 1. RestTemplate

- Proposta: Facilita a comunicação com APIs RESTful, abstraindo a complexidade de fazer requisições HTTP manualmente.
- Funcionalidade: Permite enviar requisições HTTP (GET, POST, PUT, DELETE) e receber respostas.
- Uso comum: Integração com APIs externas, como a TheDogApi.
  - Exemplo:
    ``` java
    RestTemplate restTemplate = new RestTemplate();
    String url = "https://api.thedogapi.com/v1/breeds";
    Breed[] breeds = restTemplate.getForObject(url, Breed[].class); // Faz uma requisição GET
    ```

## 2. RequestConfig

- Proposta: Configura parâmetros de requisições HTTP, como timeouts.
- Funcionalidade: Define timeout de conexão, timeout de leitura e outras configurações.
- Uso comum: Melhora a robustez das requisições HTTP, evitando que o sistema fique travado esperando uma resposta.

    Exemplo:
     ```java
    RequestConfig config = RequestConfig.custom()
        .setConnectTimeout(5000) // Timeout de conexão: 5 segundos
        .setSocketTimeout(5000)  // Timeout de leitura: 5 segundos
        .build();
	 ```
	 
## 3. PoolingHttpClientConnectionManagerBuilder

- Proposta: Cria um gerenciador de conexões HTTP com pooling.
- Funcionalidade: Reutiliza conexões HTTP, melhorando o desempenho em cenários com muitas requisições.
- Uso comum: Aplicações que fazem muitas requisições simultâneas.

    Exemplo:
    ```java
    PoolingHttpClientConnectionManager connectionManager = PoolingHttpClientConnectionManagerBuilder.create()
        .setMaxConnTotal(100) // Número máximo de conexões
        .setMaxConnPerRoute(20) // Número máximo de conexões por rota
        .build();
    ```

## 4. CloseableHttpClient

- Proposta: Implementação de HttpClient que pode ser fechada após o uso.
- Funcionalidade: Executa requisições HTTP e gerencia conexões.
- Uso comum: Requisições HTTP personalizadas com configurações específicas.

    Exemplo:
    ```java  
    CloseableHttpClient httpClient = HttpClients.custom()
        .setConnectionManager(connectionManager)
        .build();
 	    ```

## 5. HttpComponentsClientHttpRequestFactory

- Proposta: Integra o Apache HttpClient com o RestTemplate.
- Funcionalidade: Permite usar o RestTemplate com configurações personalizadas do Apache HttpClient.
- Uso comum: Quando você precisa de configurações avançadas, como pooling de conexões.

  Exemplo:
  ```java
    HttpComponentsClientHttpRequestFactory factory = new HttpComponentsClientHttpRequestFactory(httpClient);
    RestTemplate restTemplate = new RestTemplate(factory); 
  ```

## 6. Logger

- Proposta: Registra logs (mensagens de depuração, erro, etc.).
- Funcionalidade: Ajuda a monitorar e depurar o comportamento da aplicação.
- Uso comum: Logs de requisições, respostas e erros.

    Exemplo:
    ```java 
    Logger logger = LoggerFactory.getLogger(MyClass.class);
    logger.info("Requisição enviada para a API.");
    ```

## 7. ResponseEntity

- Proposta: Representa a resposta HTTP completa (status, cabeçalhos e corpo).
- Funcionalidade: Usada para manipular respostas de APIs externas ou retornar respostas personalizadas.
- Uso comum: Controladores REST ou manipulação de respostas de APIs.

    Exemplo:
    ```java
    ResponseEntity<Breed[]> response = restTemplate.getForEntity(url, Breed[].class);
    Breed[] breeds = response.getBody(); // Corpo da resposta
    int statusCode = response.getStatusCodeValue(); // Status HTTP

## 8. HttpClient

- Proposta: Interface para fazer requisições HTTP.
- Funcionalidade: Similar ao RestTemplate, mas com mais controle sobre as requisições.
- Uso comum: Requisições HTTP personalizadas.

    Exemplo:
    ```java
    HttpClient httpClient = HttpClients.createDefault();
    ```

## 9. HttpResponse

- Proposta: Representa a resposta HTTP recebida de uma requisição.
- Funcionalidade: Permite acessar o status, cabeçalhos e corpo da resposta.
- Uso comum: Manipulação de respostas HTTP.

    Exemplo:
    ```java   
    HttpResponse response = httpClient.execute(request);
    String responseBody = EntityUtils.toString(response.getEntity()); // Corpo da resposta
    ```
    
## 10. Breed

- Proposta: Modelo de dados para representar uma raça de cachorro.
- Funcionalidade: Desserializa o JSON da resposta da API em objetos Java.
- Uso comum: Representação de dados retornados pela API.

    Exemplo:
    ```java
    public class Breed {
        private String id;
        private String name;
        // getters e setters
    }
    ```

## 11. HttpClientErrorException

- Proposta: Exceção lançada quando ocorre um erro HTTP (como 4xx).
- Funcionalidade: Tratamento de erros de requisições HTTP.
- Uso comum: Captura de erros em requisições.

    Exemplo:
    ```java
    try {
        restTemplate.getForObject(url, Breed[].class);
    } catch (HttpClientErrorException e) {
        logger.error("Erro na requisição: " + e.getStatusCode());
    }
    ```

## 12. ObjectMapper

- Proposta: Converte objetos Java em JSON e vice-versa.
- Funcionalidade: Desserializa o JSON da resposta da API em objetos Java.
- Uso comum: Manipulação de JSON.

    Exemplo:
    ```java
    ObjectMapper mapper = new ObjectMapper();
    Breed breed = mapper.readValue(jsonResponse, Breed.class);
    ```
    
## 13. JsonNode

- Proposta: Representa um nó em uma árvore JSON.
- Funcionalidade: Manipulação dinâmica de JSON.
- Uso comum: Quando você não tem um modelo de dados fixo.

    Exemplo:
    ```java
    JsonNode rootNode = mapper.readTree(jsonResponse);
    String breedName = rootNode.get("name").asText();
    ```

## 14. HttpMethod

- Proposta: Enum que representa métodos HTTP (GET, POST, PUT, DELETE).
- Funcionalidade: Define o método HTTP em requisições.
- Uso comum: Requisições HTTP personalizadas.

    Exemplo:
    ```java
    HttpMethod method = HttpMethod.GET;
    ```

## 15. Image

- Proposta: Modelo de dados para representar uma imagem.
- Funcionalidade: Desserializa informações de imagens retornadas pela API.
- Uso comum: Representação de dados de imagens.

    Exemplo:
    ```java
    public class Image {
        private String url;
        // getters e setters
    }
    ```

## 16. Collections

- Proposta: Classe utilitária para manipular coleções.
- Funcionalidade: Ordenação, busca e transformação de coleções.
- Uso comum: Manipulação de listas, conjuntos e mapas.

    Exemplo:
    ```java
    List<Breed> breedsList = Arrays.asList(breeds);
    Collections.sort(breedsList, Comparator.comparing(Breed::getName));
    ```
    
