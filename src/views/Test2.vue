<template>
  <div id="app">
    <chartjs-bar v-bind:labels="labels" v-bind:datasets="datasets" v-bind:option="option"></chartjs-bar>
  </div>
</template>

<script>
import axios from "axios"
export default{

  data() {

    return {
      labels :[],
      test:[59,55],
      datasets:[

        {
          data: [],
          backgroundColor: ["Red","Yellow","Purple"]

        }
      ],
        option: {
          title:{
            display:true,
            position:"bottom",
            text:"Fruits"
          }

        }

    }

  },
  mounted(){
      var instance = this.labels;
      var num = this.datasets[0].data;
  axios.get("https://sleepy-reef-53571.herokuapp.com/api/products")
  .then(function(response){
    response.data.data.map((posts) => {
    instance.push(posts.title)
    console.log(posts.title)
    num.push(78)
    })
    
  })
}

}
/* eslint-disable */
</script>
