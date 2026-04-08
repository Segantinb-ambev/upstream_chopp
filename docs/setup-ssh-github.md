# Setup SSH — GitHub Ambev

Siga os passos abaixo uma única vez. Depois, push e pull funcionam sem senha.

---

## Passo 1 — Gerar a chave SSH

Abra o Terminal e rode:

```bash
ssh-keygen -t ed25519 -C "seu-email@ze.delivery" -f ~/.ssh/id_ed25519_ambev -N ""
```

Vai aparecer algo como:

```
Your identification has been saved in /Users/seu-usuario/.ssh/id_ed25519_ambev
Your public key has been saved in /Users/seu-usuario/.ssh/id_ed25519_ambev.pub
```

---

## Passo 2 — Copiar a chave pública

```bash
cat ~/.ssh/id_ed25519_ambev.pub
```

Selecione e copie **toda** a linha que aparecer (começa com `ssh-ed25519`).

---

## Passo 3 — Adicionar a chave no GitHub

1. Acesse: [github.com/settings/keys](https://github.com/settings/keys)
2. Clique em **New SSH key**
3. **Title:** `Mac - upstream-chopp`
4. **Key type:** Authentication Key
5. **Key:** cole a linha copiada no passo anterior
6. Clique em **Add SSH key**

---

## Passo 4 — Configurar o host SSH local

Rode o comando abaixo no Terminal (copia e cola tudo de uma vez):

```bash
cat >> ~/.ssh/config << 'EOF'

Host github-ambev
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_ambev
EOF
```

---

## Passo 5 — Adicionar o GitHub nos hosts conhecidos

```bash
ssh-keyscan github.com >> ~/.ssh/known_hosts
```

---

## Passo 6 — Testar a conexão

```bash
ssh -T git@github-ambev
```

Se funcionou, vai aparecer:

```
Hi Segantinb-ambev! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## Passo 7 — Clonar o repositório

```bash
git clone --recurse-submodules git@github-ambev:Segantinb-ambev/upstream_chopp.git
cd upstream_chopp
```

A flag `--recurse-submodules` garante que a skill LIPE (design) também seja baixada.

---

## Pronto

Abra a pasta `upstream_chopp` no Cursor e as skills já estarão disponíveis.

Para pegar atualizações do Bruno no futuro:

```bash
git pull origin main
```

---

## Problemas comuns

**"Permission denied (publickey)"**
→ A chave não foi adicionada no GitHub ou o `~/.ssh/config` está errado. Refaça os passos 3 e 4.

**"Host key verification failed"**
→ Refaça o passo 5 (`ssh-keyscan`).

**Push rejeitado**
→ Alguém commitou antes. Rode `git pull origin main` e tente o push novamente.
