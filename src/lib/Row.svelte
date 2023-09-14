<script lang="ts">
 import { fly } from 'svelte/transition';
 export let last;
 let yValue = last ? -200 : 200;
</script>
<div class="row" transition:fly={{ y: yValue, duration: 2000 }}>
        <div class="cell size-3" ></div>
        <div class="cell size-2"></div>
        <div class="cell size-7"></div>
        <div class="cell size-6"></div>
        <div class="cell size-10"></div>
        <div class="cell size-10"></div>
</div>  
