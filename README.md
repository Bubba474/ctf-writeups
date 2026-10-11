# ctf-writeups 🚩

Coletânea organizada das minhas resoluções de **Capture The Flag**. Cada writeup prioriza o
*raciocínio* — como cheguei ao vetor, o que descartei e por quê — mais do que o despejo de comandos.

> ⚖️ Todos os desafios foram resolvidos em plataformas de CTF/treino autorizadas
> (HackTheBox, TryHackMe, PicoCTF e similares). As técnicas são apresentadas para fins educacionais.

---

## Índice

| Writeup | Categoria | Plataforma | Dificuldade | Técnicas |
|---|---|---|---|---|
| [idor-no-perfil](writeups/web/idor-no-perfil.md) | Web | Treino | Fácil | IDOR, enumeração de IDs |
| [sqli-login-bypass](writeups/web/sqli-login-bypass.md) | Web | Treino | Médio | SQL injection, bypass de auth |

> Lista crescendo conforme resolvo novos desafios.

---

## Metodologia

Sigo um fluxo consistente, documentado em [`METHODOLOGY.md`](METHODOLOGY.md):

```
Recon → Enumeração → Identificação do vetor → Exploração → Flag → Lição
```

Cada writeup usa o mesmo [template](TEMPLATE.md), então é fácil comparar abordagens entre
desafios.

## Por que isto num portfólio

Resolver o desafio é metade; **comunicar** a solução de forma clara é a outra. Writeups mostram
como eu penso, documento e transfiro conhecimento — habilidade central em red team e consultoria.

## Estrutura

```
ctf-writeups/
├── METHODOLOGY.md      # meu fluxo de trabalho
├── TEMPLATE.md         # modelo de writeup
└── writeups/
    ├── web/
    ├── crypto/
    ├── pwn/
    └── forensics/
```
