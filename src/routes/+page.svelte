<div class ='page'>

    <img src='logo.jpg' alt=''/>

    <h1>Torneo padel DAW</h1>
    
    <input />
    
    <button on:click={addJugador}>ADD</button>
    
    <p>{name}</p>

</div>

<script>
    let name = 'Carlos';

    function addJugador() {
        name = 'Hector';
    }
</script>

<style>
    .page{
        display: grid;
        justify-content: center;
    }
</style>