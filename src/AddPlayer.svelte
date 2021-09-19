<script>

    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    let player = {
        name: "",
        points: 0,
        defaultPoints: 0,
        id: Math.random() * Math.random()
    }

    const onSubmit = e => {
        e.preventDefault();
        player.defaultPoints = player.points;
        dispatch("addplayer", player);
        player = {
            name: "",
            points: 0,
            defaultPoints: 0,
            id: Math.random() * Math.random()
        }
    };

</script>


<form on:submit={onSubmit}>
    <input type="text" placeholder="Player name" bind:value={player.name} required>
    <input type="number" placeholder="Player points" bind:value={player.points} min="-999" max=999>
    <button class="ui primary button" type="submit">+</button>
</form>


<style>
    form {
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-end;
        flex-grow: 1;
        max-width: 500px;
    }
    form > * {
        border-radius: 15px;
        border: none;
        outline: none;
        margin: 0 .5rem;
        height: 2.2rem;
        line-height: 2.2rem;
        padding: 0 5px;
        min-width: 50px;
        box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px,rgba(50, 50, 93, 0.3) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px, rgba(10, 37, 64, 0.3) 0px -2px 6px 0px inset;
    }
    input {
        max-width: 200px;
        padding-left: 20px;
        flex-grow: 1;
        flex-shrink: 1;
        /*
        background-color: rgb(54,55,61);
        background-image: linear-gradient(90deg, rgba(54,55,61,1) 0%, rgba(47,48,52,1) 93%);
        */
        background-color: rgb(42, 44, 51);
        background-image: linear-gradient(90deg, rgba(42,44,51,1) 0%, rgba(47,48,52,1) 93%);
        color: #BABBBF;
        border: 1px solid rgb(54,55,61);
        transition: all .5s;
    }
    input:focus,
    input:hover {
        padding-left: 25px;
    }
    button {
        border-radius: 100px;
        font-weight: 400;
        font-size: 20px;
        letter-spacing: 1px;
        cursor: pointer;
        min-width: 2.2rem;
        /*
        background-color: rgb(13, 13, 14);
        */
        background-color: rgb(40, 43, 49);
        color: orangered;
        transition: all .3s;
    }
    button:hover {
        transform: scale(1.1);
    }
    button:active {
        transform: scale(1);
        background-color: rgb(54,55,61);
    }
    @media screen and (max-width: 920px) {
        form {
            margin: 1rem auto;
        }
    }
    @media screen and (max-width: 620px) {
        form {
            display: flex;
            flex-direction: column;
        }
        form > * {
            margin: 0 auto;
        }
        input {
            margin-bottom: .5rem;
            width: 90%;
            max-width: 90%;
        }
        button {
            width: 50%;
        }
	}
</style>