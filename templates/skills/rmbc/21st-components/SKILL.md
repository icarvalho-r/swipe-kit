---
name: 21st-components
description: Busca e extrai componentes prontos do 21st.dev/community/components usando browser automation. Recebe uma descrição do componente desejado, navega no site, encontra o mais relevante e retorna o código completo pronto para uso.
allowed-tools: Bash(npx agent-browser:*), Bash(agent-browser:*), WebFetch
---

# Skill: 21st-components

Busca componentes do 21st.dev e retorna o código pronto para usar no projeto.

## Como funciona

1. Recebe a descrição do componente que o usuário quer (ex: "card de produto", "navbar com dropdown", "hero section animada")
2. Navega em https://21st.dev/community/components
3. Identifica os componentes mais relevantes
4. Acessa o componente escolhido e extrai o código-fonte completo
5. Entrega o código pronto com instruções de uso

## Fluxo de execução

### Passo 1 — Abrir o site e buscar

```bash
agent-browser open https://21st.dev/community/components
agent-browser snapshot -i
```

Se houver campo de busca, usar:
```bash
agent-browser fill @[ref-do-input] "[descrição do componente]"
agent-browser snapshot -i
```

### Passo 2 — Identificar componentes relevantes

Fazer snapshot da página e listar os componentes visíveis. Apresentar ao usuário os 3-5 mais relevantes com nome e descrição antes de prosseguir.

### Passo 3 — Acessar o componente

```bash
agent-browser click @[ref-do-componente]
agent-browser snapshot -i
```

Ou acessar diretamente pela URL do componente se disponível.

### Passo 4 — Extrair o código

Procurar o botão de "View code", "Copy", ou aba de código. Fazer snapshot para identificar a ref correta:

```bash
agent-browser click @[ref-botao-codigo]
agent-browser snapshot -i
```

Extrair o conteúdo do bloco de código com:
```bash
agent-browser text @[ref-bloco-codigo]
```

### Passo 5 — Entregar

Retornar:
- Nome e link do componente
- Stack utilizada (React, Tailwind, etc.)
- Dependências necessárias (se houver)
- Código completo, pronto para copiar

## Instrução para o Claude

Ao executar essa skill:

1. Sempre confirmar com o usuário qual componente encontrado ele quer antes de extrair o código
2. Se o site tiver autenticação obrigatória para ver o código, informar e oferecer alternativa (ex: buscar o componente no GitHub do autor)
3. Adaptar o código ao stack do projeto atual se o usuário informar qual está usando (React, HTML/Tailwind, Next.js, etc.)
4. Se o componente usar dependências externas (Framer Motion, Radix, etc.), listar claramente no início

## Exemplos de uso

- `/21st-components card de produto com imagem e botão`
- `/21st-components navbar responsiva com menu mobile`
- `/21st-components hero section com gradiente animado`
- `/21st-components tabela de preços com toggle mensal/anual`
- `/21st-components formulário de contato com validação`
