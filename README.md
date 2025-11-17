<h1 align="center">API de Avaliação de Crédito 💳</h1>

<p align="center">
  <strong>Bootcamp TQI / DIO – Documentando uma API REST com Spring Boot e Kotlin</strong>
</p>

<p align="center">
  <a href="https://kotlinlang.org/">
    <img src="https://img.shields.io/badge/Kotlin-1.x-7F52FF?logo=kotlin&logoColor=white" alt="Kotlin">
  </a>
  <a href="https://spring.io/projects/spring-boot">
    <img src="https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot">
  </a>
  <a href="https://gradle.org/">
    <img src="https://img.shields.io/badge/Gradle-7+-02303A?logo=gradle&logoColor=white" alt="Gradle">
  </a>
  <img src="https://img.shields.io/badge/Status-Em%20desenvolvimento-yellow" alt="Status">
</p>

---

## 📌 Sobre o projeto

Este repositório contém a implementação de uma **API REST para análise de solicitações de crédito**, desenvolvida em **Kotlin** com **Spring Boot**.

O sistema simula o fluxo de uma empresa de empréstimos, permitindo:

- Cadastro e gestão de **clientes** (Customer)
- Registro e consulta de **solicitações de crédito** (Credit)
- Aplicação de **regras de negócio** para aprovação da proposta

O projeto foi desenvolvido como solução prática do desafio de projeto da DIO/TQI: **“API para Sistema de Avaliação de Créditos”**. :contentReference[oaicite:1]{index=1}  

---

## 🎯 Objetivos de aprendizado

- Criar uma **API REST** com Spring Boot e Kotlin
- Aplicar conceitos de:
  - Arquitetura em **camadas** 
  - **JPA/Hibernate** + banco de dados H2
  - **Bean Validation** (validações de entrada)
  - **DTOs** (Data Transfer Objects)
  - **Tratamento de exceções** e respostas padronizadas
- Documentar a API (ex.: Swagger/OpenAPI/Postman)

---

## 🧠 Domínio do problema

A API trabalha com dois agregados principais:

- **Customer (Cliente)**
  - Cadastro, edição, visualização e exclusão
  - Campos principais: `firstName`, `lastName`, `cpf`, `income`, `email`, `password`, `zipCode`, `street` :contentReference[oaicite:2]{index=2}  

- **Credit (Solicitação de Empréstimo)**
  - Registro de uma nova solicitação de crédito
  - Consulta de todas as solicitações de um cliente
  - Consulta detalhada de uma solicitação específica
  - Campos principais: `creditValue`, `dayFirstOfInstallment`, `numberOfInstallments`, `customerId` :contentReference[oaicite:3]{index=3}  

---

## 🏛️ Arquitetura

## 🏛 Arquitetura da Aplicação

A estrutura do projeto segue uma arquitetura organizada em camadas, utilizando os seguintes pacotes:

---

### 📁 `configuration`
Contém configurações da aplicação, como configurações de beans, Swagger/OpenAPI ou integrações específicas do projeto.

---

### 📁 `controller`
Implementa a camada **de apresentação** (API REST).  
Responsável por receber as requisições HTTP e retornar as respostas adequadas.

Principais responsabilidades:
- Expor endpoints
- Validar entradas via DTOs
- Delegar operações aos serviços

---

### 📁 `dto`
Contém os **Data Transfer Objects**, responsáveis por transportar dados entre client → controller → service.

Subpastas:
- `request` – Dados recebidos pela API
- `response` – Dados devolvidos pela API

---

### 📁 `entity`
Contém as **entidades JPA**, representando as tabelas do banco de dados.  
São modelos persistentes que representam o domínio da aplicação.

---

### 📁 `enummeration`
Contém enums utilizados pelo domínio, como status de crédito ou outros tipos de valores categóricos.

---

### 📁 `exception`
Agrupa o tratamento global de exceções da aplicação.

Inclui:
- Exceções personalizadas
- Representações estruturadas de erro
- Handler global (`RestExceptionHandler`) para padronizar respostas de erro

---

### 📁 `repository`
Implementa a camada **de acesso aos dados**.  
Contém interfaces que estendem Spring Data JPA e fazem a ponte entre as entidades e o banco.

Responsabilidades:
- Buscar, salvar, atualizar e remover entidades
- Consultas específicas via métodos derivados ou queries anotadas

---

### 📁 `service`
Representa a camada **de negócio**.  
Aqui estão as regras de negócio e lógica central do sistema.

Estrutura típica:
- Interfaces (contratos)
- Implementações (`impl/`) contendo as regras de negócio de fato

Responsabilidades:
- Validar dados antes de persistir
- Processar regras (ex.: limite de parcelas, data da primeira parcela)
- Integrar controller ↔ repository

---

## ✔ Resumo
O projeto segue uma arquitetura limpa, modular e de fácil manutenção, aplicando boas práticas comuns em aplicações Spring Boot:

- **Controller**: interface com o cliente  
- **Service**: lógica de negócio  
- **Repository**: persistência de dados  
- **Entity** + **Enummeration**: modelo de domínio  
- **DTO**: transporte de dados  
- **Exception**: tratamento global de erros  
- **Configuration**: configurações da aplicação  

---

## 🧰 Tecnologias e dependências

- **Linguagem**: Kotlin
- **Framework**: Spring Boot 3.x
- **Build**: Gradle
- **Banco de dados**: H2 (em memória)
- **ORM**: Spring Data JPA / Hibernate
- **Migração de banco**: Flyway
- **Validações**: Bean Validation (Jakarta Validation)
- **Testes** (opcional, se implementado):
  - Spring Boot Test
  - JUnit / MockK

---

## ▶️ Como executar o projeto

### ✅ Pré-requisitos

- Java 17+
- Git instalado
- IntelliJ IDEA (recomendado para Kotlin/Spring) ou outra IDE de sua preferência

### 🔽 Clonar o repositório

```bash
git clone https://github.com/bartguitar/dio-desafio-de-projeto-bootcamp-tqi-modulo8-documentando-api.git
cd dio-desafio-de-projeto-bootcamp-tqi-modulo8-documentando-api
```
# 📌 Endpoints da API

## 👤 Customer Controller  
**Base URL:** `/api/customers`

---

### ➕ Criar cliente  
**POST** `/api/customers`

#### Request Body
- firstName  
- lastName  
- cpf  
- income  
- email  
- password  
- zipCode  
- street  

#### Response (201 - Created)
- Mensagem de confirmação de criação do cliente

---

### 👁 Visualizar cliente  
**GET** `/api/customers/{id}`

#### Response Body
- Dados completos do cliente consultado

---

### ✏ Atualizar cadastro  
**PATCH** `/api/customers`

#### Request Body
- id  
- firstName  
- lastName  
- income  
- zipCode  
- street  

#### Response (200 - OK)
- Mensagem de confirmação da atualização

---

### ❌ Deletar cliente  
**DELETE** `/api/customers/{id}`

#### Response (204 - No Content)
- Sem corpo de resposta

---

## 💳 Credit Controller  
**Base URL:** `/api/credits`

---

### ➕ Registrar solicitação de crédito  
**POST** `/api/credits`

#### Request Body
- creditValue  
- dayFirstOfInstallment  
- numberOfInstallments  
- customerId  

#### Response (201 - Created)
- Mensagem de confirmação do registro do crédito

---

### 📜 Listar créditos por cliente  
**GET** `/api/credits?customerId={id}`

#### Response Body
- Lista das solicitações de crédito do cliente  
- creditCode  
- creditValue  
- numberOfInstallment  

---

### 🔍 Detalhar crédito específico  
**GET** `/api/credits/{creditCode}?customerId={id}`

#### Response Body
- creditCode  
- creditValue  
- numberOfInstallment  
- status  
- emailCustomer  
- incomeCustomer  

---

# ⚠️ Regras de Negócio

## 🔹 Limite de parcelas
- Máximo permitido: **48 parcelas**
- Caso ultrapasse: retornar erro **400 Bad Request**

---

## 🔹 Data da primeira parcela
- Deve ser dentro de **até 3 meses** a partir da data atual
- Caso ultrapasse: retornar erro **400 Bad Request**

---

# ✔️ Validações Importantes
- CPF inválido não é aceito  
- Campos obrigatórios precisam ser preenchidos  
- Valores como income e creditValue não podem ser negativos  
- numberOfInstallments deve respeitar as regras  
- Crédito deve estar associado a um cliente existente  

---

## 🧪 Testes

A aplicação inclui testes automatizados para garantir a qualidade, estabilidade e corretude do comportamento das principais funcionalidades.

Os testes estão organizados no diretório:

src/test/kotlin/me.dio.credit.application.system

### 📄 Teste existente

- `CreditApplicationSystemApplicationTests.kt`  
  - Utiliza a anotação `@SpringBootTest`
  - Executa o método `contextLoads()`
  - Responsável por validar se o *Application Context* do Spring Boot sobe com sucesso

Isso garante que:
- A aplicação está bem configurada
- Todas as dependências principais carregam normalmente
- Não há falhas de configuração no projeto

---


### 📁 Estrutura de Testes

- **controller**
  - Testes dos endpoints expostos pela API REST
  - Verificam:
    - Códigos de status
    - Corpo das respostas
    - Validações de entrada
    - Comportamento das rotas sob diferentes cenários

- **service**
  - Testes da camada de negócio
  - Validam:
    - Regras de negócio (parcelas, datas, CPF, etc.)
    - Interações com repositórios (mockados)
    - Cenários de sucesso e falha

- **repository**
  - Testes de integração com o banco H2
  - Garantem que:
    - As entidades estão mapeadas corretamente
    - Queries funcionam como esperado

---

### ▶️ Como executar os testes

Use o Gradle wrapper:

```bash
./gradlew test
```


---

# 🏁 Conclusão

Este projeto demonstra a construção de uma API REST completa utilizando **Kotlin** e **Spring Boot**, seguindo boas práticas de arquitetura, organização de camadas, uso de DTOs, validações e regras de negócio aplicadas ao domínio de análise de crédito.  

Por meio da implementação dos módulos de **Customer** e **Credit**, foi possível consolidar conceitos importantes como persistência com **JPA/Hibernate**, integração com banco de dados **H2**, criação de rotas RESTful bem definidas, tratamento centralizado de erros e uso eficiente do Gradle com Kotlin DSL.  

Além de cumprir os requisitos do desafio, o projeto fornece uma base sólida para futuras evoluções, como autenticação, migração para bancos SQL reais, deploy em containers e integração com serviços externos.  

Este repositório serve como um ótimo ponto de partida para estudos, portfólio profissional e aprofundamento no ecossistema Kotlin + Spring.  




