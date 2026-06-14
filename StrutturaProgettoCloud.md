# Struttura progetto Sistemi Cloud

## Indice

- [Struttura progetto Sistemi Cloud](#struttura-progetto-sistemi-cloud)
  - [Indice](#indice)
  - [1. Versione base: deployment locale (un primo repo GitHub)](#1-versione-base-deployment-locale-un-primo-repo-github)
    - [Architettura applicativa](#architettura-applicativa)
    - [Persistenza dei dati](#persistenza-dei-dati)
    - [Comunicazione asincrona (opzionale)](#comunicazione-asincrona-opzionale)
    - [Containerizzazione e orchestrazione](#containerizzazione-e-orchestrazione)
    - [Infrastructure as Code](#infrastructure-as-code)
  - [2. Versione cloud: deployment su AWS](#2-versione-cloud-deployment-su-aws)
    - [Cloudificazione dell'architettura](#cloudificazione-dellarchitettura)
    - [Esempi di componenti AWS aggiuntivi](#esempi-di-componenti-aws-aggiuntivi)
    - [Alternative architetturali](#alternative-architetturali)
    - [Infrastructure as Code e CI/CD](#infrastructure-as-code-e-cicd)

## 1. Versione base: deployment locale (un primo repo GitHub)

### Architettura applicativa

- Applicazione **3-tier** basata su microservizi.
- Microservizi realizzabili, ad esempio, con:
  - Java Spring Boot;
  - Node.js;
  - Python Flask.
- Frontend libero, ad esempio:
  - Angular;
  - React;
  - Vue;
  - HTML, CSS (vanno più che bene) e JavaScript.

### Persistenza dei dati

- Database relazionale:
  - MySQL;
  - PostgreSQL.
- Database NoSQL:
  - MongoDB;
  - Redis, per casi particolari: p. es. dati molto veloci da leggere ma non destinati a essere il database principale.

### Comunicazione asincrona (opzionale)

- Code di messaggi per la comunicazione tra microservizi, ad esempio:
  - RabbitMQ;
  - Kafka.

### Containerizzazione e orchestrazione

- Containerizzazione con **Docker**.
- Orchestrazione con **Kubernetes (K8s)**.
- Primo deployment in locale su un cluster K8s reale tramite **Multipass**.

### Infrastructure as Code

- Utilizzo di **Terraform** e **Ansible** in locale per:
  - gestione dell'infrastruttura;
  - configurazione dei servizi.

## 2. Versione cloud: deployment su AWS

### Cloudificazione dell'architettura

- Migrazione dell'architettura su AWS con servizi gestiti, ad esempio:
  - **EKS** per Kubernetes;
  - **RDS** per MySQL o PostgreSQL;
  - **DynamoDB** per database NoSQL;
  - **ElastiCache** per Redis.

### Esempi di componenti AWS aggiuntivi

- **SQS**: coda messaggi serverless e cloud-native AWS; non ha un componente locale, ma una scelta alternativa quando si vuole delegare completamente ad AWS la gestione delle code.
- **Amazon MQ for RabbitMQ**: alternativa gestita AWS se si vuole usare RabbitMQ nel cloud senza gestire manualmente il broker.
- **Amazon MSK**: servizio gestito AWS per Apache Kafka, utile per streaming di eventi e comunicazione asincrona ad alto volume.
- **SNS**: per la comunicazione asincrona tra microservizi in risposta a eventi specifici.
- **Lambda**: opzionale, per l'esecuzione di funzioni serverless in risposta a eventi.

### Alternative architetturali

- Sostituzione di **EKS** con un cluster Kubernetes su istanze **EC2**, per avere maggiore controllo sull'infrastruttura.
  
  Questo potrebbe essere un progetto a sé stante su repo GH.

- Sostituzione del cluster Kubernetes cloud con un cluster di istanze EC2 in **Auto Scaling**.

Questo potrebbe essere un altro progetto a sé stante su repo GH.


### Infrastructure as Code e CI/CD

- Deployment su AWS con approccio **Infrastructure as Code (IaC)** tramite Terraform e Ansible.
- Pipeline **CI/CD** realizzata mediante **GitHub Actions**.
