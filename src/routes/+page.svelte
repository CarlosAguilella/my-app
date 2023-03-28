<div class ='page'>

    <img src='logo.jpg' alt=''/>

    <h1>Torneo padel DAW</h1>

    {#if players.length < 8}
        <input bind:value = {name}/>
    
        <button on:click={addJugador}>ADD a {name}</button>
    {/if}
    
    
    
    <ul>
        {#each players as player}
            <li>{player} <button on:click={() => remJugador(player)}>🚮🚮🚮</button></li>            
        {/each}
    </ul>
</div>

<script>
    let name ='';

    let players = ['Hector','Carlos','Gerard','Alex','Josep','JP','Juan'];

    function addJugador() {
        players.push(name);
        players = players;
    }

    function remJugador(playerToRemove){
        players = players.filter(player => player !== playerToRemove);
    }
</script>

<style>
    .page{
        display: grid;
        justify-content: center;
    }
    li{
        list-style-type: "🎾";
        background-color: rgb(89, 243, 148);
        font-size: 25px;
        font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
        padding: 0.6em;
        margin: 0.3em;
        box-shadow: 3px 3px 3px black;
    }
</style>