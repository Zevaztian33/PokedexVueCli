<template>
    <section>
        <div class="container p-3 text-center">
            <div class="row">
                <form @submit.prevent="busqueda" class="mb-2 mx-auto col-12 col-sm-12 col-md-12 col-lg-8 col-xl-8">
                    <div class="input-group">
                        <input v-model="nameId" type="search" class="form-control" placeholder="Ingrese Nombre/Número" aria-label="Search" aria-describedby="button-addon2">
                        <div class="input-group-append">
                            <button class="btn btn-outline-light btn-warning" type="submit" id="button-addon2">Search</button>
                        </div>
                    </div>
                </form>
            </div>
            <div class="row">
                
                <div class="bloque col-12 col-sm-12 col-md-12 col-lg-4 col-xl-4">
                    <img :src="getImagen" alt="Imagen no ingresada aún" class="text-light">
                </div>

                <div class="bloque2 pt-2 col-12 col-sm-12 col-md-12 col-lg-4 col-xl-4">
                <div id="nombre">{{getNombre}}</div>
                    <hr>
                <div>N° Id: {{getNum}}</div>
                    <hr>
                <div>Tipo:
                    <div class="pb-1 d-inline-block" id="types" v-for="(poke,index) in getTipo" :key="index">
                        <div class="pokeType poke-info" :class="[poke.type.name]">{{poke.type.name}}</div>
                    </div>
                </div>
                    <hr>
                <div>Peso: {{getPeso}} kls. / Altura: {{getAltura}} mts.</div>
                    <hr>
                    <div>Habilidades:</div>
                <div>
                    <p id="skills" class="poke-info pokeSkill bg-success" v-for="(abilities, index) in getHabilidades" :key="index">{{ abilities.ability.name }}</p>
                </div>
                </div>

                <div class="bloque3 pt-2 col-12 col-sm-12 col-md-12 col-lg-4 col-xl-4">
                <table class="table mt-4 table-striped text-center text-warning">
                    <thead>
                        <tr>
                        <th scope="col">STATS:</th>
                        <th scope="col">BASE:</th>
                        </tr>
                    </thead>
                    <tbody class="text-light">
                        <tr>
                        <th scope="row">HP</th>
                            <td>{{getHP}}</td>
                        </tr>
                        <tr>
                        <th scope="row">ATK</th>
                        <td>{{getAtk}}</td>
                        </tr>
                        <tr>
                        <th scope="row">DEF</th>
                        <td>{{getDef}}</td>
                        </tr>
                        <tr>
                        <th scope="row">SpATK</th>
                        <td>{{getSpAtk}}</td>
                        </tr>
                        <tr>
                        <th scope="row">SpDEF</th>
                        <td>{{getSpDef}}</td>
                        </tr>
                        <tr>
                        <th scope="row">Speed</th>
                        <td>{{getSpeed}}</td>
                        </tr>
                    </tbody>
                    </table>
                </div>
            </div>
        </div>        
    </section>
</template>

<script>
    export default {
        name: 'Section',
        data(){
            return{
                nameId: "",
                ficha: {},
            };
        },

        mounted() {
            fetch("https://pokeapi.co/api/v2/pokemon/pikachu")
            .then((captura) => captura.json())
            .then((data) => {
                this.ficha = data;
            });
        },

        methods: {
            busqueda(){
                fetch("https://pokeapi.co/api/v2/pokemon/" + this.nameId)
                .then((captura) => captura.json())
                .then((data) => {
                    this.ficha = data;
                    this.nameId = "";
                })
                .catch((error) => {
                    console.log(error)
                    alert("El nombre o número no es correcto");
                })
            },
        },
        
        computed: {
            getImagen() {
                if (this.ficha.sprites) {
                    return this.ficha.sprites.other['official-artwork'].front_default ? this.ficha.sprites.other['official-artwork'].front_default : this.ficha.sprites.front_default;
                } else {
                    return "";
                }
            },
            getNombre(){
                return this.ficha.name;
            },
            getNum(){
                return this.ficha.id;
            },
            getTipo(){
                return this.ficha.types.slice(0, 2);
            },
            getPeso(){
                return this.ficha.weight/10;
            },
            getAltura(){
                return this.ficha.height/10;
            },
            getHabilidades(){
                return this.ficha.abilities.slice(0, 5);
            },
            getHP(){
                return this.ficha.stats[0].base_stat;
            },
            getAtk(){
                return this.ficha.stats[1].base_stat;
            },
            getDef(){
                return this.ficha.stats[2].base_stat;
            },
            getSpAtk (){
                return this.ficha.stats[3].base_stat;
            },
            getSpDef(){
                return this.ficha.stats[4].base_stat;
            },
            getSpeed(){
                return this.ficha.stats[5].base_stat;
            },
        },
    }
</script>

<style scoped>
    section{
        background-image: url('../assets/fondo4.png');
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        margin: 0;
        padding: 0;
    }

    .bloque{
        width: 300px;
        height: 400px;
        background: black;
        border: 3px solid goldenrod; 
        transform: skew(-5deg);
        overflow: hidden;
    }

    .bloque img{
        width: 100%;
        filter: drop-shadow(0 0 0.75rem white);
    }

    .bloque2{
        width: 300px;
        height: 400px;
        background: white;
        border: 3px solid black; 
        transform: skew(-5deg);
        transition: 1s all ease;
        opacity: 0.8;
        text-transform: capitalize;
        font-size: 20px;
        font-weight: bold;
    }

    #nombre{
        font-size: 34px;
        font-weight: bold;
    }

    .bloque2:hover{
        opacity: 1;
    }

    .bloque3{
        width: 300px;
        height: 400px;
        background-color: darkblue;
        border: 3px solid yellowgreen; 
        transform: skew(-5deg);
        transition: 1s all ease;
        opacity: 0.8;
        text-transform: capitalize;
    }

    .bloque3:hover{
        opacity: 1;
    }

.poke-info {
    display: inline-block;
    margin-right: 2px;
    
}
  
.pokeType{
    padding: 5px 30px;
    color: black;
    border: 2px solid black;
    border-radius: 25px;
    font-size: 16px;
    margin: 5px;
    font-weight: 700;
}

.pokeSkill{
    padding: 5px 10px;
    color: white;
    border: 2px solid black;
    border-radius: 25px;
    font-size: 12px;
    margin: 5px;
    font-weight: 700;
}

.normal {
    background-color: #a8a878;
  }

  .grass {
    background-color: #78c850;
  }

  .ground {
    background-color: #e0c068;
  }

  .fighting {
    background-color: #c03028;
  }

  .rock {
    background-color: #b8a038;
  }

  .steel {
    background-color: #b8b8d0;
  }

  .fire {
    background-color: #f08030;
  }

  .electric {
    background-color: #f8d030;
  }

  .flying {
    background-color: #a890f0;
  }

  .psychic {
    background-color: #f85888;
  }

  .bug {
    background-color: #a8b820;
  }

  .dragon {
    background-color: #7038f8;
  }

  .water {
    background-color: #6890f0;
  }

  .ice {
    background-color: #98d8d8;
  }

  .poison {
    background-color: #a040a0;
  }

  .dark {
    background-color: #705848;
  }

  .ghost {
    background-color: #705898;
  }

  .fairy {
    background-color: #ffaec9;
  }

</style>