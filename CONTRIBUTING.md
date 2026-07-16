# Fluxo de contribuição — Smart Produto Core Status Report

A partir de 16/07/2026, alterações no `index.html` deste repositório não são
mais enviadas diretamente para `main`. Toda mudança passa por Pull Request.

## Passo a passo

1. Criar uma branch a partir de `main`:
   - Convenção de nome: `update/DD-MM-descricao-curta` (ex.: `update/16-07-aba-outras-frentes`)
2. Commitar a alteração em `index.html` (ou outros arquivos do repo).
3. Push da branch para o GitHub.
4. Abrir o Pull Request contra `main` (via UI do GitHub, usando o link de
   compare que a branch gera automaticamente).
5. Aguardar aprovação de **qualquer um dos 4 autorizados**:
   - italo.gomes@smarttravelit.com.br
   - daniel.silva@smarttravelit.com.br
   - rafael.driendl@smarttravelit.com.br
   - mauricio.maran@smarttravelit.com.br
6. Após aprovação, fazer o merge (squash ou merge commit, sem preferência
   fixa) via GitHub.
7. Cloudflare Pages faz o deploy automático assim que `main` é atualizado —
   nenhuma ação extra é necessária depois do merge.

## Proteção de branch (configurar uma vez no GitHub)

Em `Settings → Branches → Branch protection rules`, criar regra para `main`:

- **Require a pull request before merging** — habilitado
- **Require approvals** — mínimo 1
- **Do not allow bypassing the above settings** — habilitado (inclui admins)
- Restringir push direto a `main` para ninguém (só via PR merge)

Isso precisa ser feito manualmente pelo dono do repositório — chamadas
programáticas à API do GitHub (`api.github.com`) não são alcançáveis a
partir do ambiente de execução do Claude, então essa configuração de
proteção de branch não pode ser automatizada por aqui.

## Observação sobre automação

Claude pode criar a branch, commitar e dar push. A criação do PR em si e o
merge continuam sendo uma ação humana (via github.com), pois:

- Não há conector de GitHub disponível no Cowork para essa conta.
- O acesso à API do GitHub (`api.github.com`) está bloqueado pela política
  de rede do ambiente sandbox usado pelo Claude (apenas `github.com` via
  `git` é permitido).

Quando a branch for enviada, o link de compare (`.../compare/main...NOME-DA-BRANCH`)
será fornecido no chat para abrir o PR com um clique.
