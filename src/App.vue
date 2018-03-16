<template>
  <div class="app" :style="style">
      <section class="header">
        <form action="">
          <fieldset>
            <legend>Letras y numeros</legend>
            <label class="toggle">
              <input type="checkbox" v-model="printLetras">
              <span>Imprimir letras</span>
            </label>
            <label class="toggle">
              <input type="checkbox" v-model="printNumeros">
              <span>Imprimir numeros</span>
            </label>
          </fieldset>
          <fieldset >
            <legend>Frase</legend>
            <label>
              <input type="text" v-model="sentence" placeholder="Texto de la frase">
              <input max="10" type="number" v-model="timesToWriteTheSentence">
            </label>
          </fieldset>
          <fieldset>
            <legend>Parrafo</legend>
            <div><input type="text" v-model="titlep" placeholder="Título del parrafo" /></div>
            <div><textarea placeholder="Contenido del parrafo" v-model="p" cols="100" rows="10"></textarea></div>
          </fieldset>
          <fieldset>
            <label>
              <legend>Tamaño letra</legend>
              <input type="number" min="30" max="45" v-model="fontSize">
            </label>
          </fieldset>
        </form>
      </section>
      <main>
        <h1>Hoja de practica</h1>
        <section v-if="printLetras">
          <h2>Letras</h2>        
          <p><span class="dotted-font" v-for="(letra, index) in letras" :key="index">{{letra}}</span></p>
        </section>
        <section v-if="printNumeros">
          <h2>Letras</h2>        
          <p><span class="dotted-font" v-for="(numero, index) in numeros" :key="index">{{numero}}</span></p>
        </section>
        <section v-if="timesToWriteTheSentence > 0">
          <h2>Escribir la frase <i>'{{sentence}}'</i> {{timesToWriteTheSentence}} {{timesToWriteTheSentence == 1 ? 'vez' : 'veces'}}</h2>        
          <p class="dotted-font" v-for="i in Number(timesToWriteTheSentence)" :key="i">{{sentence}}</p>
        </section>
        <section v-if="paragraph">
          <h2>Escribir este parrafo ({{titlep}})</h2>
          <p class="dotted-font" v-html="paragraph"></p>
        </section>
      </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      fontSize: 40,
      letras: 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz',
      printLetras: false,
      numeros: '0123456789',
      printNumeros: false,
      sentence: 'El perro de mi casa tiene hambre',
      timesToWriteTheSentence: 0,
      titlep: '',
      p: 'mklmkmlkml'
    }
  },
  computed: {
    paragraph: {
      set(value) {this.p = value},
      get() {return this.p.replace(/\n/g, "</br>")}
    },
    style() {
      return {
        fontSize: this.fontSize + 'px'
      }
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0px;
  padding: 0px;
}
.header {
  background: lightgrey;
  padding: .25em;
  border-bottom: 1px solid;
  position: absolute;
  top: -47vh;
  width: 100vw;
  transition: all .5s;
  &:hover {
    top: 0vh;
  }
}
@font-face {
    font-family: 'kg-primary-dots';
    src: url('../static/kg_primary_dots/KGPrimaryDots.ttf');
}

.dotted-font {
  font-family: 'kg-primary-dots';
}

.header *, h1, h2 {
  font-size: initial;
} 

main {
  margin-top: 2em;
}

@media print {
  .header {
    display: none;
  }
  main {
    margin: 0px;
  }
  h1 {
    font-size: 1em;
  }  
  h2 {
    font-size: .86em;
  }
}

fieldset {
  margin: 1em;
  &:first-child {
    margin-top: 0px;
  }
}

.toggle {
  & > input {
    display: none;
    &:checked + span {font-weight: bold;}
  }
  & > span {cursor: pointer; text-decoration: underline dotted blue;}
}

</style>
