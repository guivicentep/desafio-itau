# API de Transações

Uma API REST desenvolvida em Spring Boot para gerenciamento e análise de transações financeiras em tempo real.

## 📋 Descrição

Esta API permite adicionar transações financeiras e calcular estatísticas em tempo real, incluindo contagem, soma, média, valor mínimo e máximo das transações dentro de um intervalo de tempo configurável.

## 🚀 Tecnologias Utilizadas

- **Java 24**
- **Spring Boot 3.5.4**
- **Spring Web**
- **Spring Actuator**
- **SpringDoc OpenAPI 3** (Swagger)
- **Lombok**
- **Gradle**

## 📁 Estrutura do Projeto

```
src/main/java/com/gvp/transacao_api/
├── business/
│   └── services/
│       ├── EstatisticasService.java
│       └── TransacaoService.java
├── controller/
│   ├── dtos/
│   │   ├── EstatisticasResponseDTO.java
│   │   └── TransacaoRequestDTO.java
│   ├── EstatisticasController.java
│   └── TransacaoController.java
├── infrastructure/
│   └── exceptions/
│       └── UnprocessableEntity.java
└── TransacaoApiApplication.java
```

## 🔧 Configuração e Execução

### Pré-requisitos

- Java 24 ou superior
- Gradle

### Executando o Projeto

1. **Clone o repositório:**
   ```bash
   git clone <url-do-repositorio>
   cd transacao-api
   ```

2. **Execute o projeto:**
   ```bash
   ./gradlew bootRun
   ```

3. **Ou construa e execute:**
   ```bash
   ./gradlew build
   java -jar build/libs/transacao-api-0.0.1-SNAPSHOT.jar
   ```

O aplicativo estará disponível em: `http://localhost:8080`

## 📚 Documentação da API

A documentação interativa da API está disponível através do Swagger UI:

- **Swagger UI:** `http://localhost:8080/swagger-ui.html`
- **OpenAPI JSON:** `http://localhost:8080/v3/api-docs`

## 🔌 Endpoints

### 1. Adicionar Transação

**POST** `/transacao`

Adiciona uma nova transação ao sistema.

**Request Body:**
```json
{
  "valor": 100.50,
  "dataHora": "2024-01-15T10:30:00Z"
}
```

**Respostas:**
- `201` - Transação criada com sucesso
- `422` - Dados inválidos (valor negativo ou data futura)
- `400` - Erro na requisição
- `500` - Erro interno do servidor

### 2. Deletar Transações

**DELETE** `/transacao`

Remove todas as transações do sistema.

**Respostas:**
- `200` - Transações deletadas com sucesso
- `400` - Erro na requisição
- `500` - Erro interno do servidor

### 3. Buscar Estatísticas

**GET** `/estatistica?intervaloBusca=60`

Retorna estatísticas das transações dentro do intervalo especificado (em segundos).

**Parâmetros:**
- `intervaloBusca` (opcional): Intervalo em segundos (padrão: 60)

**Response Body:**
```json
{
  "count": 5,
  "sum": 500.00,
  "avg": 100.00,
  "min": 50.00,
  "max": 150.00
}
```

**Respostas:**
- `200` - Estatísticas retornadas com sucesso
- `400` - Erro na busca
- `500` - Erro interno do servidor

## 🔍 Funcionalidades

### Validações de Transação

- **Valor:** Deve ser maior ou igual a zero
- **Data/Hora:** Não pode ser uma data futura
- **Formato:** Utiliza `OffsetDateTime` para suporte a timezone

### Estatísticas em Tempo Real

- **Contagem:** Número total de transações no intervalo
- **Soma:** Valor total das transações
- **Média:** Valor médio das transações
- **Mínimo:** Menor valor das transações
- **Máximo:** Maior valor das transações

### Armazenamento

- As transações são armazenadas em memória (ArrayList)
- Não há persistência em banco de dados
- Transações são filtradas por tempo para estatísticas

## 🛠️ Desenvolvimento

### Executar Testes

```bash
./gradlew test
```

### Construir JAR

```bash
./gradlew build
```

### Executar com Perfil de Desenvolvimento

```bash
./gradlew bootRun --args='--spring.profiles.active=dev'
```

## 📊 Monitoramento

A API inclui Spring Actuator para monitoramento:

- **Health Check:** `http://localhost:8080/actuator/health`
- **Info:** `http://localhost:8080/actuator/info`
- **Metrics:** `http://localhost:8080/actuator/metrics`

## 🔒 Tratamento de Erros

A API implementa tratamento de erros personalizado:

- **UnprocessableEntity (422):** Para dados inválidos
- **Logging:** Todas as operações são logadas
- **Respostas padronizadas:** Mensagens claras de erro

## 🚀 Deploy

### Docker (Recomendado)

```dockerfile
FROM openjdk:24-jdk-slim
COPY build/libs/transacao-api-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

### Executar com Docker

```bash
docker build -t transacao-api .
docker run -p 8080:8080 transacao-api
```

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 👨‍💻 Autor

Desenvolvido por GVP

---

**Versão:** 0.0.1-SNAPSHOT  
**Última atualização:** Janeiro 2024 