# Supabase

O banco conectado foi preparado com a migração inicial aplicada diretamente ao projeto Supabase.
O esquema contém perfis, assembleias, pautas, inscrições e votos, com RLS habilitado.

## Primeiro administrador

1. No Supabase Dashboard, abra **Authentication → Providers → Email** e ajuste o tamanho mínimo da senha para 4 caracteres. Depois, em **Authentication → Users → Add user**, crie a conta com o e-mail `julia_adm@assembleia.local`, senha `1234` e e-mail confirmado. O painel apresenta o login como `Julia_adm` e converte esse nome para o e-mail interno da conta.
2. Nos metadados do usuário, informe `full_name` e um `cpf` com 11 dígitos. Exemplo: `{"full_name":"Julia_adm","cpf":"00000000000"}`. Esse CPF de exemplo é apenas um identificador técnico do perfil administrativo; não use dados pessoais reais no ambiente de demonstração.
3. Copie o UUID da conta em **Authentication → Users** e, no SQL Editor, promova somente essa conta:

```sql
update public.profiles
set role = 'admin'
where id = 'UUID_DA_CONTA';
```

O cadastro público sempre cria perfis como participante. A coluna de função não pode ser alterada pelo cliente.

O login solicitado usa uma senha de quatro dígitos, fácil de adivinhar e abaixo do mínimo de oito caracteres recomendado pelo Supabase. Para um site público, troque por uma senha longa antes de divulgar o endereço. A senha é mantida pelo Supabase Auth e não fica escrita nos arquivos do site.

## URLs de autenticação

No Supabase Dashboard, configure **Authentication → URL Configuration** com a URL HTTPS do site em **Site URL** e inclua a URL da página `cliente/cliente.html` na lista de redirecionamentos permitidos. O link de confirmação de e-mail retorna ao convite que iniciou o cadastro.

## Segurança

`supabase-config.js` contém somente a URL e a chave publicável do projeto. Nunca use uma chave `secret` ou `service_role` no front-end. A autorização depende das políticas RLS do banco.
