# Metodologia

O fluxo que sigo em qualquer desafio, do recon à flag. Não é rígido — é um checklist mental que
evita pular etapas sob pressão.

## 1. Recon

- Ler o enunciado **duas vezes**. Palavras no título/descrição costumam ser dicas.
- Mapear a superfície: portas, endpoints, tecnologias, parâmetros.
- Anotar tudo. Um achado "inútil" agora pode ser a chave depois.

## 2. Enumeração

- Web: diretórios, métodos HTTP, cookies, headers, JS do front, comentários no HTML.
- Rede: versões de serviço, banners, configs default.
- Buscar o *delta*: o que foge do padrão é quase sempre o caminho.

## 3. Identificação do vetor

- Formular hipóteses de vulnerabilidade a partir do que foi enumerado.
- Priorizar pelo custo/benefício: testar o mais provável e barato primeiro.

## 4. Exploração

- Validar a hipótese com o menor PoC possível antes de automatizar.
- Iterar: cada erro do servidor é informação.

## 5. Flag & Lição

- Capturar a flag.
- Escrever a **lição**: que configuração/erro permitiu o ataque e como seria mitigado no mundo real.
  Essa seção é a que transforma um CTF em aprendizado transferível.

## Princípios

- **Documentar enquanto resolve**, não depois — detalhes se perdem.
- **Entender > decorar**: saber *por que* o payload funciona vale mais que o payload.
- **Time-box**: travou? Anota o estado, troca de abordagem.
