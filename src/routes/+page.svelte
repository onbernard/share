<script>
    import Chord from "$lib/Chord.svelte";
    import { data, names, colors, calls } from "$lib/data.js"
    import Table from "$lib/Table.svelte"
</script>

<Chord {data} {names} {colors} />
<Table />