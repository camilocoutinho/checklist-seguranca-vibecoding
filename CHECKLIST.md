# 🔒 Checklist de Segurança para Vibecoding
### por Camilo Coutinho · Double Play Media

> "Construir com IA é rápido. Publicar um buraco de segurança também é."
> Este arquivo é o meu checklist antes de colocar qualquer app ou site no ar.
> Coloque-o na raiz do projeto e peça à IA para segui-lo **antes de cada deploy**.

Para colar de uma vez no Claude Code ou no Cursor, com este checklist já dentro do texto, use o [prompt unificado](PROMPT.md).

---

## Changelog

- **v2.0 (23/11/2026):** Entrou o fluxo do plugin oficial **Claude Security** e o aviso de que um pedido genérico do tipo "deixe o site seguro e inhackeável" não é auditoria. Fonte: [@matheustilli](https://www.instagram.com/p/DfUrdsQChb3/).
- **v1.0 (21/11/2026):** Versão inicial, a partir de @geraldo.alv3s, @o.lucasevangelista e @c4msg.

---

## Como usar com a IA (Claude, Cursor, etc.)

Cole este pedido:

> Leia o arquivo `CHECKLIST.md` e audite meu projeto item por item.
> Para cada item, diga **OK**, **FALHOU** ou **NÃO SE APLICA**, mostre **onde** verificou (arquivo e linha)
> e corrija o que falhou. Não me responda só "está tudo certo".
> Não basta um pedido genérico do tipo "deixe o site seguro e inhackeável": isso não é análise de segurança.
> Se estiver no Claude Code, instale o plugin oficial (`/plugin install claude-security@claude-plugins-official` e depois `/reload-plugins`, se ainda não estiver),
> rode `/claude-security`, escolha **Scan codebase** e cruze o relatório com este checklist.

---

<a id="chaves-e-segredos"></a>

## 1. Chaves e segredos
- [ ] As chaves de API **nunca** ficam no front-end nem visíveis no código do cliente. Elas ficam no back-end.
- [ ] Nenhuma senha ou segredo fica escrito direto no código (*hardcoded*).
- [ ] O `.env` está no `.gitignore` e nunca foi para o Git, principalmente em repositório público.
- [ ] O histórico do Git foi revisado em busca de senhas ou chaves vazadas, e as que vazaram foram trocadas.
- [ ] No front, uso só a chave **pública** do banco (*anon key*), nunca a chave de serviço ou admin.

<a id="acesso-e-usuarios"></a>

## 2. Acesso e usuários
- [ ] Existe login de verdade para usar a IA e as funções do app. Ninguém usa sem estar logado.
- [ ] A autenticação e as permissões são validadas **no servidor**, não só na tela.
- [ ] Não confio no ID que vem da tela do usuário. O servidor confirma quem ele é.
- [ ] O RLS (*Row Level Security*) está ativo e as permissões do banco estão travadas.
- [ ] As regras do Firebase, do Storage e do Supabase estão protegidas, sem leitura ou escrita pública.
- [ ] Cada usuário só vê e edita os próprios dados: o usuário A nunca mexe nos dados do usuário B.
- [ ] Todas as páginas e rotas de admin estão protegidas.
- [ ] Os cookies de sessão são seguros (`HttpOnly`, `Secure`, `SameSite`).
- [ ] As senhas são guardadas com hash (bcrypt ou argon2), nunca em texto puro.
- [ ] Há limite de tentativas no login e no cadastro.
- [ ] Há proteção contra bots (captcha ou *rate limit*).

<a id="dados-e-entradas"></a>

## 3. Dados e entradas
- [ ] Os dados sensíveis são criptografados.
- [ ] Uso consultas parametrizadas, sem injeção de SQL.
- [ ] Tudo o que o usuário envia é validado **no servidor**.
- [ ] O conteúdo escrito pelo usuário é limpo e escapado (contra XSS).
- [ ] O upload de arquivos está restrito por tipo, tamanho e local de armazenamento.
- [ ] Existe backup automático do banco.

<a id="servidor-e-publicacao"></a>

## 4. Servidor e publicação
- [ ] Os cabeçalhos de segurança estão configurados (CSP, HSTS, X-Frame-Options...).
- [ ] O CORS libera só os domínios certos, nunca `*` em produção.
- [ ] O HTTPS é obrigatório.
- [ ] As dependências estão atualizadas e sem vulnerabilidades conhecidas (`npm audit` ou equivalente).
- [ ] O modo debug está desligado em produção.
- [ ] O usuário não vê mensagens de erro detalhadas nem *stack trace*.

<a id="custos-da-ia"></a>

## 5. Custos da IA (para não acordar com uma fatura de milhares)
- [ ] Há limite de gasto configurado na OpenAI ou no provedor de IA que eu uso.
- [ ] Há limite de uso por usuário (requisições por dia ou por minuto).
- [ ] Há limite de cobrança (*billing*) e alerta de gasto na conta.

<a id="revisao-final"></a>

## 6. Revisão final (antes de publicar)
- [ ] Não usei um pedido genérico do tipo "deixe o site seguro e inhackeável" ou "não cometa erros". Isso não é análise, é torcida.
- [ ] A IA listou **o que verificou e onde**, em vez de só dizer "está tudo certo".
- [ ] Testei o app como um estranho: sem login, em aba anônima, tentando acessar o que não deveria.
- [ ] Pedi à IA para **simular um ataque** ao meu sistema, achar as brechas e corrigir cada uma.

<a id="plugin-claude-security"></a>

## 7. Plugin oficial Claude Security
O plugin da Anthropic não substitui este checklist: ele é um scan a mais, no Claude Code. Fonte: [@matheustilli](https://www.instagram.com/p/DfUrdsQChb3/).

- [ ] Para essa análise, o Claude Code está no modelo mais capaz disponível (no post: **Opus 5.5**, "o melhor, disparado" para este tipo de revisão).
- [ ] O plugin oficial está instalado: `/plugin install claude-security@claude-plugins-official`. Na página do plugin, clique em adicionar, volte ao Claude Code e rode `/reload-plugins`.
- [ ] Rodei `/claude-security` e escolhi a primeira opção, **Scan codebase (Recommended)**. Ele procura vulnerabilidades e bugs na codebase.
- [ ] Escolhi o alcance do scan (**completo**, o repositório inteiro, ou **parcial**, só uma parte do projeto) e confirmei o ok. O plugin avisa que o scan gasta bastante token e leva tempo: deixe o Claude Code aberto e espere.
- [ ] Li o relatório, corrigi o que ele encontrou e não publiquei só porque o scan rodou. Por baixo, o plugin coloca subagentes de segurança treinados nas falhas mais comuns e atualizados pela Anthropic.

---

## Regra de ouro do Camilo
> **A IA escreve o código. A responsabilidade continua sendo sua.**
> Rode este checklist a cada versão nova, não só no primeiro lançamento.

---
*Compilado por Camilo Coutinho a partir de dicas de @geraldo.alv3s, @o.lucasevangelista, @c4msg e @matheustilli, organizadas e complementadas. Versão 2.0 · novembro de 2026.*
