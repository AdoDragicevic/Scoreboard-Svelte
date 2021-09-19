<script>
    export let players;
</script>

{#each players as player, index}
    <article class="item">
        <span class="index">{index+1}.</span>
        <div class="content">
            <span class="content__name">{player.name}</span>
            <span class="content__score">{player.points}</span>
        </div>
    </article>
{/each}

<style>
    .item {
        height: 60px;
		margin: 1rem;
        padding: 0 2rem;
		border-radius: 15px;
        /*
        background-color: #363940;
        */
        background-color: rgb(24, 30, 44);
        background-color: rgb(21, 26, 39);
        color: #BABBBF;
		width: 100%;
		box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px, rgba(50, 50, 93, 0.25) 0px 30px 6px -12px inset, rgba(0, 0, 0, 0.3) 0px 18px 9px -18px inset;
		display: flex;
		align-items: center;
		transition: all .3s ease-in;
        animation: fadeIn 1s ease-in;
    }
    .item:hover .content__name {
        color: rgb(145, 111, 53);
    }
    .item:hover {
        transform: translateX(2px);
    }
    .index {
        width: 5%;
        min-width: 15px;
    }
    .content {
        display: flex;
        justify-content: space-between;
        width: 95%;
    }
    .content__name {
        width: 80%;
        text-transform: uppercase;
		letter-spacing: 2px;
		font-size: 15px;
		overflow: hidden;
    }
    .content__score {
        color: red;
    }
    @keyframes fadeIn {
        0% {
            opacity: 0;
        }
        100% {
            opacity: 100%;
        }
    }
</style>