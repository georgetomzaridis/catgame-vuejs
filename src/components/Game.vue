<template>
    <img :src="gameimgsrc" v-if="!isGivingAnswers"/>

    <div style="margin: 2em 0;">
        <Answer v-if="isGivingAnswers" :isGivingAnswers="isGivingAnswers" :total_cats_answer="total_cats_answer"/>
    </div>
</template>

<script>

import Answer from './Answer.vue';

export default {

    
    components: {
        Answer
    },
    setup() {
    
    },

    data(){
        return {
            gameimgsrc: "getready.jpg",
            isGivingAnswers: false
        }
    },

    props: ['image_given', 'switch_time', 'isPlaying', 'total_cats_answer'],

    methods: {
        loadGame: function(){
            if(this.isPlaying){
                console.log(this.image_given);
                
               
            
                let this_access = this;
            
                let k_access = 0;
                let final_total_length = this.image_given.length;
                let change_process = setInterval(function() {  
                    
                    console.log("cats-count/"+ this_access.image_given[k_access]);
                    console.log("TOTAL LENGTH >> " + final_total_length);
                    console.log("K >>" + k_access);
                    this_access.gameimgsrc = "cats-count/"+ this_access.image_given[k_access];
                    k_access += 1;
                    if(k_access > final_total_length){
                        console.log("DONE!");
                        this_access.gameimgsrc = "getready.jpg";
                        setTimeout(function() {
                        this_access.isGivingAnswers = true;
                        clearInterval(change_process);
                        }, 2500)
                        
                    }
                    //
                }, (this.switch_time * 1000));

                //console.log("DONE!");

                //this.gameimgsrc = "cats-count/4.jpg"
            }
        }
    },

    beforeMount(){
        this.loadGame()
        
    } 
}
</script>
