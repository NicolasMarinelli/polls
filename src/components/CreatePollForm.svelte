<script>
    import { createEventDispatcher } from "svelte";
    import Button from "../shared/Button.svelte";

    let dispacth= createEventDispatcher()
    let fields= {question: "",answerA: "",answerB: ""}
    let errors= {question: "",answerA: "",answerB: ""}

    const sumitHandler= ()=>{
        let valid=true
        
        if(fields.question.trim().length < 5){
            valid= false
            errors.question="questions must be at least 5 characters long"

        } else{
            errors.question=""
        }

        if(fields.answerA.trim().length < 1){
            valid= false
            errors.answerA="answerA Cannot be empty"

        } else{
            errors.answerA=""
        }

        if(fields.answerB.trim().length < 1){
            valid= false
            errors.answerB="answerB Cannot be empty"

        } else{
            errors.answerB=""
        }

        //add new poll 

        if(valid){
            let poll = {...fields, votesA:0,votesB:0, id: Math.random() }
            dispacth("add",poll)
        }
    }

</script>

<form on:submit|preventDefault={sumitHandler}>
    <div class="form-field">
        <label for="question">POLL Question:</label>
        <input type="text" id="question" bind:value={fields.question}>
        <div class="error">{errors.question}</div>
    </div>
    
    <div class="form-field">
        <label for="answer-A">Answer A</label>
        <input type="text" id="answer-A" bind:value={fields.answerA}>
        <div class="error">{errors.answerA}</div>
    </div>
    
    <div class="form-field">
        <label for="answer-A">Answer B</label>
        <input type="text" id="answer-B" bind:value={fields.answerB}>
        <div class="error">{errors.answerB}</div>
    </div>
    <Button type="secondary" flat= {false} >Add Poll</Button>
</form>

<style>
    form{
        width: 400px;
        margin: 0;
        text-align: center; 

    }

    .form-field{
        margin: 18px auto
    }

    input{
        width: 100%;
        border-radius: 6px;
    }
    label{
        margin: 10px auto;
        text-align: left;
    }
    .error{
        font-weight: bold;
        font-size: 12px;
        color: #d91b42;
    }

</style>