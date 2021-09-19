<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

	export let name;
    export let points;
    export let id;

	let showControls = false;

	const increment = (e) => {
		let newPoints;
		if (e.target.name === "minus") newPoints = points - 1;
		else newPoints = points + 1;
		dispatch("increment", {id, newPoints});	
	}
	const toggleControls = () => showControls = !showControls;
    const deletePlayer = () => dispatch("deleteplayer", id);
	const updatePlayer = () => {
		toggleControls();
		return dispatch("updateplayer", {id, name, points});
	};
	const resetDefaultPoints = () => dispatch("resetdefaultpoints", id);
</script>



<div class="card">
	<div class="card__header">
		{#if !showControls}
			<h5 class="card__title">{name}</h5>
			<div class="card__option-btns">
				<button class="btn-secondary" on:click={toggleControls}>
					&#9881;
				</button>
				<button class="btn-secondary" on:click={resetDefaultPoints}>
					&#8635;
				</button>
				<button class="btn-secondary" on:click={deletePlayer}>
					x
				</button>
			</div>
		{/if}
	</div>

	{#if !showControls}
		<div class="card__main-content">
			<button class="btn-primary" name="minus" on:click={increment}>-</button>
			<div class="card__score">
				<h3>{points}</h3>
				<span>Points</span>
			</div>
			<button class="btn-primary" name="plus" on:click={increment}>+</button>
		</div>
	{:else}
		<form class="card__edit-content" on:submit={updatePlayer}>
			<button class="btn-secondary btn-secondary--back" type="submit">
				&#8592;
			</button>
			<label class="card__input-label">
				Change name
				<input class="card__input" type="text" bind:value={name}>
			</label>
			<label class="card__input-label">
				Change score
				<input class="card__input" type="number" bind:value={points} min="-999" max=999>
			</label>
		</form>	
	{/if}
</div>



<style>
	.card {
		height: 150px;
		overflow: hidden;
		margin: 1rem;
		border-radius: 15px;
        /*
		background-color: #363940;
		background-color: rgb(48, 55, 75);
		*/
		background-color: rgb(21, 26, 39);
		color: #BABBBF;
		position: relative;	
		flex-grow: 1;
		width: 100%;
		box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px, rgba(50, 50, 93, 0.25) 0px 30px 6px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 9px -18px inset;
		display: flex;
		align-items: center;
		justify-content: center;
		transition: all .2s ease-in;
		flex-grow: 1;
	}
	.card__header {
		width: 100%;
		display: flex;
		justify-content: space-between;
		position: absolute;
		top: 1rem;
		left: 1rem;
		width: 95%;
		/*
		color: rgb(134, 109, 65);
		*/
		color: rgb(145, 111, 53);
		opacity: .8;
	}
	.card__title {
		text-transform: uppercase;
		font-family: sans-serif;
		letter-spacing: 2px;
		font-size: 15px;
		overflow: hidden;
		font-weight: 100;
		width: 60%;
		overflow: hidden;
	}
	.card__option-btns {
		width: 25%;
		min-width: 100px;
		display: flex;
		justify-content: space-around;
		align-items: flex-start;
	}
	.btn-secondary {
		background-color: transparent;
		border: none;
		outline: none;
		cursor: pointer;
		font-size: 12px;
		padding: 0;
		color: inherit;
	}
	.btn-secondary--back {
		font-size: 20px;
		transform: translateY(-10px);
		color: #bb9450;
	}
	.card__main-content {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 70%;
		padding-top: 10px;
	}
	.card__main-content div {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.btn-primary {
		background-color: transparent;
		border-radius: 100px;
		width: 45px;
		height: 45px;
		outline: none;
		cursor: pointer;
		transition: all .2s ease-in-out;
		font-size: 20px;
		font-weight: 100;
		color: rgba(238, 238, 238, .4);
		outline: none;
		border: 1px solid rgba(238, 238, 238, .4);
	}
	.btn-primary:hover {
		border: 1px solid rgba(238, 238, 238, .5);
	}
	.btn-primary:active {
		transform: scale(.95);
	}
	.card__score h3 {
		font-size: 4rem;
		font-weight: 100;
	}
	.card__score span {
		font-size: 8px;
		text-transform: uppercase;
		letter-spacing: 2px;
		font-family: sans-serif;
	}
	.card__edit-content {
		display: flex;
		flex-direction: column;
		width: 90%;
		padding-top: 1rem;
	}
	.card__input-label {
		font-size: 10px;
	}
	.card__input {
		width: 100%;
		background-color: red;
		border: none;
		outline: none;
		height: 35px;
        padding-left: 20px;
        background-color: rgb(54,55,61);
        background: linear-gradient(90deg, rgba(54,55,61,1) 0%, rgba(47,48,52,1) 93%);
        color: #BABBBF;
        border: 1px solid rgb(54,55,61);
        transition: all .5s;
		margin-bottom: 5px;
	}
	@media screen and (min-width: 920px) {
		.card {
			max-width: 380px;
		}
		.card__title {
			width: 70%;
		}
		.card__option-btns {
			width: 25%;
		}
	}
</style>