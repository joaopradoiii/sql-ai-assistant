# 🤖 SQL AI Assistant

Assistente inteligente em **Java** concebido para converter perguntas em linguagem natural em consultas SQL seguras para bases de dados relacionais, retornando respostas contextualizadas e amigáveis ao utilizador.

---

## 🎯 Proposta & Problema Resolvido
Em sistemas de gestão e ERPs, gestores e equipas operacionais frequentemente necessitam de extrair relatórios rápidos (ex.: volume de vendas, artigos com baixo stock, movimentações diárias), mas dependem de equipas técnicas para elaborar consultas SQL complexas.

Esta solução actua como uma camada intermediária inteligente que:
1. Recebe a intenção de negócio em linguagem natural.
2. Mapeia a estrutura relacional do banco de dados (schema DDL).
3. Gera a query SQL correspondente através de modelos de linguagem (LLM).
4. Aplica validações estritas de segurança em código antes de qualquer execução.
5. Executa a leitura dos dados e apresenta a resposta estruturada.

---

## 🛡️ Camada de Segurança (Security Guardrails)
Para evitar riscos de injecção ou perda de dados, o backend implementa directrizes de segurança rigorosas:
- **Operações estritamente Read-Only:** Apenas consultas com `SELECT` são aceites. Qualquer instrução contendo comandos como `DROP`, `DELETE`, `UPDATE`, `ALTER` ou `TRUNCATE` é bloqueada imediatamente.
- **Protecção de Metadados:** Nenhum dado sensível ou de registo real de clientes é enviado à LLM; apenas os nomes das tabelas e colunas necessárias para a elaboração do SQL são injectados no contexto.
- **Utilizador de Base de Dados Limitado:** Conexão executada sob permissões mínimas no banco de dados.

---

## 🏗️ Arquitectura da Solução

```text
[Utilizador / Aplicação]
         │ (Pergunta em linguagem natural)
         ▼
[Backend em Java] ──── (Injecção de Schema DDL) ────► [API de LLM]
         │                                                 │
         │ <───────── (SQL gerado pela LLM) ───────────────┘
         ▼
[Validador de Segurança Java] (Verificação de SELECT & Sanitização)
         │
         ├── [Bloqueado] ──► Retorna erro de segurança
         ▼
[Base de Dados Relacional] (Execução da query de leitura)
         │
         ▼
[Formatador de Resposta] ──► [Entrega do resultado amigável]

```

---

## 🛠️ Tecnologias Utilizadas
- **Linguagem:** Java (JDK 17+)
- **Conceitos:** Programação Orientada a Objetos (POO), Validação de Dados, Integração de APIs REST
- **Base de Dados:** PostgreSQL / MySQL / SQLite
- **Inteligência Artificial:** Integração via API de LLM (Google Gemini / OpenAI)
- **Versionamento:** Git & GitHub

---

## 📋 Próximos Passos do Roteiro (Roadmap)
- [x] Conceção da arquitetura de dados e modelo de segurança.
- [ ] Implementação da classe de validação léxica de queries em Java.
- [ ] Construção do conector JDBC com pooling de conexões seguras.
- [ ] Integração com endpoint da API de IA para tradução automática.
- [ ] Disponibilização de endpoint REST para consumo em painéis de gestão.
