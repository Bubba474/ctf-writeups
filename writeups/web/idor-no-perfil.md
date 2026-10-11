# IDOR no perfil de usuário

| | |
|---|---|
| **Categoria** | Web |
| **Plataforma** | Ambiente de treino |
| **Dificuldade** | Fácil |

## Enunciado

> A aplicação deixa cada usuário ver "seu" perfil em `/profile?id=1001`. Ache a flag no perfil do administrador.

## Recon

Após o login como usuário comum, a URL do perfil é:

```
GET /profile?id=1001
```

O `id` no parâmetro é um número sequencial e — importante — a página não parece amarrar esse `id`
à sessão autenticada.

## Enumeração

Hipótese imediata: **IDOR** (Insecure Direct Object Reference). Testei trocar o próprio `id` por
outro valor:

```
GET /profile?id=1000
```

A aplicação retornou o perfil de **outro** usuário — ou seja, a autorização é feita só pela posse
do `id`, não pela identidade da sessão.

## Vetor

IDOR clássico: o backend confia no `id` fornecido pelo cliente sem verificar se o usuário logado
tem permissão de ver aquele objeto. Faltou um *authorization check* no servidor.

## Exploração

Contas administrativas costumam estar nos primeiros IDs. Enumerando para baixo a partir de 1001,
o `id=1` revelou o perfil do administrador com a flag no campo de bio.

```
GET /profile?id=1
```

## Flag

```
flag{idor_broken_object_level_authorization}
```

## Lição

Este é o **A01:2021 – Broken Access Control** do OWASP Top 10 (especificamente BOLA/IDOR). A
correção não é esconder o `id` nem torná-lo aleatório (isso é *security by obscurity*) — é validar,
**no servidor e a cada requisição**, que o usuário autenticado tem direito ao objeto solicitado:

```python
# errado: confia no id do cliente
profile = db.get_profile(request.args["id"])

# certo: amarra à identidade/autorização da sessão
profile = db.get_profile(request.args["id"])
if not current_user.can_view(profile):
    abort(403)
```

UUIDs ajudam a dificultar enumeração, mas **não substituem** o controle de acesso.
