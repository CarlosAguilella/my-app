<div class ='page'>

<img src='logo.jpg' alt=''/>    
    <h1>Torneo padel DAW</h1>
    <input bind:value={nPlayer}/>

    {#if faltanPlayers }
        <input bind:value = {name}/>
    
        <button on:click={addJugador}>ADD a {name}</button>
    {/if}
    
    
    
    {#each players as player}
        <li>{player} <button on:click={() => remJugador(player)}>🚮🚮🚮</button></li>            
    {/each}

    <button disabled={faltanPlayers} on:click={generar}>GENERAR</button>
    
    {#each partidos as p}
        <li><button>{p.j1} - {p.j2}</button> vs <button>{p.j3} - {p.j4}</button></li>
    {/each}

</div>

<script>
    let name ='';
    let nPlayer ='';

    let players = ['Hector','Carlos','Gerard','Alex','Josep','JP','Juan','Dolors'];
    let partidos = [];
    let ranking = [];

    $: faltanPlayers = players.length < nPlayer;

    function addJugador() {
        players.push(name);
        players = players;
    }

    function remJugador(playerToRemove){
        players = players.filter(player => player !== playerToRemove);
    }

    function generar(){
        let playersCopia = players;
        partidos=[];
        for(let i = 0; i<players.length/4;i++){
            let j1 = playersCopia[Math.floor(Math.random() * playersCopia.length)];
            playersCopia = playersCopia.filter(player => player !== j1);

            let j2 = playersCopia[Math.floor(Math.random() * playersCopia.length)];
            playersCopia = playersCopia.filter(player => player !== j2);

            let j3 = playersCopia[Math.floor(Math.random() * playersCopia.length)];
            playersCopia = playersCopia.filter(player => player !== j3);

            let j4 = playersCopia[Math.floor(Math.random() * playersCopia.length)];
            playersCopia = playersCopia.filter(player => player !== j4);

            partidos.push({j1:j1, j2:j2, j3: j3, j4:j4});
        }

        partidos = partidos;
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