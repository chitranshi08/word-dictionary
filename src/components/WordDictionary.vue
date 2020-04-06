<template>
    <div>
        <h2>Word Dictionary</h2>
        <input @input="hideResult" @keyup.enter="getValue" type="text" v-model="enterWord" placeholder="Please enter word"/>
        <div v-show="inCorrectWord" class="error">Can't find definition, please try again</div>
        <div v-show="getDefinitions" class="container">
            <div class="definition"><strong>Definition - </strong>{{getDefinitions}}</div>
            <img v-show="getImage" :src="getImage" alt="">
        </div>
        <div v-show="showLoader" class="loader">
          <img src="../assets/loader.gif" alt="">
        </div>
    </div>
</template>
<script>
export default {
    name: 'WordDictionay',
    data: () => ({
        enterWord: null,
        getDefinitions: null,
        getImage: null,
        inCorrectWord: false,
        showLoader:false
    }),
    methods: {
        getValue: function() {
            var word = this.enterWord
            word = word.toLowerCase()
            this.showLoader = true;
            fetch(`https://owlbot.info/api/v4/dictionary/${word}`, {
                    headers: {
                        "Authorization": "Token 5dcd0054c090f43be5f4e685d55d9254046f077b"
                    }
                })
                .then((response) => { return response.json() })
                .then((response) => {
                    console.log(response)
                    this.getDefinitions = response.definitions[0].definition
                    this.getImage = response.definitions[0].image_url
                })
                .catch((error) => {
                    this.inCorrectWord = true
                })
                .finally(() =>{
                  this.showLoader = false
                })
        },
        hideResult() {
            this.getImage = null
            this.getDefinitions = null
            this.inCorrectWord = false
        }
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

input {
    font-size: 20px;
    padding: 10px;

}

.speechType {
    font-size: 40px;
    font-weight: bold;
}

.definition {
    height: 50px;
}

.speechType,
.definition {
    margin-top: 100px;
}

.container {
    display: flex;
    justify-content: space-around;
    color: white;
    font-size: 20px;
}

.error {
    color: red;
    margin-top: 25px;
}

h2 {
    color: white;
    font-weight: bold;
    font-size: 60px;
}
.loader{
  height: 100vh;
  width:100vw;
  position: fixed;
  top:0;
  left:0;
  background-color: rgba(255,255,255,0.6);
  display: flex;
  justify-content: center;
  align-items: center;

}
</style>