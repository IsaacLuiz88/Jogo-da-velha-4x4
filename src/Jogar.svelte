<svelte:head>
	<link rel="stylesheet" href="/styles/jogar.css">
</svelte:head>

<script>
	import VoltarMenu from './VoltarMenu.svelte'

	// todas as combinações de 4 índices que formam uma vitória no tabuleiro 4x4
	// (linhas, colunas e as duas diagonais)
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

	// estado do jogo: cada posição do array representa uma célula do tabuleiro.
	// como é uma variável normal (não um writable do Estado.js), o svelte já
	// re-renderiza o HTML sozinho sempre que ela é reatribuída.
	let celulas = criarTabuleiroVazio()
	let jogadorDaVez = 'x'
	let vencedor = null // null, 'x', 'o' ou 'empate'

	function criarTabuleiroVazio() {
		return Array(16).fill(null)
	}

	// reiniciar o jogo é só voltar o estado para os valores iniciais
	function reiniciar() {
		celulas = criarTabuleiroVazio()
		jogadorDaVez = 'x'
		vencedor = null
	}

	function jogar(indice) {
		// ignora o clique se a célula já estiver marcada ou o jogo já tiver terminado
		if (celulas[indice] || vencedor) {
			return
		}

		// reatribuir o array (em vez de só mudar uma posição) garante que o
		// svelte perceba a mudança e atualize a tela
		celulas = celulas.map((valor, i) => i === indice ? jogadorDaVez : valor)

		if (checarVencedor(jogadorDaVez)) {
			vencedor = jogadorDaVez
		} else if (checarEmpate()) {
			vencedor = 'empate'
		} else {
			jogadorDaVez = jogadorDaVez === 'x' ? 'o' : 'x'
		}
	}

	function checarVencedor(jogador) {
		return condicaodevitoria.some((combinacao) =>
			combinacao.every((indice) => celulas[indice] === jogador)
		)
	}

	function checarEmpate() {
		return celulas.every((valor) => valor !== null)
	}
</script>

<h1>
	{#if vencedor}
		Fim de jogo
	{:else}
		É a vez do jogador <span class="marcador {jogadorDaVez}">{jogadorDaVez.toUpperCase()}</span>
	{/if}
</h1>

<div class="container">
	{#each celulas as valor, indice}
		<div class="cell {valor}" on:click={() => jogar(indice)}>
			{valor ? valor.toUpperCase() : ''}
		</div>
	{/each}
</div>

{#if vencedor}
	<div class="mensagemdeVitoria">
		<p class="mensagemdeVitoria-text">
			{vencedor === 'empate' ? 'Empatou!' : `${vencedor.toUpperCase()} Venceu!`}
		</p>
		<button class="mensagemdeVitoria-button" on:click={reiniciar}>
			Reiniciar!
		</button>
	</div>
{/if}

<br>

<!-- reaproveita o botão de voltar para o menu -->
<VoltarMenu/>
