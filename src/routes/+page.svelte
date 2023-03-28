<div class ='page'>

    <img src='logo.jpg' alt=''/>    
    <h1>Torneo padel DAW</h1>

    {#if nPlayersEstablecido === false}
        <input bind:value={nPlayer} size=4/>
        <button on:click={establecerCantidad}>CANTIDAD JUGADORES</button>
    {/if}

    {#if faltanPlayers && nPlayersEstablecido}
        <input bind:value = {name}/>
        <button on:click={addJugador}>ADD a {players.length+1} de {nPlayer}</button>
    {/if}
    
    
    <ol>
        {#each players as player}
            <li class="rank"><span class="name">{player}</span><span class="wins">{ranking[player]}</span><button on:click={() => remJugador(player)}>🚮</button></li>            
        {/each}
    </ol>

    {#if !faltanPlayers}
        <button on:click={generar}>GENERAR</button>
    {/if}
    
    {#each partidos as p}
        <li class="partido"><button on:click={() => sumar(p.j1, p.j2)}>{p.j1} - {p.j2}</button> vs <button on:click={() => sumar(p.j3, p.j4)}>{p.j3} - {p.j4}</button></li>
    {/each}

</div>

<script>
    let name = '';
    let nPlayer = 8;
    let nPlayersEstablecido = true;

    let players = ['Hector','Carlos','Gerard','Alex','Josep','JP','Juan','Dolors'];
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
        ranking[a]++;
        ranking[b]++;

        players = players.sort((a,b) => ranking[b] - ranking[a]);
    }

    function establecerCantidad(){
        nPlayersEstablecido = true;
    }
</script>

<style>
    .page {
        background: #bdc3c7;  /* fallback for old browsers */
        background: -webkit-linear-gradient(to top, #2c3e50, #bdc3c7);  /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(to top, #2c3e50, #bdc3c7); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

        padding-bottom: 4em;
        display: grid;
        justify-items: center;
        gap: 1em;
        font-family:'System UI', 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    }

    li {
        list-style-type: "🎾";
        background: #f12711;  /* fallback for old browsers */
        background: -webkit-linear-gradient(to right, #f5af19, #f12711);  /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(to right, #f5af19, #f12711); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

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

    ol {
        place-self: center stretch;
    }

    ol li.rank {
        display: grid;
        grid-template-columns: 4fr 1fr 1fr;
    }

</style>