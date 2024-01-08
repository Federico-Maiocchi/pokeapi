<script>


import axios from 'axios';


export default {
    

    data() {
      return {
        poke:[]
        
        

      }
    },

    created() {
        axios.get('https://pokeapi.co/api/v2/pokemon?limit=10&offset=0')
        .then((res)=>{
          console.log(res.data.results)

          axios.all(res.data.results.map(result => axios.get(result.url)))
            .then(allDatas => {
              allDatas.map(allData => {
                const data = allData.data;
                console.log(data.sprites);
              })
            })

          this.poke = res.data.results;


        })
    },

    methods: {
        
        
    },

    mounted() {
    // console.log(this.cards)
    // console.log(store)
    }


    }



</script>

<template>
  <h1>cose</h1>

  <div class="container">
    <div class="row">
        <ul>
          <li v-for="(item , index) in poke" :key="index">
            {{ item.name }}
            <img :src="item.url" alt="">
          </li>
          
        </ul>
    </div>
  </div>



</template>

<style scoped>



</style>
