# 💰 FinChat - Assistente Financeiro com IA

> Projeto desenvolvido durante o **DIO Lab: Vibe Coding**. Um aplicativo de controle financeiro baseado em chat (Conversational UI), gerado 100% com Inteligência Artificial.

![Status do Projeto](https://img.shields.io/badge/Status-Concluído-green) ![IA](https://img.shields.io/badge/AI-Powered-blueviolet)

## 🔗 Demo Online
👉 **[Clique aqui para testar o App](https://claude.ai/public/artifacts/b502cc62-8fd6-4442-99bc-983d762e0ed3)**

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

---

## 🚀 Como Rodar Localmente
Como o projeto é um arquivo único, é extremamente simples:

1.  Clone este repositório ou baixe o arquivo `index.html`.
2.  Dê um duplo clique no `index.html`.
3.  Pronto! O app rodará diretamente no seu navegador padrão.

## 📄 Licença
Projeto desenvolvido para fins educacionais. Sinta-se livre para usar e modificar.

---
*Desenvolvido com 💚 e Inteligência Artificial.*
