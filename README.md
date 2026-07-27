## Jogo da Velha 4x4

## Tecnologias
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black) ![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white) ![CSS](https://img.shields.io/badge/CSS-239120?&style=for-the-badge&logo=css3&logoColor=white) ![SVELTE](https://img.shields.io/badge/Svelte-4A4A55?style=for-the-badge&logo=svelte&logoColor=FF3E00)

## O que é

Uma versão 4x4 do jogo da velha (em vez do tradicional 3x3), feita em [Svelte](https://svelte.dev/). O projeto nasceu como trabalho da disciplina de Lógica de Programação e serviu de introdução ao conceito de framework front-end para quem estava começando a programar.

O jogo tem três telas controladas por um estado global simples (`src/Estado.js`):

- **Menu** — tela inicial, com atalhos para jogar ou ver a página "Sobre".
- **Jogar** — o tabuleiro 4x4 em si.
- **Sobre** — créditos do projeto.

## Como funciona

O tabuleiro é representado por um array reativo de 16 posições (`celulas`, em `src/Jogar.svelte`). Cada clique em uma célula vazia marca a posição com "X" ou "O" e o Svelte atualiza a tela automaticamente — sem nenhuma manipulação manual de DOM.

A verificação de vitória usa uma lista fixa com todas as combinações de índices que formam 4 em linha no tabuleiro 4x4 (linhas, colunas e as duas diagonais):

```js
const condicaodevitoria = [
	[0, 1, 2, 3],
	[4, 5, 6, 7],
	[8, 9, 10, 11],
	[12, 13, 14, 15],
	[0, 4, 8, 12],
	[1, 5, 9, 13],
	[2, 6, 10, 14],
	[3, 7, 11, 15],
	[0, 5, 10, 15],
	[3, 6, 9, 12]
]
```

A cada jogada, o código testa se alguma dessas combinações está totalmente preenchida pelo jogador da vez. Se nenhuma combinação vencer e todas as 16 células estiverem preenchidas, o jogo termina em empate. O botão "Reiniciar" apenas zera esse estado, sem recarregar a página.

## Como rodar

```bash
npm install
npm run dev
```

Em outro terminal:

```bash
npm start
```

Depois é só abrir `http://localhost:5000` (ou a porta indicada no terminal) no navegador.

## Desenvolvedores

Projeto criado em 2021 pela turma abaixo, como trabalho de conclusão da disciplina de Lógica de Programação. A ideia original ficou parada desde então, sem continuidade por parte da turma:

- <a href="https://github.com/IsaacLuiz88"> Isaac Luiz </a>
- <a href="https://github.com/Jonatas2021"> Jonatas Cândido</a>
- <a href="https://github.com/gabriellaBatista"> Gabriella Batista </a>
- <a href="https://github.com/BrunoSTZ"> Bruno Stelzer</a>
- <a href="https://https://github.com/jenni101101"> Jennifer Fonseca</a>

Em 2026, Isaac Luiz retomou o projeto sozinho para finalizar o que havia ficado incompleto: a lógica de jogo (vitória, empate e reinício) foi reescrita usando a reatividade do Svelte, e os protótipos antigos em JavaScript puro, que não eram mais usados, foram removidos.
