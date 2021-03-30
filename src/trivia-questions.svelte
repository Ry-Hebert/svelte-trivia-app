<script>
import { getContext } from 'svelte'
import CategorySelect from './category-select.svelte'

let cSelect = getContext('cSelect')
let dSelect = getContext('dSelect')
const aCorrect = getContext('qRight')
const aWrong = getContext('qWrong')

$: playerQuestions = []
$: qReturned = false

const fQuestions = async () =>{
    const connectString = `https://opentdb.com/api.php?amount=10&category=${$cSelect}&difficulty=${$dSelect}&type=multiple`
    const fRes = await fetch(connectString)
    let resJson = await fRes.json()
    
    let finalRes = await resJson.results

    console.log(finalRes)
    let tempQuestions = finalRes
    playerQuestions = tempQuestions.map( element =>{
        let newArray = []
        newArray.push(element.correct_answer)
        newArray.push.apply(newArray, element.incorrect_answers)
        
        let tempObj = {
            correct_answer: element.correct_answer,
            incorrect_answers: element.incorrect_answers,
            all_answers: newArray,
            question: element.question
            .replace(/&amp;/g, '&')
            .replace(/&quot;/g, '"')
            .replace(/&ldquo;/g, '"')
            .replace(/&rdquo;/g, '"')
            .replace(/&rsquo;/g, `'`)
            .replace(/&hellip;/g, `…`)
            .replace(/&#039;/g, `'`),
        }
        console.log(tempObj.all_answers)
        return tempObj
    })
    qReturned = true

}

const isCorrect = (tAnswer, currAnswer, index) =>{
    console.log(index)
    console.log(index.value)
    if(index.value == undefined){
        index.value = false
        $aWrong = $aWrong + 1
    }
    console.log('This is the current answer: ')
    console.log(currAnswer)
    console.log(index.value)
    if(currAnswer != tAnswer && index.value == true){
        $aCorrect = $aCorrect - 1
        $aWrong = $aWrong + 1
    }
    if(currAnswer == tAnswer && index.value != true){
        $aCorrect = $aCorrect + 1
        $aWrong = $aWrong - 1
    }
}

</script>

<div>
    <div>
        {#if $cSelect != null && $dSelect != null}
            <button on:click={fQuestions}>Start</button>
        {/if}
    </div>
    {#if qReturned != false}
        {#each playerQuestions as { correct_answer, incorrect_answers, all_answers, question}, i}
            <div class="questionBlock" id={"rightWrong" + i}>
                <h3>{question}</h3>
                <select on:input={isCorrect(correct_answer, this.value, document.querySelector(`#rightWrong${i}`))}>
                    <option value=null>Select an Answer</option>
                    {#each all_answers as an_answer}
                        <option value={an_answer}>{an_answer}</option>
                    {/each}
                </select>
            </div>
        {/each}
    {/if}
</div>

<style>
    .questionBlock{
        margin-bottom: 2rem;
    }
</style>