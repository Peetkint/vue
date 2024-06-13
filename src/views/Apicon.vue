<template>
  <div>
    <h1>API connect</h1>
    <!-- <h1>{{apidata}}</h1> -->
    <v-btn color="seccess" @click="getData()">API   </v-btn>

    <v-col cols="12" v-for="(item,index) in apidata" :key="index">
            <v-card width="300"  >
                <v-img 
                src="https://scontent.fbkk27-1.fna.fbcdn.net/v/t39.30808-6/288682938_2655977067880700_7428804885472758011_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=5f2048&_nc_ohc=dXK-gyYonbYQ7kNvgGlP5-I&_nc_ht=scontent.fbkk27-1.fna&oh=00_AYCDe2Esg4BtvgZ1I_6HWQ57r04mkIdT6286spkOP4veUg&oe=666DCE13"
                aspect-ratio="1">
                </v-img>
                <v-card-title primary-title>
                {{item.product_name}} 
                </v-card-title>
                
            </v-card>
        </v-col>
  </div>
</template>

<script>
import InteractiveCard from '../components/chart.vue';
export default {
    data(){
        return{
            apidata:[]
        }
    },
    methods:{
        getData(){
                this.axios.get('http://localhost:3000/admin').then((response)=>{
                console.log(response.data)
                this.apidata = response.data
            })
        }
    },
    computed:{
        InteractiveCard
    }

}
</script>

<style>

</style>