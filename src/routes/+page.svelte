<div class ='page'>

    <img src='logo.jpg' alt=''/>    
    <h1>Torneo padel DAW</h1>

    {#if nPlayersEstablecido === false}
        <input bind:value={nPlayer}/>
        <button on:click={establecerCantidad}>CANTIDAD JUGADORES</button>
    {/if}

    {#if faltanPlayers && nPlayersEstablecido}
        <input bind:value = {name}/>
        <button on:click={addJugador}>ADD a {players.length+1} de {nPlayer}</button>
    {/if}
    
    
    
    {#each players as player}
        <li>{player} {ranking[player]}<button on:click={() => remJugador(player)}>🚮🚮🚮</button></li>            
    {/each}

    {#if !faltanPlayers}
        <button on:click={generar}>GENERAR</button>
    {/if}
    
    {#each partidos as p}
        <li><button on:click={() => sumar(p.j1, p.j2)}>{p.j1} - {p.j2}</button> vs <button on:click={() => sumar(p.j3, p.j4)}>{p.j3} - {p.j4}</button></li>
    {/each}

</div>

<script>
    let name = '';
    let nPlayer = '';
    let nPlayersEstablecido = false;

    let players = []; // ['Hector','Carlos','Gerard','Alex','Josep','JP','Juan','Dolors'];
    let partidos = [];
    let ranking = {'Hector':0, 'Carlos':0, 'Gerard':0, 'Alex':0,'Josep':0,'JP':0,'Juan':0,'Dolors':0};

    $: faltanPlayers = nPlayer === '' || players.length < nPlayer;

    function addJugador() {
        players.push(name);
        players = players;
        ranking[name] = 0;
        name = '';
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

    function sumar(a, b) {
        if (ranking[a] === undefined) ranking[a] = 0;
        if (ranking[b] === undefined) ranking[b] = 0;
        ranking[a]++;
        ranking[b]++;
    }

    function establecerCantidad(){
        nPlayersEstablecido = true;
    }
</script>

<style>
    .page {
        display: grid;
        justify-items: center;
        font-family:'System UI', 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }

    li {
        list-style-type: "🎾";
        background-color: rgb(89, 243, 148);
        font-size: 25px;
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
    img {
        width: 8em;
        display: block;
    }
</style>