<script>
import { getContext, setContext } from 'svelte'

const aCorrect = getContext('qRight')
const aWrong = getContext('qWrong')
</script>

<div class='score-banner'>
    <div>
        <h3>Correct</h3>
        <h4>{$aCorrect}</h4>
    </div>
    <div>
        <h3>Wrong</h3>
        <h4>{$aWrong}</h4>
    </div>
</div>

<style>
    .score-banner{
        display: grid;
        grid-template-columns: 1fr 1fr;
    }
</style>

