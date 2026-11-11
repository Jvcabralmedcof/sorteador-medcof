# Sorteador MedCof

Sorteador de nomes e números do Grupo MedCof. É uma página estática: um único `index.html`, sem servidor, sem banco de dados e sem dependências para instalar.

- **Nomes:** lista com um nome por linha, quantidade de ganhadores, opção de não repetir e de remover os sorteados da lista.
- **Números:** intervalo "de/até", quantidade, opção de permitir repetição e de ordenar o resultado.
- O sorteio usa `crypto.getRandomValues`, o gerador aleatório criptográfico do navegador.
- Os nomes digitados ficam só no navegador de quem usa. A página não envia nada para nenhum servidor, e o cabeçalho de segurança `connect-src 'none'` bloqueia qualquer envio.

## Arquivos

| Arquivo | Para que serve |
|---|---|
| `index.html` | A página inteira (HTML, CSS e JavaScript). O logo vai embutido. |
| `favicon.png` | Ícone da aba do navegador. |
| `vercel.json` | Cabeçalhos de segurança aplicados pelo Vercel em cada resposta. |
| `SECURITY.md` | Como reportar uma falha de segurança. |

> **Nunca suba listas de participantes** (planilhas, CSV, nomes de alunos) para este repositório. Ele é público, e esses dados são pessoais (LGPD).

---

## 1. Criar o repositório no GitHub (pelo site, sem linha de comando)

1. Acesse **github.com/new**.
2. Nome: `sorteador-medcof`. Visibilidade: **Public**. Deixe as opções de README, .gitignore e licença **desmarcadas**.
3. Clique em **Create repository**.
4. Na página seguinte, clique no link **uploading an existing file**.
5. Arraste estes 5 arquivos: `index.html`, `favicon.png`, `vercel.json`, `README.md` e `SECURITY.md`.
6. Clique em **Commit changes**.

## 2. Ligar as verificações de segurança do GitHub

Em **Settings → Advanced Security** do repositório (em algumas contas o menu se chama **Code security**), ative:

| Recurso | O que faz |
|---|---|
| **Private vulnerability reporting** | Permite que alguém reporte uma falha em particular, sem expor publicamente. |
| **Dependabot alerts** | Avisa se algo que o projeto usa tiver uma vulnerabilidade conhecida. |
| **Secret Protection** e **Push protection** | Bloqueia o envio de senhas, tokens ou chaves por engano. |
| **CodeQL analysis → Set up → Default** | Analisa o JavaScript da página a cada mudança e abre um alerta se achar algo inseguro. |

Os alertas aparecem na aba **Security** do repositório. Em repositórios públicos todos esses recursos são gratuitos.

## 3. Publicar no Vercel

1. Acesse **vercel.com/new** e entre com **Continue with GitHub**.
2. Autorize o Vercel a acessar **apenas** o repositório `sorteador-medcof`.
3. Clique em **Import** no repositório.
4. Em **Framework Preset**, escolha **Other**. Não precisa preencher comando de build.
5. Clique em **Deploy**. Em menos de um minuto o site fica no ar num endereço `*.vercel.app`.

A partir daí, **toda mudança no GitHub publica sozinha** no Vercel.

### Domínio próprio (opcional)

No Vercel, em **Settings → Domains**, adicione algo como `sorteio.grupomedcof.com.br`. O Vercel mostra o registro DNS (CNAME) que o time de TI precisa criar.

### Plano do Vercel

O plano gratuito (Hobby) do Vercel é só para uso pessoal e não comercial. Para uso da empresa, o correto é o plano **Pro**. Se preferir não pagar, o site também funciona no Cloudflare Pages, no Netlify ou no GitHub Pages, mas aí o `vercel.json` não vale e os cabeçalhos de segurança precisam ser configurados no formato de cada um.

## 4. Fazer alterações depois

1. No GitHub, abra o `index.html` e clique no ícone de lápis (**Edit this file**).
2. Faça a mudança e clique em **Commit changes**.
3. O Vercel publica a nova versão sozinho em cerca de 30 segundos.

Para trocar um arquivo inteiro, use **Add file → Upload files** e arraste a versão nova.

## Cabeçalhos de segurança (`vercel.json`)

| Cabeçalho | Efeito |
|---|---|
| `Content-Security-Policy` | A página só carrega a si mesma e as fontes do Google. `connect-src 'none'` impede qualquer envio de dados. `frame-ancestors 'none'` impede que outro site a coloque dentro de um iframe. |
| `X-Frame-Options: DENY` | Mesma proteção contra iframe, para navegadores antigos. |
| `X-Content-Type-Options: nosniff` | O navegador não tenta adivinhar o tipo dos arquivos. |
| `Referrer-Policy` | Não vaza o endereço completo ao clicar em links externos. |
| `Permissions-Policy` | Bloqueia câmera, microfone, localização, pagamentos e USB. |
| `Cross-Origin-Opener-Policy` | Isola a página de janelas abertas por outros sites. |
