<div align="center">

<img src="./assets/banner.svg" width="100%" alt="Victhor Loiola — Back-End Developer · Java & Spring Boot"/>

<a href="https://www.linkedin.com/in/victhor-loiola">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=19&duration=3000&pause=1000&color=E53935&center=true&vCenter=true&width=620&lines=Back-End+Developer+%C2%B7+Java+%26+Spring+Boot;REST+APIs+%C2%B7+Microservices+%C2%B7+RabbitMQ;Software+Engineering+%40+PUC+Minas;Open+to+internship+and+junior+roles" alt="Typing SVG"/>
</a>

<br/>

<a href="https://www.linkedin.com/in/victhor-loiola"><img src="https://img.shields.io/badge/LinkedIn-161B22?style=for-the-badge&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI0U1MzkzNSIgZD0iTTIwLjQ0NyAyMC40NTJoLTMuNTU0di01LjU2OWMwLTEuMzI4LS4wMjctMy4wMzctMS44NTItMy4wMzctMS44NTMgMC0yLjEzNiAxLjQ0NS0yLjEzNiAyLjkzOXY1LjY2N0g5LjM1MVY5aDMuNDE0djEuNTYxaC4wNDZjLjQ3Ny0uOSAxLjYzNy0xLjg1IDMuMzctMS44NSAzLjYwMSAwIDQuMjY3IDIuMzcgNC4yNjcgNS40NTV2Ni4yODZ6TTUuMzM3IDcuNDMzYTIuMDY0IDIuMDY0IDAgMSAxIDAtNC4xMjggMi4wNjQgMi4wNjQgMCAwIDEgMCA0LjEyOHptMS43ODIgMTMuMDE5SDMuNTU1VjloMy41NjR2MTEuNDUyek0yMi4yMjUgMEgxLjc3MUMuNzkyIDAgMCAuNzc0IDAgMS43Mjl2MjAuNTQyQzAgMjMuMjI3Ljc5MiAyNCAxLjc3MSAyNGgyMC40NTFDMjMuMiAyNCAyNCAyMy4yMjcgMjQgMjIuMjcxVjEuNzI5QzI0IC43NzQgMjMuMiAwIDIyLjIyMiAwaC4wMDN6Ii8%2BPC9zdmc%2B" alt="LinkedIn"/></a>
<a href="mailto:loiola_victhor@hotmail.com"><img src="https://img.shields.io/badge/Email-161B22?style=for-the-badge&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI0U1MzkzNSIgZD0iTTIgNGgyMGEyIDIgMCAwIDEgMiAydjEyYTIgMiAwIDAgMS0yIDJIMmEyIDIgMCAwIDEtMi0yVjZhMiAyIDAgMCAxIDItMnptMCAydi4zNWwxMCA2LjI1IDEwLTYuMjVWNkgyem0yMCAyLjctMTAgNi4yNUwyIDguN1YxOGgyMFY4Ljd6Ii8%2BPC9zdmc%2B" alt="Email"/></a>
<img src="https://img.shields.io/badge/Open_to_work-E53935?style=for-the-badge" alt="Open to work"/>

</div>

<br/>

<img src="./assets/divider.svg" width="100%" alt=""/>

## 01 · About me

I'm a **Software Engineering student at PUC Minas** building back-end systems with **Java** and **Spring Boot**: REST APIs, PostgreSQL databases with versioned migrations, authentication with Spring Security and communication between services with RabbitMQ. Each project documents its decisions and trade-offs, not just the code.

```java
public class Victhor implements BackEndDeveloper {

    String education  = "B.Sc. Software Engineering @ PUC Minas (2025 – 2029)";
    String currentJob = "Network Technical Support @ Brasil TecPar";

    List<String> stack = List.of("Java 21", "Spring Boot", "Spring Security",
                                 "PostgreSQL", "RabbitMQ", "Docker");

    List<String> languages = List.of("Portuguese", "English (B1)");

    @Override
    public String lookingFor() {
        return "Back-end internship or junior role · Belo Horizonte area";
    }
}
```

<img src="./assets/divider.svg" width="100%" alt=""/>

## 02 · Featured project

### [delivery-ai](https://github.com/victhor-loiola/delivery-ai)

Delivery platform built with **microservices in Java 21 and Spring Boot**. The customer creates an account, builds an order from a restaurant menu, pays and requests the delivery; an operator takes the delivery to the end. The focus is the **integration between services**.

```mermaid
%%{init: {'theme':'base','themeVariables':{'primaryColor':'#161B22','primaryTextColor':'#E6EDF3','primaryBorderColor':'#30363D','lineColor':'#E53935','textColor':'#E6EDF3','edgeLabelBackground':'#161B22','fontFamily':'JetBrains Mono, monospace'}}}%%
flowchart LR
    GW["API Gateway"]:::accent --> U["User<br/>issues JWT"]
    GW --> C["Catalog"]
    GW --> O["Order"]
    GW --> P["Payment"]
    GW --> D["Delivery"]
    O -- REST --> C
    O -- "REST + Idempotency-Key" --> P
    O -. "outbox event" .-> MQ[("RabbitMQ")]:::accent
    MQ -. "idempotent consumer" .-> D
    classDef accent fill:#E53935,stroke:#E53935,color:#FFFFFF
```

- **One database per service** — PostgreSQL + Flyway; layers `domain` → `application` → `api` → `infrastructure`
- **Transactional outbox** with publisher confirms, **idempotent consumer**, retries with backoff and **dead-letter queue**
- **Idempotent payments** with `Idempotency-Key` and **optimistic locking** with `@Version`
- **JWT RS256** issued only by the User service and validated by the others through **JWKS**
- **`X-Request-Id`** propagated through every service and RabbitMQ, with metrics on Actuator
- **JUnit 5, Mockito and Testcontainers**, running on **GitHub Actions** for every pull request

<img src="./assets/divider.svg" width="100%" alt=""/>

## 03 · Projects

| Project | About | Stack | Status |
| :-- | :-- | :-- | :-: |
| [**delivery-ai**](https://github.com/victhor-loiola/delivery-ai) | Delivery platform with microservices: orders, payments and deliveries integrated through REST and RabbitMQ events | Java 21 · Spring Boot · RabbitMQ · PostgreSQL · Docker | ![v1](https://img.shields.io/badge/release-v1-E53935?style=flat-square&labelColor=161B22) |
| [**finance-control**](https://github.com/victhor-loiola/finance-control) | Personal finance REST API: accounts, categories, income and expenses, balance per account and filtered statements. Each user only accesses their own data | Java 21 · Spring Boot · Spring Security · PostgreSQL · Flyway | ![done](https://img.shields.io/badge/status-done-E53935?style=flat-square&labelColor=161B22) |
| [**task-manager**](https://github.com/victhor-loiola/task-manager) | Terminal task manager in plain Java to practice OOP: encapsulation, enums, collections and exception handling | Java 21 | ![done](https://img.shields.io/badge/status-done-E53935?style=flat-square&labelColor=161B22) |

<img src="./assets/divider.svg" width="100%" alt=""/>

## 04 · Tech stack

<div align="center">

<img src="https://skillicons.dev/icons?i=java,spring,maven,hibernate,postgres,rabbitmq,docker,githubactions,git,github,idea,postman,linux&perline=13&theme=dark" alt="Java, Spring, Maven, Hibernate, PostgreSQL, RabbitMQ, Docker, GitHub Actions, Git, GitHub, IntelliJ IDEA, Postman, Linux"/>

<br/><br/>

![Spring Security](https://img.shields.io/badge/Spring_Security-161B22?style=for-the-badge&logo=springsecurity&logoColor=E53935)
![Flyway](https://img.shields.io/badge/Flyway-161B22?style=for-the-badge&logo=flyway&logoColor=E53935)
![JUnit 5](https://img.shields.io/badge/JUnit_5-161B22?style=for-the-badge&logo=junit5&logoColor=E53935)
![Mockito](https://img.shields.io/badge/Mockito-161B22?style=for-the-badge)
![Testcontainers](https://img.shields.io/badge/Testcontainers-161B22?style=for-the-badge&logo=testcontainers&logoColor=E53935)

</div>

<img src="./assets/divider.svg" width="100%" alt=""/>

## 05 · Training

- **Java Foundations** · Oracle
- **AWS DevOps Practices** · AWS Skill Builder

<!-- Certifications: descomente quando passar na prova
[![AWS Certified Cloud Practitioner](https://img.shields.io/badge/AWS_Certified-Cloud_Practitioner-161B22?style=for-the-badge&logo=amazonwebservices&logoColor=E53935)](LINK_DO_CREDLY)
-->

<img src="./assets/divider.svg" width="100%" alt=""/>

## 06 · GitHub activity

<div align="center">

<img height="170" src="https://streak-stats.demolab.com?user=victhor-loiola&hide_border=true&border_radius=12&background=0D1117&ring=E53935&fire=E53935&currStreakLabel=E53935&sideLabels=E6EDF3&currStreakNum=FFFFFF&sideNums=FFFFFF&dates=8B949E&stroke=30363D" alt="GitHub streak"/>

<img width="100%" src="https://raw.githubusercontent.com/victhor-loiola/victhor-loiola/output/activity-graph.svg" alt="Contribution graph"/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/victhor-loiola/victhor-loiola/output/snake-dark.svg"/>
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/victhor-loiola/victhor-loiola/output/snake-light.svg"/>
  <img width="100%" alt="Contribution snake" src="https://raw.githubusercontent.com/victhor-loiola/victhor-loiola/output/snake-dark.svg"/>
</picture>

</div>

<img src="./assets/divider.svg" width="100%" alt=""/>

<div align="center">
  <sub>Thanks for stopping by · Let's build something together</sub>
</div>
