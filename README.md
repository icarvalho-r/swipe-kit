# Swipe Kit — Claude Code OS pro time da Swipe Offers

Workspace pré-configurado pra cada pessoa do time da Swipe Offers usar o Claude Code com contexto, marca e skills já alinhados.

Cada pessoa clona o repositório, roda `/setup`, responde a função no time e o Claude já vem com as skills certas pra rotina dela.

---

## Como instalar

### Opção 1 — Via prompt (mais fácil)

Com o Claude Code aberto em qualquer pasta, copie e cole:

```
Instala pra mim o repositório https://github.com/dobralabs/swipe-kit.git na pasta atual, abre ela e roda /setup
```

### Opção 2 — Via terminal

```bash
git clone https://github.com/dobralabs/swipe-kit.git
cd swipe-kit
code .
```

Abra o terminal integrado (`Cmd + ` no Mac / `Ctrl + ` no Windows) e rode:

```bash
claude
```

Depois:

```
/setup
```

---

## O que vem no kit

**Skills comuns (todo mundo recebe):**
- `/iniciar` — carrega o contexto da Swipe e da sua função no começo de cada sessão
- `/syncar` — salva no GitHub (commit + push)
- `/atualizar` — varre o projeto e atualiza arquivos de contexto desatualizados

**Skills por função:**

| Função | Skills atribuídas |
|---|---|
| Sócio (Trevizan) | `/analisar-dados`, `/email-profissional`, `/proposta-comercial`, `/slide` |
| CEO (Caique) | `/analisar-dados`, `/email-profissional`, `/slide`, `/roteiro-post` |
| CRM (Thais) | `/email-profissional`, `/roteiro-post`, `/analisar-dados` |
| Dados (Guibson) | `/analisar-dados`, `/publicar-site`, `/slide` |
| Onboarding (Henrique T) | `/email-profissional`, `/slide`, `/roteiro-post` |
| Pesquisa/Social (Bruna) | `/carrossel`, `/roteiro-post`, `/analisar-dados` |
| Operacional (Helen, Luan) | `/email-profissional`, `/proposta-comercial`, `/carrossel`, `/roteiro-post` |
| Vendas/CS (Luanna) | `/email-profissional`, `/roteiro-post`, `/analisar-dados` |
| Head de Operações (Isabella) | todas |

**Pré-configurado:**
- Contexto da Swipe Offers em `_contexto/empresa.md`
- Identidade visual da Swipe em `marca/design-guide.md`
- Tom de voz e preferências do time em `_contexto/preferencias.md`

---

## Estrutura

```
swipe-kit/
├── _contexto/          contexto da empresa, preferências, foco atual
├── marca/              identidade visual (cores, fontes, logo)
├── dados/              drop zone pra arquivos de análise
├── templates/
│   ├── skills/         catálogo completo de skills disponíveis
│   ├── funcoes/        mapa função → skills
│   └── ferramentas/    APIs e MCPs disponíveis
└── .claude/commands/   comandos ativos pro Claude
```

---

## Ficou travado?

Fala com a Isabella (`@isabella` ou ferramentas@swipeoffers.com.br).
