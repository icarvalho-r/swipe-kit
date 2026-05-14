---
name: setup
description: >
  Configura o Swipe Kit pra função da pessoa no time. Pergunta nome, função e
  preferências básicas, e gera _contexto/estrategia.md personalizado + copia as
  skills certas pra .claude/commands/. Use quando rodar /setup pela primeira vez.
---

# /setup — Configuração do Swipe Kit

## Verificação inicial

Antes de qualquer coisa, verifique se `_contexto/estrategia.md` já tem conteúdo personalizado (não só o template).

- Se **não tem ou está vazio**: rode o onboarding abaixo
- Se **já tem conteúdo**: avisar que o setup já foi feito e perguntar se quer refazer ou atualizar

---

## Onboarding

Comece com uma mensagem curta:

> "Boa. Vou te fazer 3-4 perguntas pra configurar o Claude pra sua função na Swipe. Em 2 minutos tá pronto."

Fazer as perguntas em sequência, uma por vez, em conversa natural.

### Pergunta 1
"Qual é o seu nome?"

### Pergunta 2
"Qual sua função na Swipe?"

Listar as opções de forma natural:

> "Pode ser uma dessas:
> - Sócio (Trevizan)
> - CEO (Caique)
> - CRM (Thais)
> - Dados / Activation (Guibson)
> - Onboarding (Henrique T)
> - Pesquisa e Social (Bruna)
> - Operacional (Helen, Luan)
> - Vendas / CS Proativo (Luanna)
> - Head de Operações (Isabella)
>
> Qual a sua?"

Aceitar variações ("CRM", "tô no CRM", "sou a Thais") e mapear pra função do `templates/funcoes/mapa.md`.

### Pergunta 3
"Qual é o seu foco principal agora? O que você tá tentando fazer ou resolver nos próximos 30 dias?"

(Pode ser "reduzir falha de pagamento", "fechar mais Debrief", "documentar onboarding", "lançar campanha X" — qualquer coisa que esteja na cabeça)

### Pergunta 4 (opcional)
"Tem alguma preferência de tom ou coisa que te incomoda em texto de IA? Se não tiver, eu sigo o tom padrão da Swipe."

(Se a pessoa disser "tudo bem o padrão", manter o `_contexto/preferencias.md` como está)

---

## Processamento

Com as respostas:

### 1. Ler `templates/funcoes/mapa.md`

Pra saber quais skills correspondem à função da pessoa.

### 2. Copiar skills da função pra `.claude/commands/`

Pra cada skill listada no mapa pra essa função:

- Skills de arquivo (ex: `analisar-dados`) → copiar `templates/skills/<skill>.md` pra `.claude/commands/<skill>.md`
- Skills de pasta simples (ex: `hormozi`) → copiar `templates/skills/<skill>/` pra `.claude/commands/<skill>/`
- Skills RMBC marcadas com `(rmbc)` → copiar `templates/skills/rmbc/<skill>/` pra `.claude/commands/<skill>/`

Mostrar os comandos disponíveis ao final.

Skills comuns que TODA função recebe (já estão em `.claude/commands/`):
- `/iniciar`
- `/syncar`
- `/atualizar`

(Não precisa copiar — já vieram com o kit)

### 3. Preencher `_contexto/estrategia.md`

Substituir o conteúdo placeholder por:

```markdown
# Foco Atual — [Nome]

## Função na Swipe
[Função respondida]

## Foco principal agora
[Resposta da pergunta 3]

## O que pode esperar
[Inferir do contexto da função e do foco — ex: "Tarefas relacionadas a [área]. Não priorizar [coisas fora do escopo]"]

---
*Atualize esse arquivo quando seu foco mudar.*
```

### 4. Atualizar `_contexto/preferencias.md` (se a pessoa pediu)

Se a pessoa respondeu algo na pergunta 4 que diverge do padrão Swipe, adicionar uma seção `## Preferências pessoais` no final do arquivo (sem reescrever o resto).

Se respondeu "tudo bem o padrão", não mexer.

### 5. Pular o que já tá pronto

NÃO refazer:
- `_contexto/empresa.md` (já vem com o contexto Swipe completo)
- `marca/design-guide.md` (já vem com a identidade Swipe)
- `CLAUDE.md` raiz (já tá configurado)

---

## Mensagem final

> "[Nome], teu setup tá pronto.
>
> Como [função], você agora tem essas skills:
> - `/iniciar` — carrega contexto da Swipe e do teu foco no começo da sessão
> - `/syncar` — salva no GitHub
> - [lista das skills específicas da função]
>
> **Como começar:**
> 1. Roda `/iniciar` no começo de cada nova conversa pra carregar o contexto
> 2. Chama qualquer skill com `/` (ex: `/email-profissional`)
> 3. Se aparecer algo que parece repetível e não tem skill, eu sugiro criar
>
> **Pra salvar teu trabalho:** roda `/syncar` quando quiser fazer backup no GitHub.
>
> Bora trabalhar."

---

## Regras

- Tom direto, sem excesso de entusiasmo
- Não listar todas as perguntas de uma vez — uma por vez, em conversa
- Se a função não bater com nenhuma do mapa, perguntar de novo dando as opções
- Não criar pastas extras (clientes/, projetos/, etc) — o kit é enxuto
- Gerar tudo de uma vez no final, não arquivo por arquivo durante as perguntas
