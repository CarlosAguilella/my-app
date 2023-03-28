<div class ='page'>

<img src='logo.jpg' alt=''/>    
    <h1>Torneo padel DAW</h1>
    <input bind:value={nPlayer}/>

    {#if faltanPlayers }
        <input bind:value = {name}/>
    
        <button on:click={addJugador}>ADD a {name}</button>
    {/if}
    
    
    
    <ul>
        {#each players as player}
            <li>{player} <button on:click={() => remJugador(player)}>🚮🚮🚮</button></li>            
        {/each}
    </ul>

    <button disabled={faltanPlayers} on:click={partidos}>GENERAR</button>
    
    {#each parejas as pareja}
        <li>{pareja.j1} y {pareja.j2}</li>
    {/each}

</div>

<script>
    let name ='';
    let nPlayer ='';

    let players = ['Hector','Carlos','Gerard','Alex','Josep','JP','Juan','Dolors'];
    let parejas = [];

    $: faltanPlayers = players.length < nPlayer;

    function addJugador() {
        players.push(name);
        players = players;
    }

    function remJugador(playerToRemove){
        players = players.filter(player => player !== playerToRemove);
    }
    function partidos(){
        parejas=[];
        for(let i = 0; i<players.length/2;i++){
            let j1 = players[Math.floor(Math.random() * players.length)];
            players = players.filter(player => player !== j1);

            let j2 = players[Math.floor(Math.random() * players.length)];
            players = players.filter(player => player !== j2);

            parejas.push({j1:j1,j2:j2});
        }

        parejas = parejas;
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
    button{
        font-size: 30px;
    }
    input{
        font-size: 30px;
    }
</style>