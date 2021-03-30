<script>
    import { getContext, setContext, onMount } from 'svelte'

    const triviaCatApi = 'https://opentdb.com/api_category.php'
    const cSelect = getContext('cSelect')
    let categoryValues = []
    $: cUpdate = cSelect

    onMount(() =>{
    fetch(triviaCatApi).then(res =>{
        console.log(res)
        return res.json()
    }).then( values =>{
        console.log('This is the Values then')
        console.log(values)
        categoryValues = values.trivia_categories
    })
    })
</script>

<div>
    <select name="trivCSelect" id='categorySelector' bind:value={$cSelect} on:blur={() => setContext('cSelect', cUpdate)}>
        <option value=''>
            --Please Select an Option--
        </option>
        {#each categoryValues as category, index }
            <option value={category.id}>
                {category.name}
            </option>
        {/each}
    </select>
</div>

<style>

</style>