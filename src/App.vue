<template>
  <h1>CALCULATRICE 🤓</h1>
  <div class="corps">
    <div class="calcul">
      <p>{{ calcul }}</p>
    </div>
    <div class="clavier">
      <div class="nombre">
          <div class="nbr" v-for="n in [1,2,3,4,5,6,7,8,9,0]" :key="n">
            <button @click="ajouterNombre(n)">{{ n }}</button>
          </div>
        </div>
      <div class="operateur">
        <div class="delete">
          <button>Del</button>
        </div>
        <div class="op" v-for="op in ['+', '-', '*', '/', '%', '=']" :key="op">
          <button @click="ajouterOperateur(op)">{{ op }}</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
  export default{
    data(){
      return{
        calcul: "0",
      }
    },
    methods:{
      ajouterNombre(n){
        if (this.calcul === "0"){
          this.calcul = String(n)
        } else {
          this.calcul = this.calcul + String(n)
        }
      },
      ajouterOperateur(op){
        this.calcul = this.calcul + String(op)
      }
    }
  }
</script>


<style lang="scss">
  body{
    font-family: sans-serif;
    background: #000;
    color: white;
    h1{
      font-size: 35px;
      text-align: center;
    }
    .calcul{
      border: 5px solid white;
      width: 400px;
      margin: 20px auto 0px;
      height: 100px;
      p{
        font-size: 40px;
        padding-left: 8px;
      }
    }
    .clavier{
      display: flex;
      border: 5px solid white;
      width: 400px;
      margin: 0px auto;
      button{
        font-size: 40px;
        background: #000;
        border: none;
        color: white;
      }
      .nombre{
        display: grid;
        /*4 ligne de 30px et 3 colone de 30px*/ 
        grid-template: repeat(4, 100px) / repeat(3, 100px);
        .nbr{
          border: 3px solid white;
          text-align: center;
          padding-top: 24px;
        }
      }
      .operateur{
        display: grid;
        grid-template: repeat(7, 57.1px) / repeat(1, 100px);
        .op , .delete{
          border: 3px solid white;
          text-align: center;
          padding-top: 2px;
        }
      }
    } 
  }
</style>