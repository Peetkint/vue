<template>
  <div > 
    <h1 v-if="show">{{name}}</h1>
    <v-btn color="success" @click="show= !show">SHOW</v-btn>
    <v-btn color="success" @click="callAlert()">Alert</v-btn>
        <v-btn color="success" @click="setlocal(item)">SETUSER</v-btn>

   
    <v-row justify="center">
        <v-col col-s="12" v-for="(item,index) in imgset" :key="index">
            <v-card width="300"  >
                <v-img 
                :src="item.imglink"
                aspect-ratio="1">
                </v-img>
                <v-card-title primary-title>
                {{item.name}}
                </v-card-title>
                <v-btn color="success" @click="callAlertParams(item.name)">Alert</v-btn>
            </v-card>
        </v-col>
        <v-col cols="12">
            <h1>{{id}}</h1>
            <v-text-field
            name="id"
            label="id"
            id="id"
            v-model="item">
                
            </v-text-field>
            <v-btn color="success" @click="callAlertParams(id)">Alert</v-btn>
        </v-col>
        <v-col cols="12">
            <simcom :id="id" @callAertParam="callAertParam"/>
        </v-col>

      
    </v-row>

  </div>
</template>
<script>

import simcom from '../components/SimCom.vue'
import {EventBus} from '@/EventBus'
import Swal from "sweetalert2";



localStorage.setItem("Firstnam", "Phichet");
localStorage.setItem("Lastname", "Mongkon");
export default{
    components:{
        simcom,
     
    },
    data() {
        return {
            id:'',
            name:'Phichet',
            show: false,
            imgset: [{name:'แมวเป้า',imglink:'https://scontent.fbkk27-1.fna.fbcdn.net/v/t39.30808-6/288682938_2655977067880700_7428804885472758011_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=5f2048&_nc_ohc=dXK-gyYonbYQ7kNvgGlP5-I&_nc_ht=scontent.fbkk27-1.fna&oh=00_AYCDe2Esg4BtvgZ1I_6HWQ57r04mkIdT6286spkOP4veUg&oe=666DCE13'},
                     {name:'แมววัด' ,imglink:require('../assets/download.jpg')}
            ]
        }
    },
    methods:{
        callAlert(){
            alert('ออกไป๊ !!')
        },
        callAlertParams(item){
            alert(item)
        },
        setlocal(item){
            localStorage.setItem("user" , item);
            
            Swal.fire({
                title: (item),
                text: "เรียบร้อยค้าบบบ !",
                icon: "success"
});
        }

        
    },
    mounted(){
        EventBus.$on('callAertz',this.callAlert)
    },
    beforeDestroy(){
        EventBus.$off('callAertz',this.callAlert)
    }
}

</script>
