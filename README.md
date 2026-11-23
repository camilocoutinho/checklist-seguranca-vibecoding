# Checklist de Segurança para Vibecoding

**Camilo Coutinho · [Double Play Media](https://doubleplay.com.br)**

> Construir com IA é rápido. Publicar um buraco de segurança também é.

Checklist para revisar a segurança de um app ou site **antes de publicar**. Para criadores e alunos que programam com IA (vibecoding), no Claude Code, no Cursor ou em outra ferramenta.

> **A IA escreve o código. A responsabilidade continua sendo sua.**

---

## O que é

Um roteiro item a item para passar no projeto antes de cada deploy. Sete blocos: chaves, acesso, dados, servidor, custo de IA, revisão final e o plugin oficial Claude Security.

Versão 2.0 · 23/11/2026.

## Para quem é

- Quem constrói um app ou site com IA e vai colocar no ar.
- Alunos de vibecoding que querem um checklist concreto antes do deploy.

## Como usar

1. Abra **[PROMPT.md](PROMPT.md)**.
2. Copie o bloco do prompt. O checklist já vai dentro dele.
3. Cole no **Claude Code** ou no **Cursor**, na raiz do projeto.
4. Rode antes de cada deploy, em cada versão nova.

Para cada item, a resposta tem de ser **OK**, **FALHOU** ou **NÃO SE APLICA**, com arquivo e linha. "Está tudo certo", sozinho, não fecha a revisão.

No Claude Code, o prompt pede o plugin oficial: instalar com `/plugin install claude-security@claude-plugins-official`, rodar `/claude-security`, escolher **Scan codebase** e cruzar o relatório com o checklist.

## O checklist

Texto completo, com changelog: **[CHECKLIST.md](CHECKLIST.md)**.

1. [Chaves e segredos](CHECKLIST.md#chaves-e-segredos) — API no back-end, nada de segredo no Git.
2. [Acesso e usuários](CHECKLIST.md#acesso-e-usuarios) — login de verdade, permissão no servidor, RLS.
3. [Dados e entradas](CHECKLIST.md#dados-e-entradas) — validar no servidor, sem injeção de SQL nem XSS.
4. [Servidor e publicação](CHECKLIST.md#servidor-e-publicacao) — HTTPS, CORS, cabeçalhos, debug desligado.
5. [Custos da IA](CHECKLIST.md#custos-da-ia) — limite de gasto e de uso por usuário.
6. [Revisão final](CHECKLIST.md#revisao-final) — testar como estranho e simular um ataque.
7. [Plugin oficial Claude Security](CHECKLIST.md#plugin-claude-security) — um scan a mais, no Claude Code.

## Créditos

Compilado por Camilo Coutinho a partir de dicas de @geraldo.alv3s, @o.lucasevangelista, @c4msg e @matheustilli, organizadas e complementadas. Versão 2.0 · novembro de 2026.

A parte sobre o plugin oficial Claude Security vem de um post de [@matheustilli](https://www.instagram.com/p/DfUrdsQChb3/) no Instagram. O plugin da Anthropic não substitui este checklist: ele é um scan a mais, no Claude Code.

## Aviso

Este checklist não substitui uma auditoria profissional de segurança.

Um pedido genérico do tipo "deixe o site seguro e inhackeável" não é análise de segurança.

## Outros projetos

- **[bases-animacao-reels](https://github.com/camilocoutinho/bases-animacao-reels)** — bases de animação para Reels, para alunos de edição.

## Camilo Coutinho

Estrategista de vídeo e YouTube, fundador da Double Play Media e autor de *Vídeos que Vendem Mais*.

**[doubleplay.com.br](https://doubleplay.com.br)**

## Licença

Conteúdo sob [CC BY 4.0](LICENSE) (Atribuição 4.0 Internacional).

Pode copiar, adaptar e republicar, inclusive comercialmente. Dê crédito ao Camilo Coutinho, inclua o link da licença e indique se houve alteração.
