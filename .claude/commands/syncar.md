---
name: syncar
description: >
  Salva o estado atual do workspace no GitHub (commit + push).
  Use quando quiser garantir que o trabalho está seguro, ao final de uma sessão produtiva,
  ou quando o usuário disser "salva no github", "faz commit", "synca", "syncar",
  "backup no github", "salva tudo", "manda pro github".
  Também configura o git pela primeira vez se ainda não estiver configurado.
---

# /syncar — Salvar no GitHub

## Verificação inicial

```bash
git status --short
git remote get-url origin 2>/dev/null
```

---

## Fluxo A: sem remote configurado (primeira vez)

Se `git remote get-url origin` não retornar nada:

> "Seu workspace ainda não está conectado a um repositório no GitHub.
>
> Pra conectar, você precisa de um repositório:
> 1. Acesse github.com/new
> 2. Crie um repositório privado com o seu nome (ex: `swipe-thais`, `swipe-luanna`)
> 3. Não inicialize com README — deixa vazio
> 4. Me passa o link do repositório criado"

Após receber o link:

```bash
git remote add origin [link]
git branch -M main
git push -u origin main
```

> "Conectado. Seu workspace está em [link]."

---

## Fluxo B: remote configurado, tem mudanças

```bash
git add -A
git commit -m "sync: [descrição curta]"
git push
```

Descrição do commit: o que foi feito na sessão (ex: "sync: emails de dunning revisados", "sync: novo carrossel social", "sync: atualização de contexto"). Se não souber, usar `sync: atualizações do dia`.

> "Salvo. Seu trabalho está em [url do remote]."

---

## Fluxo C: sem mudanças

> "Tudo já está sincronizado."

---

## Fluxo D: erro no push

> "Não consegui enviar pro GitHub. O erro foi: [mensagem]
>
> Causas comuns:
> - Sem conexão
> - Precisa configurar autenticação (token ou SSH)
>
> Se quiser resolver, me diz."

---

## Regras

- Nunca commitar `.env`, `.env.local` ou qualquer arquivo com chave secreta
- Tom direto, sem explicar git a fundo
- Se der erro, mostrar o próximo passo — nunca só o erro
