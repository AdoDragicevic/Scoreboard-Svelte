<script>

	import Navbar from "./Navbar.svelte";
	import Player from "./Player.svelte";
	import AddPlayer from "./AddPlayer.svelte";

	const seedPlayers = [
		{name: "Ado", points: 55, id: 1},
		{name: "Hrvoje", points: 5, id: 2},
		{name: "Job", points: 7, id: 3},
		{name: "Milan", points: 90, id: 4}
	];

	const localStrgPlayers = JSON.parse(window.localStorage.getItem("players"));

	let players = localStrgPlayers || seedPlayers;

	const addPlayer = e => {
		const newPlayer = e.detail;
		players = [...players, newPlayer];
		window.localStorage.setItem("players", JSON.stringify(players));
	};

	const deletePlayer = e => {
		const id = e.detail;
		players = players.filter(p => p.id !== id);
		window.localStorage.setItem("players", JSON.stringify(players));
	}

</script>


<Navbar />
<div class="container">
	<AddPlayer on:addplayer={addPlayer} />
	{#if players.length === 0}
		<p>No players</p>
	{:else}
	{#each players as player}
		<Player
			name={player.name} 
			points={player.points} 
			id={player.id} 
			on:deleteplayer={deletePlayer}
		/>
	{/each}
	{/if}
</div>