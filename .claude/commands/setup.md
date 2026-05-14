---
name: setup
description: >
  Configura o Swipe Kit pra função da pessoa no time. Reconhece a pessoa pelo nome,
  confirma função, pergunta sobre o contexto atual e copia as skills certas.
  Usar quando rodar /setup pela primeira vez.
---

# /setup — Configuração do Swipe Kit

## Antes de começar — ler o contexto

Antes de qualquer mensagem, ler:

1. `_contexto/empresa.md` — o que é a Swipe, produtos, time, projetos ativos
2. `templates/time/pessoas.md` — quem é quem no time, apelidos, função e contexto atual de cada pessoa
3. `templates/funcoes/mapa.md` — quais skills correspondem a cada função

Com isso carregado, o Claude já sabe: o que é o High Ticket, quem é o Luan, o que a Thais faz, o que tá ativo em cada frente. Usar esse contexto naturalmente nas perguntas — sem precisar explicar o que é a Swipe pra pessoa.

---

## Verificação inicial

Checar se `_contexto/estrategia.md` já tem conteúdo real (sem `<!-- NOT CONFIGURED -->`).

- Se **já tem conteúdo personalizado**: avisar que o setup já foi feito e perguntar se quer refazer.
- Se **não tem ou está vazio**: rodar o onboarding abaixo.

---

## Onboarding

### Passo 1 — Pedir o nome

> "Oi. Qual é o seu nome?"

Aguardar a resposta.

---

### Passo 2 — Reconhecer a pessoa

Ler `templates/time/pessoas.md` e tentar identificar a pessoa pelo nome ou apelido informado.

**Se reconheceu:**

Confirmar diretamente com tom casual — sem perguntar de novo:

> "Luan — você é o Operacional né. Sei que você tá tocando o High Ticket agora.
> Qual é o seu foco principal na próxima semana?"

Adaptar a fala ao contexto da pessoa conforme o `templates/time/pessoas.md`:
- Se a pessoa tem um campo **"Pergunta de contexto"** definido, usar exatamente aquela pergunta
- Caso contrário, mencionar o projeto ativo mais relevante pra função e perguntar sobre o foco atual
- Tom: conversa entre colegas, não onboarding corporativo

**Se não reconheceu (nome desconhecido):**

> "[Nome] — qual é a sua função na Swipe?"

Listar as opções de forma natural:

> "Pode ser: Sócio, CEO, CRM, Dados, Onboarding, Pesquisa/Social, Operacional, Vendas/CS ou Head de Ops."

---

### Passo 3 — Pergunta de contexto

Usar o campo **"Pergunta de contexto"** do `templates/time/pessoas.md` pra essa pessoa. Se não tiver, perguntar: "Qual é o seu foco principal essa semana?"

Aguardar a resposta.

### Passo 3b — Perguntas extras (se houver)

Se a pessoa tiver campo **"Pergunta extra"** no `pessoas.md`, fazer essas perguntas em sequência.

Exemplo pra Luan:
1. "Quais concorrentes você tá analisando no High Ticket agora? Me passa os nomes que eu já crio as pastas."
2. "E pro Spy do produto principal — tem concorrentes específicos que você acompanha?"

Guardar as respostas pra usar na criação de pastas no Passo 5.

Aguardar as respostas.

---

### Passo 4 (opcional) — Preferências

> "Tem alguma preferência de tom ou coisa que te incomoda em texto de IA? Se não tiver, sigo o padrão da Swipe."

Se disser "tudo bem" ou não tiver preferência específica: manter `_contexto/preferencias.md` como está, sem modificar.

---

## Processamento — gerar os arquivos

### 1. Preencher `_contexto/estrategia.md`

Incluir também os concorrentes ou projetos que a pessoa mencionou nas perguntas extras, se houver.

```markdown
# Foco Atual — [Nome]

## Função na Swipe
[Função]

## Foco principal agora
[Resposta da pergunta de contexto]

## O que pode esperar
[Inferir do contexto e função — ex: "Tarefas relacionadas a high ticket, espionagem e operação"]

---
*Atualize esse arquivo quando seu foco mudar.*
```

### 2. Criar estrutura de pastas

Ler o campo **"Estrutura de pastas"** da pessoa em `templates/time/pessoas.md` e criar as pastas listadas.

Para pastas dinâmicas (como os concorrentes do Luan):
- Usar os nomes informados nas perguntas extras pra criar subpastas dentro da pasta pai
- Normalizar os nomes: minúsculo, espaço → hífen (ex: "Hotmart Club" → `hotmart-club`)
- Se a pessoa não informou nenhum nome, criar `concorrente-1/` como placeholder

Exemplo para Luan (se ele informou "Hotmart Club" e "Mentoria Pay"):
```
high-ticket/
  hotmart-club/
  mentoria-pay/
  referencias/
  scripts/
spy/
  analises/
```

Criar também um `README.md` mínimo dentro de cada pasta principal explicando o que vai lá.

### 3. Copiar skills da função pra `.claude/commands/`

Ler `templates/funcoes/mapa.md` e copiar as skills da função:

- Skills de arquivo `.md` → copiar `templates/skills/<skill>.md` pra `.claude/commands/<skill>.md`
- Skills de pasta → copiar `templates/skills/<skill>/` pra `.claude/commands/<skill>/`
- Skills RMBC `(rmbc)` → copiar `templates/skills/rmbc/<skill>/` pra `.claude/commands/<skill>/`

Skills comuns (já estão em `.claude/commands/`, não precisa copiar):
- `/iniciar`, `/syncar`, `/atualizar`, `/setup`

### 4. Atualizar `_contexto/preferencias.md` (só se a pessoa pediu algo diferente)

Se respondeu algo na pergunta opcional que diverge do padrão: adicionar seção `## Preferências pessoais` no final.
Se não pediu nada: não tocar no arquivo.

---

## Mensagem final

```
[Nome], pronto.

Como [função], você tem:
- /iniciar — carrega contexto da Swipe e do teu foco no começo da sessão
- /syncar — salva no GitHub
[lista das skills específicas copiadas]

Pastas criadas:
[lista das pastas criadas, incluindo as de concorrentes se houver]

Como usar: chama qualquer skill com / (ex: /email-profissional, /hook-battery).
Roda /iniciar no começo de cada nova conversa.
```

Tom direto. Sem entusiasmo excessivo. Sem listas de instruções longas.

---

## Regras

- Tom casual — conversa entre colegas, não onboarding corporativo
- Se reconheceu a pessoa, NÃO pedir a função de novo — confirmar e seguir
- Se a função for desconhecida, pedir e mapear pro mapa de funções
- Não criar pastas extras (projetos/, clientes/, etc.)
- Gerar tudo de uma vez no final — não ir arquivo por arquivo durante as perguntas
- Máximo 3-4 perguntas no total
