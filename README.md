# Assembleia Digital

Aplicação web responsiva para assembleias e votações, feita em HTML, CSS e JavaScript e conectada ao Supabase.

## Acessar

- Administração: `adm/adm.html`
- Participante: `cliente/cliente.html` (cadastro aberto por link de convite)

Sirva a pasta inteira por HTTP/HTTPS para que as páginas compartilhem a sessão de autenticação. O painel gera links com código para convidar participantes.

## Configuração do banco

O projeto Supabase está definido em `supabase-config.js`. O arquivo contém somente a URL e a chave publicável. A estrutura e as políticas RLS foram aplicadas no projeto Supabase conectado. As contas usam Supabase Auth; não existe senha administrativa padrão no front-end.

Para preparar o primeiro administrador, siga [supabase/README.md](supabase/README.md). O cadastro de participantes começa pelo link de convite. Se a confirmação de e-mail estiver habilitada no Supabase, a pessoa precisa confirmar o endereço antes de entrar.

## Publicar o site

O workflow [.github/workflows/deploy-pages.yml](.github/workflows/deploy-pages.yml) publica os arquivos estáticos no GitHub Pages a cada envio para a branch `main`. Crie ou escolha um repositório no GitHub, envie o projeto e, em **Settings → Pages**, selecione **GitHub Actions** como fonte. Depois do primeiro deploy, configure o endereço publicado em **Authentication → URL Configuration** no Supabase. A publicação requer uma conta e um repositório GitHub; ainda não há um destino conectado nesta pasta.

## Limites desta versão

Os e-mails de convite e resultado ainda são preparados no aplicativo de e-mail do usuário, não enviados automaticamente. Antes de usar em assembleias oficiais ou armazenar CPFs reais, configure os requisitos de privacidade, segurança, recuperação de conta, auditoria e operação adequados ao seu contexto. Os códigos de convite permitem cadastro a qualquer pessoa que tenha o link; compartilhe-os com cuidado.
