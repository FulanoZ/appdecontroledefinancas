# 💰 FinChat - Assistente Financeiro com IA

> Projeto desenvolvido durante o **DIO Lab: Vibe Coding**. Um aplicativo de controle financeiro baseado em chat (Conversational UI), gerado 100% com Inteligência Artificial.

![Status do Projeto](https://img.shields.io/badge/Status-Concluído-green) ![IA](https://img.shields.io/badge/AI-Powered-blueviolet)

## 🔗 Demo Online
👉 **[Clique aqui para testar o App](https://claude.ai/public/artifacts/b502cc62-8fd6-4442-99bc-983d762e0ed3)**

## PRD refinado no Perplexity com correções de erros

```Markdown 
Role: Você é um Tech Lead e Desenvolvedor Fullstack Sênior.
Projeto: Criar um MVP de App de Finanças Pessoais (Mobile First) chamado "FinChat".
Stack: React (Vite), Tailwind CSS, Lucide React (ícones), Context API.

Contexto e Problemas Conhecidos (Para você já resolver):
Versões anteriores falharam em:

Confundir números em frases normais com gastos (ex: "quero comprar 1 ps5" virava gasto de R$ 1,00).

Interpretar valores brasileiros errado (ex: "3.500" virava 3,50).

Não persistir dados entre abas (o chat sumia).

Elogiar gastos ("Continue assim" ao registrar despesa).

Requisitos Funcionais Obrigatórios:

Core: Processamento de Linguagem Natural (Frontend Only)

Crie uma função robusta processMessage(text) que identifique intenções:

LIMPEZA: palavras "reset", "limpar", "zerar". Ação: Limpar tudo.

META: palavras "meta", "comprar", "juntar", "sonho". Ação: Criar meta. (NUNCA registrar como gasto).

RECEITA/ECONOMIA: palavras "ganhei", "recebi", "economizei". Ação: Add transação tipo 'income'. Elogiar o usuário!

GASTO (Default): Se tem número e não é meta/receita. Ação: Add transação tipo 'expense'. Resposta neutra/informativa.

CORREÇÃO/NEGAÇÃO: Se começar com "Não", "Errado", "Corrija". Ação: Ignorar e pedir para reformular.

Tratamento de Moeda (Crítico)

Crie uma função parseCurrencyBR(text) que lide corretamente com formatos:

"3.500" -> 3500.00

"3500" -> 3500.00

"1.200,50" -> 1200.50

"50" -> 50.00

Estado Global (Context API)

FinanceContext deve guardar: transactions, goals, chatHistory, balance.

O histórico do chat deve persistir ao navegar entre as abas.

Interface (UI/UX)

Layout Mobile: Barra de navegação inferior fixa (Chat | Resumo | Metas).

Aba Chat: Lista de mensagens (balões verdes para user, cinza para bot).

Aba Resumo: Cards com "Saldo Atual", "Entradas", "Saídas" e lista de últimas transações.

Aba Metas: Lista de cartões com barra de progresso. Se vazio, mostrar empty state amigável.

Instruções de Saída (Output):
Gere o código completo em múltiplos arquivos (simulados) para eu copiar:

App.tsx (Roteamento simples condicional)

FinanceContext.tsx (Lógica pesada aqui)

utils/parser.ts (Funções de regex e moeda)

components/ChatTab.tsx

components/SummaryTab.tsx

components/GoalsTab.tsx

Estilo: Use Tailwind para um visual limpo, moderno e verde (tema financeiro). Utilize cores escuras para ficar agradavel aos olhos
```

Interações com o Claude

> Olá, preciso criar um APP com vibe coding para um trabalho de um curso. Preciso que voce crie {PRD}

> PS5 (play station 5) ele adicionou um gasto de 5 reais erroneamente e nao criou a meta. Depois, pedi pra ele apagar todas as metas e ele nao entendeu. Preciso de um app que funcione com todas as funcionalidades.

> outro problema, eu peço para ele resetar os gastos, ele diz que fez, mas quando vou na aba "resumos" ele mantem o mesmo valor de R$ 639,90. Outro problema é que o histórico do chat desaparece quando eu navego entre as abas do app.

> O que eu disse foi resolvido, ele arrumou. Porém identifiquei outro problema. Na primeira imagem, eu pedi para ele criar uma nova meta de comprar um PS5 (play station 5) ele adicionou um gasto de 5 reais erroneamente e nao criou a meta. Depois, pedi pra ele apagar todas as metas e ele nao entendeu. Preciso de um app que funcione com todas as funcionalidades.

Site resultado final: https://claude.ai/public/artifacts/b502cc62-8fd6-4442-99bc-983d762e0ed3

<img width="672" height="940" alt="image" src="https://github.com/user-attachments/assets/4f029ec1-4d61-4c8d-9823-6c1333f67107" />
<img width="670" height="936" alt="image" src="https://github.com/user-attachments/assets/12952673-d2c7-411e-8f2f-faee8f56032c" />

---

## 🛠️ Tecnologias
O diferencial deste projeto é sua arquitetura **Serverless e No-Build**. Todo o código (Lógica React, Estilos e Componentes) reside em um único arquivo HTML, compilado em tempo real no navegador.

- **React + ReactDOM** (via CDN)
- **Babel Standalone** (para compilar JSX no browser)
- **Tailwind CSS** (para estilização via CDN)
- **Lucide React** (ícones via CDN)

## 📱 Funcionalidades
- **Registro via Chat:** Digite naturalmente (ex: *"Gastei 35,00 no almoço"*).
- **Criação de Metas:** Reconhecimento inteligente de objetivos (ex: *"Quero comprar um PS5 de 3.500"*).
- **Dashboard:** Resumo visual de entradas, saídas e saldo.
- **Persistência:** O histórico e os dados não somem ao navegar entre abas.

---

## 🤖 A Jornada "Vibe Coding" (Processo de Criação)
Este projeto foi um exercício de **Prompt Engineering** avançado utilizando o **Claude 3.5 Sonnet**.

### 🚧 O Desafio da Lógica
Inicialmente, a IA tinha dificuldade em distinguir números de produtos de valores monetários.
*   *Erro:* Ao digitar "Meta PS5", o app registrava um gasto de R$ 5,00.
*   *Erro:* Ao digitar "Gastei 3.500", ele entendia R$ 3,50 (formatação americana).

### 💡 A Solução via Prompt
Refinamos o prompt para incluir uma lógica de **Parsing de Intenção** (NLP simplificado) escrita em Javascript puro:

1.  **Normalização:** Tratamento específico para moeda brasileira (ponto como milhar, vírgula como decimal).
2.  **Regex Inteligente:** Filtros que removem palavras do contexto de "Meta" antes de capturar o valor, evitando que números de modelos (iPhone 15, PS5) sejam lidos como dinheiro.
3.  **Contexto:** Separação estrita entre "Despesa", "Receita" e "Meta" baseada em palavras-chave.

### Reflexão

#### O que funcionou bem?
- A geração inicial da interface (UI) com React e Tailwind foi extremamente rápida e visualmente agradável, tanto no Lovable quanto no Bolt/Claude.
- A estratégia de usar um arquivo HTML único ("No-Build") facilitou muito o deploy e o compartilhamento do projeto final sem configurações complexas.
- O conceito de "Context API" para manter o estado do chat entre as abas funcionou perfeitamente após o ajuste no prompt.

#### O que não funcionou como o esperado?
- A lógica inicial de interpretação de texto (NLP) da IA foi simplista demais, confundindo números de produtos (ex: "PS5") com valores monetários.
- A persistência de dados e histórico do chat falhou nas primeiras versões ao navegar entre as telas, exigindo uma refatoração da arquitetura de estado.
- O reconhecimento de moeda brasileira (R$ 3.500 vs 3,50) precisou de regras explícitas de Regex para não seguir o padrão americano.

#### O que aprendeu sobre conversar com IAs?
- A importância da especificidade técnica nos prompts: pedir "um app financeiro" gera algo genérico; pedir "um parser que ignore números seguidos de texto" resolve problemas reais.
- Que a IA atua melhor quando você divide o problema: primeiro a interface, depois a lógica de estado, e por fim as regras de validação de dados.
- Iterar entre diferentes ferramentas (Lovable -> Bolt -> Claude) é uma estratégia válida para superar limitações de créditos ou capacidade de raciocínio de cada modelo.

---

## 🚀 Como Rodar Localmente
Como o projeto é um arquivo único, é extremamente simples:

1.  Clone este repositório ou baixe o arquivo `index.html`.
2.  Dê um duplo clique no `index.html`.
3.  Pronto! O app rodará diretamente no seu navegador padrão.

## 📄 Licença
Projeto desenvolvido para fins educacionais. Sinta-se livre para usar e modificar.
