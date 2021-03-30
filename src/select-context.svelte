<script>
    import { setContext } from 'svelte'
    import { writable } from 'svelte/store'

    let key = {initialValue: 0, nullValue: null}

    let keyStore_qRight = writable(key)
    let keyStore_qWrong = writable(key)
    let keyStore_cSelect = writable(key)
    let keyStore_dSelect = writable(key)


    $: keyStore_qRight.set(key.initialValue)
    $: keyStore_qWrong.set(key.initialValue)
    $: keyStore_cSelect.set(key.nullValue)
    $: keyStore_dSelect.set(key.nullValue)

    setContext('qRight', keyStore_qRight)
    setContext('qWrong', keyStore_qWrong)
    setContext('cSelect', keyStore_cSelect)
    setContext('dSelect', keyStore_dSelect)
</script>
<slot></slot>