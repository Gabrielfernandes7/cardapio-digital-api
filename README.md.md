# Cardápio Digital Online

## DTO (Data Transfer Object)

No trecho de código apresentado, a função `getAll()` retorna uma lista de objetos `Food` diretamente. No entanto, essa prática não é considerada ideal, especialmente quando se trata de APIs, pois pode expor mais dados do que o necessário e tornar a comunicação menos eficiente.

### Por que usar um DTO?

Um DTO, ou Data Transfer Object, é uma classe utilizada para transferir dados entre camadas da aplicação. Ele permite que você modele os dados de uma maneira específica para atender aos requisitos de uma solicitação ou resposta da API, sem a necessidade de expor todos os detalhes da entidade original.

### Melhorando o Código

A seguir, foi introduzido um DTO chamado `FoodResponseDTO`, que é utilizado para transformar os objetos `Food` em uma representação mais adequada para serem enviados como resposta da API.

```java
@GetMapping
public List<FoodResponseDTO> getAll() {
    List<FoodResponseDTO> foodList = repository.findAll()
                                        .stream()
                                        .map(FoodResponseDTO::new)
                                        .toList();

    return foodList;
}
```

No exemplo acima, `FoodResponseDTO` é uma classe que encapsula os dados necessários para a resposta, fornecendo uma visão mais controlada e eficiente.

```java
// Exemplo de classe FoodResponseDTO como record
public record FoodResponseDTO(String nome, String descricao, BigDecimal preco) {
    // Construtor gerado automaticamente
}
```

**Observações:** A utilização de "roles" (funções) é mencionada como parte da gestão de permissões e controle de acesso ao banco de dados. Roles desempenham um papel fundamental na administração do banco de dados.

## Referências

* [DigitalOcean - How To Use Roles and Manage Grant Permissions in PostgreSQL on a VPS](https://www.digitalocean.com/community/tutorials/how-to-use-roles-and-manage-grant-permissions-in-postgresql-on-a-vps-2)
* [Hackernoon - Using Postgres Effectively in Spring Boot Applications](https://hackernoon.com/using-postgres-effectively-in-spring-boot-applications)