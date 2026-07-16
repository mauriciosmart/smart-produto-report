# Fluxo de contribuição — Smart Produto Core Status Report

A partir de 16/07/2026, alterações no `index.html` deste repositório não são
mais enviadas diretamente para `main`. Toda mudança passa por Pull Request.

## Passo a passo

1. Criar uma branch a partir de `main`:
   - Convenção de nome: `update/DD-MM-descricao-curta` (ex.: `update/16-07-aba-outras-frentes`)
2. Commitar a alteração em `index.html` (ou outros arquivos do repo).
3. Push da branch para o GitHub.
4. Abrir o Pull Request contra `main`. O link de compare fornecido no chat
   já vem com **título e descrição pré-preenchidos** via query params
   (`?title=...&body=...`) — ao clicar, o GitHub abre o formulário de PR
   com o template abaixo pronto; só falta clicar em "Create pull request".
   Se por algum motivo o pré-preenchimento não aparecer, o texto da
   descrição também é enviado no chat para copiar e colar manualmente.
5. Aguardar aprovação de **qualquer um dos 4 autorizados**:
   - italo.gomes@smarttravelit.com.br
   - daniel.silva@smarttravelit.com.br
   - rafael.driendl@smarttravelit.com.br
   - mauricio.maran@smarttravelit.com.br
6. Após aprovação, fazer o merge (squash ou merge commit, sem preferência
   fixa) via GitHub.
7. Cloudflare Pages faz o deploy automático assim que `main` é atualizado —
   nenhuma ação extra é necessária depois do merge.

## Template de descrição do PR

Toda branch enviada por Claude inclui uma descrição de PR com esta estrutura,
para facilitar a revisão de quem for aprovar:

```
## O que mudou
- (resumo objetivo da mudança)

## Por que
- (motivo/contexto da mudança)

## Validação
- (checagens automáticas feitas: divs balanceados, html fecha corretamente,
  contagem de abas, etc.)

## Aprovação
Qualquer um dos 4 autorizados (Ítalo, Daniel, Rafael, Maurício) pode aprovar
e mesclar.
```

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
