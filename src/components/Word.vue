<template>
  <div class="container-fluid col-12">
    <form class="pt-4" @submit.prevent="submitForm">
      <div class="row offset-4">
        <div class="col-auto">
          <input type="text" readonly class="form-control-plaintext" id="staticEmail2" value="Ingrese su word">
        </div>
        <div class="col-auto">
          <input type="text" class="form-control" v-model="userData.word" id="inputword" placeholder="word">
        </div>
        <div class="col-auto">
          <input type="text" class="form-control" v-model="userData.wordCompare" id="inputwordCompare" placeholder="word">
        </div>
        <div class="col-auto">
          <button type="submit" class="btn btn-primary mb-3">Enviar</button>
        </div>
      </div>
    </form>
  </div>
  <div class="container">
    <table class="table">
      <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Palabra</th>
        <th scope="col">Palabra a comparar</th>
        <th scope="col">Anagrama</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(item, index) in wordData" :key="index">
        <th scope="row">{{item.id}}</th>
        <td>{{item.word}}</td>
        <td>{{item.word_inv}}</td>
        <td v-if="item.anagrams == 0">No</td>
        <td v-if="item.anagrams == 1">Si</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Word',
  props: {
    msg: String
  },
  data() {
    return {
      userData: {
       word: '',
       wordCompare: '',
       anagrams: 0,
      },
      wordData: [],
      message: 'La word es: ',
    }
  },
  mounted() {
    this.getWords();
  },
  methods:{
    getWords: function (){
      axios.get('http://127.0.0.1:8000/api/word', {
        headers: {
          'Authorization': 'Bearer' + 'Your Bearer Password',
          "Content-Type": "application/json",
        }
      })
          .then(response => {
            this.wordData = response.data
            this.getWords();
          })
          .catch(function (error) {
            console.log(error);
          });
    },
    submitForm: function (){
      let word = this.userData.word.toLowerCase();
      let wordCompare = this.userData.wordCompare.toLowerCase();
      word = word.split("");
      wordCompare = wordCompare.split("");
      word = word.sort();
      wordCompare = wordCompare.sort();
      word = word.join("");
      wordCompare = wordCompare.join("");
      if(word === wordCompare){
        alert('is anagram');
        this.userData.anagrams = 1;
      }
      this.saveWord(this.userData.word, this.userData.wordCompare, this.userData.anagrams)
    },
    saveWord: function (word , wordCompare, anagrams){
      let data = {
        word: word,
        wordCompare : wordCompare,
        anagrams : anagrams
      };
      axios.post('http://127.0.0.1:8000/api/word', data, {
        headers: {
          'Authorization': 'Bearer' + 'Your Bearer Password',
          "Content-Type": "application/json",
        }
      })
          .then(response => {
            this.datas = response.data
            console.log(response.data);
            alert(response.status);
          })
          .catch(function (error) {
            console.log(error);
          });
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
