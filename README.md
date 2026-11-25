# Painel Slim3D – Fluxo de impressão 3D

Painel de pedidos de impressão 3D do Fab Lab Joinville: quadro de pedidos, agenda das máquinas, estoque de material, analíticos e exportação dos trabalhos concluídos para Excel / Google Planilhas.

É um arquivo único (`index.html`). Não precisa de servidor: ele busca as respostas do formulário pelo Apps Script do Google e envia o e-mail de "pronto" pelo EmailJS.

## Publicar no GitHub Pages

1. Crie um repositório **público** no GitHub (ex.: `painel-impressao`).
2. **Add file → Upload files** → envie o `index.html` (e este `README.md`) → **Commit changes**.
3. **Settings → Pages** → *Source*: **Deploy from a branch** → branch **main**, pasta **/ (root)** → **Save**.
4. Em 1–2 minutos o painel fica em `https://SEU-USUARIO.github.io/painel-impressao/`.

Para atualizar, envie o novo `index.html` por cima do antigo no mesmo repositório.

> Os pedidos, a agenda e o estoque ficam salvos **no navegador** de quem usa. Para levar para outro computador, use **💾 Salvar backup** e **📂 Carregar backup**.

## Exportar trabalhos concluídos (Analíticos)

Em **Analíticos → Exportar trabalhos concluídos**:

- **⬇ Excel (.xlsx)** baixa a planilha.
- **Google Planilhas** baixa a mesma planilha e abre o Google Planilhas. Lá, clique no ícone de pasta (*Abrir seletor de arquivos*) → *Fazer upload* e escolha o arquivo.

Uma linha por trabalho da coluna **Prontos**, respeitando o período do filtro de datas e, se escolhida, a impressora. Colunas:

| Coluna | De onde vem |
|---|---|
| Nome do Projeto | Formulário (editável) |
| Nome de quem enviou | Formulário (editável) |
| Telefone | Formulário (editável). Sempre gravado como texto |
| E-mail | Formulário (editável) |
| Tempo de impressão (h) | Duração agendada (editável) |
| Quantidade de material (g/ml) | Material lançado no agendamento (editável) |
| Material | Rolo/resina usado; sem agendamento, o material escolhido no formulário |
| Máquina | Impressora agendada |
| Material próprio | **Sim** se o material usado é do estoque da equipe, **Não** se é da casa. Sem material lançado, usa a resposta do formulário. Pode ser fixado em ✎ Editar dados |

Antes de baixar, o painel avisa quantos trabalhos estão com algum campo vazio. Para completar, use **✎ Editar dados** no pedido.

## Campos que o Apps Script precisa enviar

O painel lê o JSON do Apps Script (`SCRIPT_URL` no código). Para preencher as colunas novas, cada resposta precisa trazer:

| Dado | Nomes aceitos no JSON |
|---|---|
| Nome de quem enviou | `submitter`, `senderName`, `fullName`, `nomeCompleto`, `nome`, `solicitante`, `requester` |
| Telefone | `phone`, `telefone`, `whatsapp`, `celular`, `tel` |
| Material escolhido | `material` |
| Filamento próprio | `ownFilament`, `filamentoProprio`, `materialProprio`, `ownMaterial` |

Se o script não enviar algum desses campos, a coluna sai vazia, e você pode completar em **✎ Editar dados**.
