<script>
    import CategorySelect from './category-select.svelte'
    import DiffSelect from './diff-level.svelte'
    import QCorrectWrong from './q-correct-wrong.svelte'
    import T_Questions from './trivia-questions.svelte'
    import SelectContext from './select-context.svelte'
</script>

<main>
    <section>
        <h1>
        Svelte Trivia App
        </h1>
        <p>This is a basic trivia app built using Svelte. Please select a category to begin.</p>
    </section>
    <section class='triviaMain'>
        <SelectContext>
            <CategorySelect></CategorySelect>
            <DiffSelect></DiffSelect>
            <QCorrectWrong></QCorrectWrong>
            <T_Questions></T_Questions>
        </SelectContext>
    </section>
</main>

<style type="text/scss">
    h1 {
            color: #ff3e00;
            text-transform: uppercase;
            font-size: 4em;
            font-weight: 100;
        }

    section{
        p{
            font-size: 1.4rem;
        }
    }
</style>