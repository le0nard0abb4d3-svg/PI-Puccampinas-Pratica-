# Estudo de Projetos Open Source no GitHub

**Projeto Integrador – Sistemas Web – PUC Campinas**
Dados coletados diretamente da API do GitHub em **30 de agosto de 2026**.

Projetos analisados: **Voicebox**, **Flowise**, **OpenMontage**, **Docsify** e **DeerFlow**.

---

## 1. Quadro comparativo

| Projeto | Repositório | Criado em | ⭐ Estrelas | 🍴 Forks | Issues abertas | Licença | Linguagem principal | Situação (30/08/2026) |
|---|---|---|---|---|---|---|---|---|
| **DeerFlow** | `bytedance/deer-flow` | 07/05/2025 | 81.128 | 11.176 | 901 | MIT | Python | Ativo (push em 30/08/2026) |
| **Flowise** | `FlowiseAI/Flowise` | 31/03/2023 | 55.398 | 24.966 | 1.046 | Apache-2.0 + Licença Comercial | TypeScript | **Arquivado** em 13/08/2026 |
| **OpenMontage** | `calesthio/OpenMontage` | 29/03/2026 | 54.430 | 6.751 | 267 | AGPL-3.0 | Python | Ativo (push em 22/08/2026) |
| **Voicebox** | `jamiepine/voicebox` | 25/01/2026 | 51.862 | 6.455 | 665 | MIT | TypeScript | Ativo (push em 09/08/2026) |
| **Docsify** | `docsifyjs/docsify` | 20/11/2016 | 31.491 | 5.797 | 93 | MIT | JavaScript | Ativo (push em 28/08/2026) |

### Leitura rápida dos números

- **Popularidade não é sinônimo de saúde.** O Flowise é o segundo mais estrelado da lista e mesmo assim foi arquivado. Estrelas medem atenção, não manutenção.
- **Velocidade de adoção.** OpenMontage e Voicebox passaram de 50 mil estrelas em **menos de 8 meses de existência**; o Docsify levou quase 10 anos para chegar a 31 mil. São ritmos de comunidade completamente diferentes.
- **Razão forks/estrelas.** No Flowise é de ~45% (24.966/55.398), muito acima dos ~13% do Voicebox e do OpenMontage. Isso indica um público que **clona para hospedar e customizar**, não apenas para contribuir — típico de ferramenta auto-hospedada em empresa.
- **Issues abertas por estrela** é um indicador de dívida de suporte: Flowise (1,9%) e Voicebox (1,3%) acumulam mais do que o Docsify (0,3%), que é um projeto maduro e com escopo estável.

---

## 2. Análise individual

### 2.1 Voicebox — `jamiepine/voicebox`

> "The open-source AI voice studio. Clone, dictate, create."

**O que é.** Um estúdio de voz por IA que roda **localmente**, posicionado como alternativa gratuita ao ElevenLabs (saída de voz) e ao Wispr Flow (ditado). Faz clonagem de voz *zero-shot* a partir de poucos segundos de áudio, síntese de fala (TTS) em 23 idiomas com 7 motores diferentes, transcrição com Whisper, ditado global por atalho de teclado, efeitos de áudio e um editor multipista.

**Arquitetura e stack.**
- Desktop em **Tauri (Rust)** com interface em **React + TypeScript**
- Backend em **Python/FastAPI**
- Motores TTS: Qwen3-TTS, LuxTTS, Chatterbox, HumeAI TADA, Kokoro
- Inferência via **MLX** (Apple Silicon) ou **PyTorch** (CUDA/ROCm/XPU)
- Persistência em **SQLite**
- Expõe **API REST + servidor MCP** (Model Context Protocol), permitindo que agentes como Claude Code e Cursor "falem" com uma voz clonada

**Pontos de destaque.** É um caso claro de arquitetura **local-first**: o argumento de venda é privacidade — áudio e modelos nunca saem da máquina. O uso de Tauri em vez de Electron reduz drasticamente o tamanho do binário. O mantenedor é Jamie Pine, também criador do Spacedrive, o que explica a escolha de stack (Rust + Tauri) e parte da tração inicial.

**Riscos e ressalvas.**
- **Bus factor baixo**: repositório sob conta pessoal, sem organização por trás.
- 665 issues abertas para um projeto de 7 meses sugere que o suporte não acompanha o crescimento.
- **Questão ética relevante**: clonagem de voz sem trava de consentimento é um vetor de *deepfake* de áudio. Vale como discussão em sala sobre responsabilidade de quem publica software.

---

### 2.2 Flowise — `FlowiseAI/Flowise`

> "Build AI Agents, Visually" — **projeto arquivado em 13/08/2026**

**O que era.** Uma plataforma *low-code/no-code* para montar agentes de IA e fluxos de RAG arrastando nós numa tela, sobre LangChain. Gerava automaticamente API e documentação para cada fluxo publicado.

**Arquitetura e stack.**
- Monorepo **PNPM** com três módulos: `server` (Node.js), `ui` (React + Vite) e `components` (nós integráveis)
- Instalação em um comando: `npm install -g flowise && npx flowise start`
- Suporte a Docker/docker-compose

**O caso mais instrutivo da lista.** O repositório foi movido para *Public Archive*: código permanece visível, mas **issues e PRs foram travados** e os pacotes npm e imagens Docker marcados como *deprecated*. A justificativa oficial ("The Future of Flowise") é que, com modelos de IA cada vez mais capazes de raciocinar, os desenvolvedores migraram para agentes de código (Claude Code e similares), e a abordagem de **fluxo rígido em low-code esbarra num teto de complexidade**. A equipe encerrou a operação e também sua presença no Discord e no GitHub.

**Licenciamento — atenção.** O README diz Apache-2.0, mas o GitHub classifica a licença como *Other* (`NOASSERTION`). O motivo é um modelo **de licença dupla**: o diretório `packages/server/src/enterprise` e arquivos específicos (ex.: `IdentityManager.ts`) estão sob **Licença Comercial**, não Apache. Ou seja, "open source" aqui é parcial — um exemplo prático de *open core*.

**Lições.**
1. Um projeto pode ter 55 mil estrelas e ainda assim ser descontinuado — **sustentabilidade financeira e relevância técnica** contam mais que popularidade.
2. Como o código é Apache-2.0 (fora do módulo enterprise), a comunidade pode **fazer fork e continuar**. Isso é exatamente o que a licença permissiva protege.
3. Sempre leia o arquivo `LICENSE` real, não só o badge do README.

---

### 2.3 OpenMontage — `calesthio/OpenMontage`

> "World's first open-source, agentic video production system."

**O que é.** Um sistema de produção de vídeo dirigido por agentes: o usuário descreve o que quer em linguagem natural e um assistente de código com IA executa pesquisa, roteiro, geração de assets, edição e composição. São 12 pipelines de produção (explicativo, documentário, *talking head*, trailer, animação, reaproveitamento de podcast), 100+ ferramentas e 700+ arquivos de "skill".

**Arquitetura — o ponto mais interessante academicamente.** O projeto organiza conhecimento em **três camadas**:
1. Ferramentas executáveis + manifestos de pipeline em **YAML**
2. Arquivos **Markdown** de *skills*, que ensinam ao agente as convenções de cada etapa
3. Pacotes de conhecimento externo sobre as tecnologias usadas

O fluxo é `pesquisa → proposta → roteiro → plano de cenas → assets → edição → composição`, e a escolha de provedor é feita por **pontuação em 7 dimensões** (adequação à tarefa, qualidade, controle, confiabilidade, custo, latência, continuidade). Isso mostra um padrão emergente: **o "código" do agente é documentação estruturada**, não apenas funções.

**Stack.** Python 3.10+ (orquestração), Node.js 18+, **Remotion** (composições em React), HyperFrames (HTML/CSS/GSAP para motion graphics), **FFmpeg** (montagem/encode) e **Piper TTS** local. Funciona sem nenhuma chave de API usando ferramentas gratuitas (Archive.org, NASA, Wikimedia Commons); chaves opcionais liberam Kling, FLUX, Google Veo, Runway, ElevenLabs e Suno.

**Licença — AGPL-3.0.** É o item mais restritivo da lista: *copyleft* forte com cláusula de rede. Quem oferecer o sistema como serviço via rede é obrigado a disponibilizar o código-fonte modificado. É uma escolha deliberada contra apropriação comercial fechada — o oposto da estratégia MIT do Voicebox e do DeerFlow.

**Riscos.** Repositório de mantenedor individual, com 5 meses de vida e 54 mil estrelas — crescimento explosivo que ainda não foi testado no tempo. Depende de muitos serviços externos pagos para os recursos mais chamativos.

---

### 2.4 Docsify — `docsifyjs/docsify`

> "🃏 A magical documentation site generator."

**O que é.** Um gerador de sites de documentação que **não gera arquivos HTML estáticos**. Em vez de compilar Markdown em páginas durante um *build*, o Docsify carrega os `.md` e os renderiza no navegador em tempo de execução, como uma SPA.

**Como funciona na prática.** Bastam três arquivos numa pasta `docs/`:

| Arquivo | Função |
|---|---|
| `index.html` | Carrega o docsify por CDN e define `window.$docsify` |
| `README.md` | É a página inicial |
| `.nojekyll` | Impede o GitHub Pages de ignorar arquivos iniciados com `_` |

Servir localmente: `docsify serve docs` (via docsify-cli) ou, sem instalar nada, `python -m http.server 3000`. Distribuído por UNPKG, jsDelivr e cdnjs. Recursos: busca *full-text*, temas, sistema de plugins e suporte a emoji.

**Por que é o mais relevante para este PI.** É o projeto tecnicamente mais simples e o mais diretamente aplicável ao curso: HTML + um `<script>` de CDN + Markdown, publicável em GitHub Pages sem *build*, sem Node, sem pipeline. Serve para documentar os próprios exercícios da disciplina.

**Trade-offs honestos.**
- ✅ Zero build, atualização instantânea, hospedagem gratuita
- ❌ Renderização no cliente prejudica **SEO** e a indexação por buscadores (ponto direto de contraste com o conteúdo de SEO semântico visto no Exercício 02)
- ❌ Exige JavaScript habilitado; sem ele a página fica em branco
- ⚠️ Fixar a versão no CDN (`@5.0.0`) em vez de `@5` evita quebras inesperadas

**Saúde do projeto.** É o mais maduro do conjunto: quase 10 anos, mantido por uma **organização** (`docsifyjs`) e não por um indivíduo, e com apenas 93 issues abertas — sinal de escopo bem delimitado e triagem eficiente. Branch padrão `develop`, o que indica um fluxo de trabalho com separação entre desenvolvimento e release.

---

### 2.5 DeerFlow — `bytedance/deer-flow`

> "An open-source long-horizon SuperAgent harness that researches, codes, and creates."

**O que é.** Originalmente um framework de *deep research* (DeerFlow = *Deep Exploration and Efficient Research Flow*), lançado pela ByteDance em maio de 2025 e reescrito na versão **2.0** (março de 2026) como um "SuperAgent harness" — uma infraestrutura completa para agentes autônomos que executam tarefas de minutos a horas.

**Arquitetura.**
- **Lead Agent** que planeja e delega, e **sub-agentes** paralelos com contexto e ferramentas isolados
- Orquestração em grafo dirigido com **LangGraph/LangChain**, com *checkpointing* e gestão de estado
- **Sandbox** em três modos de isolamento: local, Docker ou Kubernetes
- **Camada de memória** de longo prazo com sumarização automática
- **Skills em Markdown**, carregadas progressivamente conforme a tarefa exige (mesmo padrão do OpenMontage)

**Stack.** Python 3.12+ no backend; **Next.js/React** com Node.js 22+ no frontend; nginx como proxy reverso; SQLite (local) ou **PostgreSQL** (produção); Docker Compose; Playwright para automação de navegador. Instalação por assistente: `make setup` → `make dev` (ou `make docker-start`). Produção pede **8–16 vCPU e 16–32 GB de RAM** — de longe o mais pesado da lista.

**Integrações.** Vários provedores de LLM (OpenAI, Anthropic, DeepSeek, Qwen, Gemini via OpenRouter, ou modelos locais via vLLM), busca web (Tavily/InfoQuest), observabilidade (LangSmith, Langfuse) e canais de mensagem (Telegram, Slack, Feishu, WeChat, DingTalk).

**Governança.** É o único projeto da lista mantido por uma **big tech** (ByteDance), sob licença **MIT**. Chegou ao #1 do GitHub Trending em fevereiro de 2026 e é hoje o mais estrelado do conjunto (81 mil). Respaldo corporativo reduz o risco de abandono súbito, mas introduz outro: a direção do projeto segue o interesse estratégico da empresa, não o da comunidade.

---

## 3. Análise transversal

### 3.1 Licenças: três estratégias distintas

| Estratégia | Projetos | Efeito prático |
|---|---|---|
| **Permissiva (MIT)** | Voicebox, Docsify, DeerFlow | Qualquer um pode usar, modificar e fechar o código derivado. Maximiza adoção. |
| **Copyleft forte (AGPL-3.0)** | OpenMontage | Quem oferece como serviço em rede deve abrir o código modificado. Protege contra apropriação por SaaS. |
| **Open core (Apache-2.0 + Comercial)** | Flowise | Núcleo aberto, módulo enterprise proprietário. Tenta financiar o desenvolvimento — e ainda assim não sustentou o projeto. |

**Conclusão:** a licença é uma decisão de *modelo de negócio e de comunidade*, não um detalhe jurídico. Antes de usar qualquer projeto em trabalho acadêmico ou profissional, verifique o arquivo `LICENSE` — o Flowise mostra que README e licença real podem divergir.

### 3.2 Modelos de governança e risco

| Modelo | Projetos | Risco principal |
|---|---|---|
| Mantenedor individual | Voicebox, OpenMontage | *Bus factor* = 1; se a pessoa parar, o projeto para |
| Organização comunitária | Docsify | Ritmo mais lento, porém estável e previsível |
| Empresa (startup) | Flowise | Depende de captação; **já descontinuado** |
| Empresa (big tech) | DeerFlow | Direção definida por interesse corporativo |

### 3.3 A tendência de 2026: "skills em Markdown"

OpenMontage e DeerFlow, criados de forma independente, convergiram para o mesmo padrão arquitetural: **capacidades do agente descritas em arquivos Markdown carregados sob demanda**, em vez de codificadas em funções. É a virada que o próprio anúncio de encerramento do Flowise descreve — do fluxo visual rígido para o agente que lê instruções em texto. Para quem estuda desenvolvimento web hoje, isso significa que *escrever documentação clara e estruturada virou uma competência de programação*.

### 3.4 Escala de complexidade

```
Docsify          → 3 arquivos, sem build, roda em GitHub Pages
Voicebox         → app desktop, 3 linguagens (Rust + TS + Python)
Flowise          → monorepo PNPM, 3 pacotes, Docker
OpenMontage      → Python + Node + FFmpeg + 60 provedores externos
DeerFlow         → microsserviços, sandbox K8s, 8–16 vCPU em produção
```

---

## 4. Conclusões e aplicação ao Projeto Integrador

1. **Adote o Docsify.** É o único da lista aplicável de imediato ao PI: documenta os exercícios da disciplina com HTML + Markdown, publica no GitHub Pages sem custo e sem *build*. Reforça na prática o conteúdo de estrutura semântica visto em aula.
2. **Use o Flowise como estudo de caso.** É a melhor lição da lista: um projeto pode ter enorme sucesso de público e ainda ser encerrado. Ao escolher uma dependência, avalie *data do último commit, licença real, número de mantenedores e modelo de sustentação* — não a contagem de estrelas.
3. **Cuidado com a métrica de estrelas.** Voicebox e OpenMontage cresceram mais rápido que qualquer projeto maduro da lista, mas têm menos de um ano de existência e um único mantenedor. Adoção precoce é uma aposta.
4. **Licença importa antes de codar.** Reutilizar código AGPL (OpenMontage) num sistema web publicado obriga a abrir o próprio código. MIT (Docsify, DeerFlow, Voicebox) não impõe essa condição.
5. **O SEO continua sendo um diferencial.** O principal ponto fraco do Docsify — conteúdo renderizado no cliente não é bem indexado — é exatamente o problema que HTML semântico e `<meta name="description">` resolvem. Boa prática: usar Docsify para documentação interna e HTML estático semântico para páginas que precisam ser encontradas por buscadores.

---

## 5. Fontes

- [jamiepine/voicebox](https://github.com/jamiepine/voicebox) · [releases](https://github.com/jamiepine/voicebox/releases)
- [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) · [The Future of Flowise (Discussion #6727)](https://github.com/FlowiseAI/Flowise/discussions/6727) · [flowiseai.com/sunset](https://flowiseai.com/sunset)
- [calesthio/OpenMontage](https://github.com/calesthio/OpenMontage) · [AGENT_GUIDE.md](https://github.com/calesthio/OpenMontage/blob/main/AGENT_GUIDE.md)
- [docsifyjs/docsify](https://github.com/docsifyjs/docsify) · [docsify.js.org](https://docsify.js.org)
- [bytedance/deer-flow](https://github.com/bytedance/deer-flow) · [deerflow.tech](https://deerflow.tech)
- Métricas quantitativas obtidas via API pública do GitHub em 30/08/2026.
