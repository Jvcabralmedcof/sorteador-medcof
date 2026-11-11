# Política de segurança

## Como reportar uma falha

Se você encontrou uma falha de segurança no Sorteador MedCof, **não abra uma issue pública**.

Use o reporte privado do GitHub:

1. Abra a aba **Security** deste repositório.
2. Clique em **Report a vulnerability**.
3. Descreva o problema e como reproduzi-lo.

Só os mantenedores do repositório veem o reporte.

## O que está no escopo

- O código da página (`index.html`).
- A configuração de publicação (`vercel.json`).

## Como a página trata dados

- Os nomes digitados ficam apenas na memória do navegador de quem usa e somem ao fechar a aba.
- A página não grava cookies nem usa `localStorage`.
- A página não envia dados a nenhum servidor. O cabeçalho `Content-Security-Policy` com `connect-src 'none'` bloqueia esse tipo de envio.
