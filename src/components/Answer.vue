<template>
    <div v-if="!doneplaying">
        <h3>How many cats did you count?</h3>
        <input type="number" placeholder="type the count number (only numbers)" v-model="answeruser">
        <button @click="submitAnswer">Check my answer</button>
    </div>
    
    <h2 v-if="doneplaying"><b>Please hard refresh the page to play again!</b></h2>
</template>


<script>
export default {
    setup() {
        
    },

    methods: {
        submitAnswer: function(){
        
           if(this.total_cats_answer === this.answeruser){
               alert("CONGRATS! HOORAYY! CORRECT ANSWER, NICE JOB!");
           }else{
               alert("Wrong Answer :( It was "+ this.total_cats_answer);
           }
           this.doneplaying = true;
           
        }
    },

    data(){
        return {
            answeruser: null,
            doneplaying: false
        }
    },

    props: ['isGivingAnswers', 'total_cats_answer']
}
</script>