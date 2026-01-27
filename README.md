# 📊 SentimentoAPI - Análise de Sentimento com IA e Microserviços

> **Nota de Portfólio**: Este repositório contém a documentação técnica, arquitetura e especificações de um projeto desenvolvido em grupo para o **Hackathon Oracle + Alura**. Por questões de propriedade intelectual da equipe, o código-fonte original é mantido em repositório privado, mas a solução completa está operacional e pode ser testada através do link de produção abaixo.

## 🌐 Acesso Direto (Cloud)
O projeto está hospedado em ambiente de produção na **Oracle Cloud Infrastructure (OCI)**:
👉 **URL:** [http://144.22.207.206/](http://144.22.207.206/)

---

## 💡 Sobre o Projeto
A **SentimentoAPI** é uma solução de MVP (*Minimum Viable Product*) desenvolvida para resolver o gargalo de análise de grandes volumes de feedbacks de clientes. Utilizando **Processamento de Linguagem Natural (NLP)**, o sistema classifica automaticamente comentários como Positivos ou Negativos, gerando inteligência de dados para setores de Marketing e Suporte.

## 👤 Minha Atuação Técnica
Neste projeto, foquei no desenvolvimento da camada de **Engenharia de Software e Infraestrutura**, sendo responsável por:
* **Backend Java**: Implementação da API principal utilizando **Spring Boot 3.x**.
* **Integração de Sistemas**: Desenvolvimento da comunicação via `RestTemplate` para consumo do microserviço de IA em Python.
* **Persistência**: Configuração do banco de dados **PostgreSQL** com Spring Data JPA e Hibernate.
* **DevOps & Cloud**: Orquestração de containers via **Docker Compose** e deploy em instância VM Ubuntu na **Oracle Cloud**, incluindo a configuração de firewalls (VCN/Security Lists).

---

## 🚀 Tecnologias e Ferramentas

### Backend & Integração
* **Java 21** e **Spring Boot 3.x**
* **Spring Data JPA** e **PostgreSQL**
* **Maven** (Gerenciamento de dependências)

### Inteligência Artificial (Microserviço)
* **Python 3.9** e **Flask**
* **Scikit-learn** (Modelo de Regressão Logística)
* **Joblib** (Serialização do modelo de IA)

### Infraestrutura
* **Docker** & **Docker Compose**
* **Oracle Cloud Infrastructure (OCI)**
* **Postman** (Validação de Endpoints)

---

## 🏗️ Arquitetura Técnica

O sistema utiliza uma arquitetura de microserviços para garantir escalabilidade e permitir a interoperabilidade entre as linguagens Java e Python.

 ```mermaid
graph LR
    A[Usuário/Frontend] -->|POST /sentiment| B{API Spring Boot}
    B -->|RestTemplate| C[Microserviço Python]
    C -->|Modelo .pkl| D[Inferência de IA]
    D -->|Previsão| C
    C -->|JSON| B
    B -->|Persistência| E[(PostgreSQL)]
    B -->|Resposta| A
    
    A -.->|PUT/DELETE| B
    A -.->|GET /stats| B
    

 ```

 
## 🔌 Documentação da API

### Endpoint: Classificar Sentimento

Analisa um texto e retorna a previsão do sentimento e a confiança do modelo.

* **URL:** `/sentiment`
* **Método:** `POST`
* **Content-Type:** `application/json`

#### Exemplo de Requisição (Body)

```json
{
  "text": "O produto chegou rápido e a qualidade é excelente!"
}
```

#### Exemplo de Resposta (Sucesso - 200 OK)

```json
{
  "previsao": "Positivo",
  "probabilidade": 0.92
}
```
## 🧠 Conceito Técnico: Vetorização TF-IDF
Para converter palavras em números compreensíveis pela máquina, utilizamos a técnica **TF-IDF** ($Term Frequency - Inverse Document Frequency$):
$$w_{i,j} = tf_{i,j} \times \log(\frac{N}{df_i})$$

Isso permite que o modelo ignore "stop words" (como "de", "o", "a") e foque em termos que carregam carga emocional (como "ruim", "ótimo", "amei").
