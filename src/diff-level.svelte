<script>
import { getContext, setContext } from 'svelte'

const dSelect = getContext('dSelect')
</script>

<div>
    <select name="trivDSelect" id='difficultySelector' bind:value={$dSelect}>
        <option value='a'>
            --Please Select an Option--
        </option>
        <option value='easy'>
            Easy
        </option>
        <option value='medium'>
            Medium
        </option>
        <option value='hard'>
            Hard
        </option>
    </select>
</div>

<style>

</style>