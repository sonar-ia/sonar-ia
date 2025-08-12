
# 🧪 Guia de Boas Práticas Git – Time Labs | Sonar

Este documento define o padrão oficial de nomenclatura, organização de branches e commits para todos os repositórios do time **Labs** da Sonar. O objetivo é garantir legibilidade, escalabilidade e rastreabilidade nos projetos.

---

## 🗂️ Convenção de Nomes para Repositórios

### 📐 Formato Geral

Existem dois padrões principais de nomenclatura, definidos pela natureza do projeto:

### 1. Projetos com estrutura modular (ex: sistemas internos da Sonar)

```
<nome-do-projeto>.<tipo>_<submodulo>
```

**Exemplos:**
- `portal.agente_alvorada`
- `portal.agente_sofia`
- `portal.api_auth`

### 2. Projetos isolados, dedicados a clientes (ex: projetos de BI ou integrações)

```
<cliente>.<tipo>_<nome-do-projeto>
```

**Exemplos:**
- `terraverde.bi_csc`
- `alvorada.bi_compras`
- `sonar.internal_bot`

### 🔍 Como interpretar:

| Elemento         | Significado                                       | Exemplo                          |
|------------------|---------------------------------------------------|----------------------------------|
| `portal`         | Projeto principal / sistema base                 | `portal.agente_sofia`            |
| `terraverde`     | Nome do cliente                                  | `terraverde.bi_csc`              |
| `agente`, `bi`   | Tipo do projeto ou módulo                        | `agente`, `bi`, `api`, `bot`     |
| `sofia`, `csc`   | Submódulo, divisão ou contexto do projeto        | `agente_sofia`, `bi_csc`         |

### 🧠 Regra de Ouro

> Se o projeto pertence a um sistema da Sonar → comece pelo nome do sistema (ex: `portal.agente_*`)  
> Se o projeto é um cliente isolado → comece pelo nome do cliente (ex: `terraverde.bi_*`)

---

## 🌱 Convenção de Nomes de Branches

As branches devem seguir o seguinte padrão:

```
<tipo>/<cliente>.<nome-do-projeto>-<descricao-curta>
```

### Tipos permitidos:

| Prefixo        | Uso                                                                |
|----------------|---------------------------------------------------------------------|
| `feature/`     | Nova funcionalidade                                                 |
| `fix/`         | Correção de bug                                                     |
| `perf/`        | Otimização de performance                                           |
| `refactor/`    | Refatoração de código (sem alteração de comportamento)             |
| `style/`       | Ajustes visuais/sintáticos (ex: indentação, renomeação)            |
| `docs/`        | Atualização ou criação de documentação                             |
| `test/`        | Adição ou correção de testes                                        |
| `improvement/` | Melhoria incremental (layout, legibilidade, performance leve)       |
| `hotfix/`      | Correções urgentes e críticas em produção                           |
| `release/`     | Preparação de uma nova versão                                       |
| `chore/`       | Tarefas técnicas ou de manutenção (CI, dependências, configs)       |

### Exemplos:

- `feature/terraverde.csc-exportar-relatorio-xlsx`
- `fix/sonar.sofia-corrige-resposta-vazia`
- `improvement/portal.agente-otimiza-tempo-carregamento`
- `docs/sonar.guia-padroes-equipe`

---

## ✅ Commits Semânticos

Todos os commits devem seguir o padrão abaixo:

```
<tipo>: <descrição curta>
```

### Tipos aceitos:

| Tipo          | Descrição                                      |
|---------------|-------------------------------------------------|
| `feat`        | Nova funcionalidade                             |
| `fix`         | Correção de bug                                 |
| `perf`        | Melhoria de performance                         |
| `refactor`    | Refatoração sem alteração funcional             |
| `style`       | Ajuste de sintaxe/estilo (sem alterar lógica)  |
| `docs`        | Atualizações de documentação                    |
| `test`        | Criação ou melhoria de testes                   |
| `improvement` | Melhoria em algo existente                      |
| `chore`       | Atividades técnicas / infraestrutura            |

| Tipo              | Uso no Contexto de BI                           |
|-------------------|-------------------------------------------------|
| `feat/bi-`        | Para a criação de novas funcionalidades de BI, como criação de dashboards, relatórios, gráficos (ex: feature/bi-criar-dashboard-financeiro). |
| `fix/bi-`         | Para correção de problemas específicos de BI, como ajustes em relatórios, gráficos ou visualizações (ex: fix/bi-ajustar-grafico-vendas).     |
| `perf/bi-`        | Para otimização de performance de dashboards, consultas SQL, ou visualizações de dados (ex: perf/bi-otimizar-relatorio-vendas).              |
| `refactor/bi-`    | Para refatoração de código de BI, como melhorar a estrutura de relatórios ou consultas sem mudar o comportamento (ex: refactor/bi-refatorar-consulta-relatorio). |
| `style/bi-`       | Para ajustes visuais ou sintáticos em dashboards, relatórios, gráficos (ex: style/bi-ajustar-estilo-grafico)  |
| `docs/bi-`        | Para atualizar ou criar documentação de BI, como explicação sobre como usar o dashboard ou interpretar relatórios (ex: docs/bi-atualizar-documentacao-dashboard).|
| `test/bi-`        | Para adição ou correção de testes de BI (ex: test/bi-criar-teste-dashboard).  |
| `improvement/bi-` | Para melhorias incrementais em relatórios, visualizações de dados ou performance de BI (ex: improvement/bi-melhorar-desempenho-dashboard).|
| `chore/bi-`       | Para tarefas técnicas, como atualização de dependências de ferramentas de BI (ex: chore/bi-atualizar-dependencias-bi).        |


### Exemplos de commits:

- `feat: adiciona suporte a múltiplos usuários no dashboard`
- `fix: corrige erro 401 na autenticação via token`
- `refactor: simplifica lógica de verificação de CPF`
- `improvement: melhora legibilidade do serviço de cache`

---

## 🔁 Fluxo de Pull Request (PR)

### Regras:

- Toda alteração relevante deve passar por PR
- Nunca fazer `push` direto na `main`
- Usar *Squash and merge* sempre que possível
- PRs devem conter:
  - Título claro (sem emojis)
  - Descrição da tarefa
  - Evidências (prints, logs, link para tarefa)

### Recomendação:

```bash
git checkout -b feature/cliente.projeto-minha-descricao
git add .
git commit -m "feat: descrição clara e objetiva"
git push origin feature/cliente.projeto-minha-descricao
```

---

## 🏷️ Versionamento com Tags

Utilizar o padrão SemVer (Semantic Versioning):

```
v<MAJOR>.<MINOR>.<PATCH>
```

| Tipo  | Quando usar                    |
|-------|--------------------------------|
| MAJOR | Quebra de compatibilidade      |
| MINOR | Nova funcionalidade sem quebra |
| PATCH | Correções e melhorias pequenas |

**Exemplo:**

```bash
git tag -a v1.2.0 -m "Release da versão 1.2.0"
git push origin v1.2.0
```

---

## 🧾 Estrutura Recomendada de Diretórios

```
/docs              → Documentação
/src               → Código-fonte
/tests             → Testes automatizados
/.github           → Workflows de CI/CD
.env.example       → Modelo de variáveis de ambiente
README.md          → Guia e instruções do projeto
CHANGELOG.md       → Histórico de versões
```

---

## 🔐 Segurança

- Nunca subir `.env`, senhas ou tokens no repositório
- Garantir que `.env` esteja no `.gitignore`
- Utilizar ferramentas como GitGuardian para validação
- Usar variáveis de ambiente nos repositórios com GitHub Actions ou Azure Pipelines

---

## 🧪 Dúvidas ou sugestões?

Esse padrão é mantido pelo time de engenharia da Sonar Labs.
Contribuições são bem-vindas via PR na documentação interna ou contato direto no canal #time-labs.
