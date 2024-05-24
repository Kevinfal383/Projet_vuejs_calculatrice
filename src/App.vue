<template>
  <h1>CALCULATRICE 🤔🤓</h1>
  <div class="corps">
    <div class="calcul">
      <p>{{ calcul }}</p>
    </div>
    <div class="clavier">
      <div class="nombre">
          <div class="nbr" v-for="n in [1,2,3,4,5,6,7,8,9,0,'.']" :key="n">
            <button @click="ajouterNombre(n)">{{ n }}</button>
          </div>
        </div>
      <div class="operateur">
        <div class="delete">
          <button @click="supprimer()">Del</button>
        </div>
        <div class="delete">
          <button @click="supprimerTous()">C</button>
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
        if (op === '='){
          this.evaluerExpession();
        } 
        else {
          this.calcul = this.calcul + op;
        }
      },
      /*evaluerExpession(){
        try {
        // Utilisation de Function constructor au lieu de eval() pour évaluer l'expression
        this.calcul = String(Function('"use strict";return (' + this.calcul + ')')());
      } catch (e) {
        this.calcul = "Erreur";
      }
      }*/
      //La fonction eval en JavaScript évalue une chaîne de caractères comme du code JavaScript et retourne le résultat de cette évaluation
      evaluerExpession(){
        try {
          this.calcul = String(eval(this.calcul));
        } catch (e) {
          this.calcul = "Syntaxe erreur";
        }
      },
      supprimer(){
        if (this.calcul.length > 1) {
          this.calcul = this.calcul.slice(0, -1).trim();
        } else {
          this.calcul = "0";
        }
      },
      supprimerTous(){
        this.calcul = "0";
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
          button{
            font-size: 40px;
          }
        }
      }
      .operateur{
        display: grid;
        grid-template: repeat(7, 50px) / repeat(1, 100px);
        .op , .delete{
          border: 3px solid white;
          text-align: center;
          button{
            padding-top: 5px;
            font-size: 30px;
          }
        }
      }
    } 
  }
</style>