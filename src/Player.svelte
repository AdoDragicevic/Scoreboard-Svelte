<script>

    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

	export let name;
    export let points;
    export let id;

	let showControls = false;

	const addPoint = () => points += 1;
	const removePoint = () => points -= 1;
	const toggleControls = () => showControls = !showControls;
    const deletePlayer = () => dispatch("deleteplayer", id);

</script>


	<div class="card">
		<h1>
			{name}
			<button class="btn btn-sm" on:click={toggleControls}>
				{#if showControls}-{:else}+{/if}
			</button>
            <button on:click={deletePlayer}>Delete Player</button>
		</h1>
		<h3>Points: {points}</h3>
		{#if showControls}
		<button class="btn" on:click={addPoint}>+1</button>
		<button class="btn btn-dark" on:click={removePoint}>-1</button>
		<input type="number" bind:value={points}>
		{/if}
	</div>


<style>
	h1 {
		color: darkblue;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
</style>