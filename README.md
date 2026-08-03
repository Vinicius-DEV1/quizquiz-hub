# 🎯 QuizQuiz

> Plataforma interativa de quizzes ao vivo com ranking em tempo real.

Plataforma onde um **host** cria e conduz quizzes ao vivo, e **participantes** entram numa sala usando um código, respondem em tempo real e veem um ranking dinâmico. Participação sem conta; criação de quizzes exige cadastro.

## Arquitetura

O projeto segue uma arquitetura **polyrepo** com 3 repositórios independentes:

```mermaid
graph TB
    subgraph Clients
        WEB[quiz-web<br>React + TypeScript]
        MOB[quiz-mobile<br>Expo + TypeScript]
    end

    subgraph Backend
        API[quiz-api<br>Node.js + Express + TypeScript]
        WS[Socket.io<br>Tempo Real]
    end

    subgraph Infra
        DB[(PostgreSQL)]
        CACHE[(Redis)]
    end

    WEB -->|REST API| API
    WEB <-->|WebSocket| WS
    MOB -->|REST API| API
    MOB <-->|WebSocket| WS
    API --> DB
    API --> CACHE
    WS --> CACHE
