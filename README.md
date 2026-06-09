# Lunar Resource Hub

**Global Solution 2026 · FIAP · 1TWDOA · Indústria Espacial**

Protótipo navegável de um sistema web de gestão de recursos para uma colônia lunar fictícia. A interface permite monitorar energia, água, oxigênio e alimentos, acompanhar condições ambientais e receber alertas com recomendações de ação — ajudando os moradores a tomar decisões rápidas em um ambiente de alta criticidade.

---

## Problema e solução

**Problema:** Em uma colônia lunar, recursos essenciais como energia, água, oxigênio e alimentos precisam ser monitorados constantemente. Qualquer falha de gestão pode comprometer toda a operação e a segurança dos moradores.

**Solução:** O Lunar Resource Hub centraliza essas informações em um protótipo web com quatro telas especializadas, menu de navegação funcional e identidade visual unificada. Os dados são simulados, mas a lógica reflete desafios reais de cidades inteligentes, monitoramento ambiental e gestão de emergências.

---

## Navegação do protótipo

| Tela          | Arquivo              | Conteúdo principal                                                                      |
| ------------- | -------------------- | --------------------------------------------------------------------------------------- |
| Dashboard     | `index.html`         | Cards de recursos (85/72/91/63%), status bar, alertas recentes (1 crítico + 1 moderado) |
| Recursos      | `recursos.html`      | Água, energia, alimentos, estoque, resumos diários e exportação JSON                      |
| Monitoramento | `monitoramento.html` | Temperatura, umidade, qualidade do ar e nível de CO₂                                    |
| Alertas       | `alertas.html`       | Central de comando: severidade, medidores, recomendações, timeline e filtros            |

As quatro telas (`index.html`, `recursos.html`, `monitoramento.html` e `alertas.html`) compartilham header, menu, status bar sticky e footer.

---

## Dashboard (`index.html`)

Visão geral da colônia, alinhada à Central de Alertas:

- **Status bar sticky** — ATENÇÃO · 1 crítico · 1 moderado · sync UTC
- **Cards de recursos** — Energia 85%, Água 72%, Oxigênio 91%, Alimentos 63%
- **Dados do satélite** — temperatura externa -18°C, comunicação estável
- **Alertas recentes** — temperatura crítica no Módulo C e estoque de alimentos abaixo de 70%
- Link direto para a Central de Alertas

---

## Gestão de Recursos (`recursos.html`)

Controle operacional de estoque, consumo e produção, alinhado ao Dashboard e à Central de Alertas:

1. **Status bar sticky** — Colônia Alpha, ATENÇÃO, 1 crítico · 1 moderado, sync UTC
2. **Hero** — estoque de alimentos em 63% (meta 70%) com link para alerta moderado; oxigênio (91%) referenciado no Dashboard e Monitoramento
3. **Menu âncora** — navegação rápida entre Água, Energia, Alimentos, Estoque, Resumos e Utilitários
4. **Controle de Água** — formulário de consumo/produção (L) e tabelas separadas por tipo
5. **Gestão de Energia** — formulário de consumo/produção (kWh) e tabelas separadas por tipo
6. **Manipulação de Alimentos** — registro de entradas e saídas por item, quantidade e unidade
7. **Administração de Estoque** — cadastro e atualização de itens (somar quantidade se já existir)
8. **Resumos diários** — adicionar consumo/produção por data, gerar resumo e comparar consumo × produção
9. **Utilitários** — exportar dados (JSON), importar backup (com label acessível) e limpar registros (confirmação na página)

**Distribuição de recursos por tela:** água, energia e alimentos são operados em `recursos.html`; **oxigênio** é monitorado no **Dashboard** (`index.html`, card 91%) e na tela de **Monitoramento** (`monitoramento.html`), pois exige sensores ambientais e não entradas manuais de estoque.

**Interatividade (JavaScript):** persistência em `localStorage`; adicionar, apagar e resumir registros; export/import JSON; mensagens de feedback na página (sem `alert()`).

**Recursos de UX:** formulários e tabelas estilizados (`.recursos-form`, `.history-table`), placeholders com exemplos lunares, telemetria em JetBrains Mono, ícones Font Awesome, layout responsivo (breakpoint 768px) e `aria-*` no menu e feedback.

---

## Monitoramento Ambiental (`monitoramento.html`)

Tela de telemetria ambiental — temperatura, umidade, qualidade do ar, CO₂ e oxigênio por módulo, alinhada ao Dashboard e à Central de Alertas:

1. **Status bar sticky** — Colônia Alpha, ATENÇÃO, 1 crítico · 1 moderado, sync UTC
2. **Hero** — leituras dos sensores com sync 09:45 UTC; badge **Módulo C · -8°C** com link para alerta crítico
3. **Menu âncora** — Módulos, Atmosfera e Exterior
4. **Cards ambientais** — O₂ 91%, qualidade do ar, CO₂ médio (437 ppm), umidade média (49%)
5. **Leituras por módulo** — tabela A (Habitação), B (Agrícola) e C (Armazenamento) com temp., umidade e CO₂
6. **Destaque Módulo C** — medidor de temperatura (-8°C, mínimo -5°C) e link para protocolo em Alertas
7. **Atmosfera interna** — detalhamento do oxigênio e filtros (complemento ao card do Dashboard)
8. **Exterior / satélite** — temperatura externa -18°C, radiação e comunicação

**Distribuição:** oxigênio aparece no Dashboard (resumo) e aqui (telemetria detalhada); o alerta crítico de temperatura conecta esta tela à Central de Alertas.

**Interatividade:** página estática (HTML/CSS), reutilizando medidores e badges de severidade do projeto.

**Recursos de UX:** telemetria em JetBrains Mono, tabela responsiva, `aria-*` em medidores e links contextuais, layout responsivo (768px).

---

## Central de Alertas (`alertas.html`)

Fluxo operacional completo da central de alertas:

1. **Status bar sticky** — Colônia Alpha, ATENÇÃO, 1 crítico · 1 moderado, sync UTC
2. **Hero com prioridade** — alerta crítico de temperatura no Módulo C (-8°C, mínimo -5°C)
3. **Cards resumo** — críticos (1) e moderados (1), com links para as seções
4. **Alertas críticos** — medidor de temperatura, Ver protocolo, Reconhecer (toggle)
5. **Alertas moderados** — estoque de alimentos 63% com medidor e meta 70%
6. **Status operacional** — seção colapsável com tabela de 4 componentes estáveis (água, energia, O₂, comunicação)
7. **Recomendações numeradas** — 1 crítico + 3 ações (reposição alimentar, acompanhamento, preventivo)
8. **Histórico** — timeline vertical (padrão) ou tabela, com filtros por severidade e status

**Interatividade (JavaScript mínimo):** botões Reconhecer atualizam timeline/tabela; filtros e alternância Timeline/Tabela.

**Recursos de UX:** telemetria em JetBrains Mono, severidade dual (cor + forma), layout responsivo (breakpoint 768px), `aria-*`, scroll suave e `prefers-reduced-motion`.

---

## Dados simulados (cenário atual)

| Indicador              | Valor     | Alerta                |
| ---------------------- | --------- | --------------------- |
| Energia                | 85%       | Estável               |
| Água                   | 72%       | Estável               |
| Oxigênio               | 91%       | Estável               |
| Alimentos              | 63%       | Moderado (meta 70%)   |
| Módulo C (temperatura) | -8°C      | Crítico (mínimo -5°C) |
| Sync geral             | 09:45 UTC | —                     |

Os valores são consistentes entre `index.html`, `recursos.html`, `monitoramento.html` e `alertas.html`.

---

## Como executar localmente

Não é necessário instalar dependências nem rodar build. Basta clonar o repositório e abrir no navegador:

```bash
git clone https://github.com/arianaarai/fiap-global-solution.git
cd fiap-global-solution
```

Abra o arquivo `index.html` no navegador (duplo clique ou extensão Live Server no VS Code).

---

## Tecnologias

- HTML5 + CSS3 + JavaScript (Central de Alertas e Gestão de Recursos; Monitoramento estático)
- [Google Fonts](https://fonts.google.com/) — Orbitron, Poppins, Inter, JetBrains Mono (telemetria)
- [Font Awesome 6](https://fontawesome.com/) — ícones
- Dados simulados (sem backend, banco de dados ou integração com satélites)

---

## ODS — Objetivos de Desenvolvimento Sustentável

**ODS 9 — Indústria, Inovação e Infraestrutura**
O sistema representa a infraestrutura digital necessária para operar uma colônia em ambiente extremo, usando inovação tecnológica para monitorar e gerenciar recursos críticos.

**ODS 11 — Cidades e Comunidades Sustentáveis**
A solução aplica princípios de gestão sustentável de recursos e segurança comunitária — conceitos diretamente transferíveis para cidades inteligentes na Terra.

---

## Contribuição (fluxo Git)

1. Clone o repositório e crie uma branch para sua tela:

   ```bash
   git checkout -b feat/nome-da-tela
   ```

2. Faça suas alterações e commit.
3. Abra um Pull Request para a branch `main`.
4. Uma pessoa do grupo centraliza os merges.

Branches sugeridas: `feat/dashboard`, `feat/recursos`, `feat/monitoramento`, `feat/alertas`.

---

## Integrantes

| Nome                         | RM     |
| ---------------------------- | ------ |
| Ariana Cristina Arai Jesus   | 570051 |
| Gabriela di Sousa Rodrigues  | 570213 |
| Hugo D'Angelo                | 571523 |
| Larissa Sayuri Ribeiro Oyama | 573300 |

---

## Entregáveis

| Item | Link |
|------|------|
| Repositório GitHub | https://github.com/arianaarai/fiap-global-solution |
| Vídeo-pitch (2–3 min) | _A definir_ |
| PDF de entrega | _A definir_ |

---

## Créditos

FIAP · Global Solution 2026 · 1TWDOA · Indústria Espacial
