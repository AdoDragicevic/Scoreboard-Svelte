<script>

	import Title from "./Title.svelte";
	import Player from "./Player.svelte";
	import AddPlayer from "./AddPlayer.svelte";
	import ScoreList from "./ScoreList.svelte";

	import seedData from "./seedData";

	const localStrgPlayers = JSON.parse(window.localStorage.getItem("players"));

	let players = localStrgPlayers || seedData;
	let isDisplayScoreboard = true;

	const addPlayer = e => {
		const newPlayer = e.detail;
		players = [newPlayer, ...players];
		window.localStorage.setItem("players", JSON.stringify(players));
	};

	const deletePlayer = e => {
		const id = e.detail;
		players = players.filter(p => p.id !== id);
		window.localStorage.setItem("players", JSON.stringify(players));
	};

	const updatePlayer = e => {
		const { id, name , points } = e.detail;
		players = players.map(player => player.id === id ? {id, name, points, defaultPoints: points} : player);
		window.localStorage.setItem("players", JSON.stringify(players));
	};

	const resetDefaultPoints = e => {
		const id = e.detail;
		players = players.map(player => player.id === id ? {...player, points: player.defaultPoints} : player);
		window.localStorage.setItem("players", JSON.stringify(players));
	};

	const increment = e =>  {
		const {id, newPoints} = e.detail;
		players = players.map(player => player.id === id ? {...player, points: newPoints} : player);
		window.localStorage.setItem("players", JSON.stringify(players));
	};

	const showScoreBoard = () => isDisplayScoreboard = true;

	const showScoreList = () => isDisplayScoreboard = false;

	const playersSortedByPoints = () => {
		return [...players].sort((a,b) => (a.points < b.points) ? 1 : ((b.points < a.points) ? -1 : 0));
	};

</script>



<nav>
	<Title txt="Scoreboard" />
	<AddPlayer on:addplayer={addPlayer} />
</nav>

<div class="options">
	<span class={isDisplayScoreboard ? "underline" : ""} on:click={showScoreBoard}>
		Score board
	</span> 
	/ 
	<span class={isDisplayScoreboard ? "" : "underline"} on:click={showScoreList}> 
		Score list 
	</span>
</div>

<div class="container">
	{#if players.length === 0}
		<p>No players</p>
	{:else}
		{#if isDisplayScoreboard}
			{#each players as player}
				<Player
					name={player.name} 
					points={player.points} 
					id={player.id} 
					on:deleteplayer={deletePlayer}
					on:updateplayer={updatePlayer}
					on:resetdefaultpoints={resetDefaultPoints}
					on:increment={increment}
				/>
			{/each}
		{:else}
			<ScoreList players={playersSortedByPoints()} />
		{/if}
	{/if}
</div>


<style>
	nav {
		display: flex;
		justify-content: space-between;
		align-items: center;
		flex-wrap: wrap;
		padding: 2vh 1vw;
	}
	.options {
		color: #eee;
		text-align: center;
		margin-top: 1rem;
	}
	.options span {
		padding: 2px;
		text-transform: uppercase;
		font-weight: 300;
		letter-spacing: 1px;
		cursor: pointer;
	}
	.container {
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
		width: 95%;
		max-width: 900px;
		border-top: 1px solid rgba(0, 0, 0, .2);
		margin: 2rem auto 4rem auto;
	}
	.container p {
		color: #eee;
		margin-top: 2rem;
	}
	.underline {
		border-bottom: 1px solid #eee;
	}
	@media screen and (min-width: 920px) {
		.container {
			padding: 1rem;
		}
	}
</style>