<script>
    export let txt;
</script>

<h1>{txt}</h1>

<style>
    h1 {
        color: #BABBBF;
        padding: 1rem;
        font-size: 15px;
        letter-spacing: 2px;
        font-family: sans-serif;
        font-weight: 100;
        text-align: center;
        text-transform: uppercase;
        color: rgba(255, 69, 0, .5);
        transition: all .5s ease;
    }
    @media screen and (max-width: 920px) {
        h1 {
            text-align: center;
            width: 100%;
        }
	}
</style>