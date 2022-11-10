# Pokedex.
PracticaPokedex.

<!--HTML-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pokedex.</title>
    <link rel="stylesheet" href="./poke.css">
</head>
<body>
    <div class="container">
        <h1>Pokedex</h1>
        <ol id="pokedex"></ol>
    </div>

    <script src="./poke.js"></script>
</body>
</html>

/*CSS*/
body{
    background-color: skyblue;
    color: black;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}

.container{
    padding: 50px;
    margin: 0 auto;
}

h1{
    text-transform: uppercase;
    text-align: center;
    font-size: 55px;
}

#pokedex{ /*Para id del elemento.*/
    display: grid; /*En forma de tabla*/
    grid-template-columns: repeat(auto-fit, minmax(320px,1fr));
    grid-gap: 20px;
    padding-inline-start: 0;
}

.card{
    list-style: none;
    padding: 40px;
    background-color: azure;
    color: black;
    text-align: center;
}

.card:hover{
    background-color: blue;

}

//JS.
const pokedex = document.getElementByld('pokedex');

const getPokemon = () => {
    const promesas = [];
    for (let i=1; i <= 150; i++ ) {
        const url = `https://pokeapi.co/api/v2/pokemon/${i}` //"'" Son para concatenar $(i)
        promesas.push(fetch(url).then(res => res.json()));
    }

    Promise.all(promesas).then(resultados => {
        const pokemons = resultados.map((result) => ({
            name : result.name,
            id : result.id,
            img : result.sprites.front_default,
            type : result.types.map(type => type.type.name)
        })); 
        showPokemon(pokemons);
    });
}

const showPokemon = (pokemon)=>{
    console.log(pokemon);
    const pokemonHTML = 
    pokemon.map ((poke)=>{
        `<li class = "card">`
            `<img class="card-img" src="${poke.img}"/>`
            `<h2 class="card-subtitle">${poke.image}</h2>`
            `<p class="card-text">${poke.type}</p>`
        `</li>`
    }).join('');
    pokedex.innerHTML=pokemonHTML;    
}
getPokemon();
