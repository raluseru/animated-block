<script lang="ts">
    import Row from './Row.svelte'
	let visible = false;
    setTimeout(()=>{
        visible = true
    },1000)

    const blueColumnClass = (index:number) => {
        let className= ""
        switch (index) {
            case 0:
            case 2:
                className="size-2"
                break;
            case 1:
                className="size-2 blue"
                break;     
            case 3:
                className="size-4"
                break;
            case 4:
                className="size-6"
            break;
            case 5:
                className="size-8"
            break;
            case 6:
                className="size-7"
            break;
            default:
                className="size-2"
            }
		return className
	};
    const secondHalfColumnClass = (index:number) => {
        let className= ""
        switch (index) {
            case 0:
            case 1:
                className="size-2"
                break;
            case 7:
                className="size-8"
                break;
            default:
                className="size-2 blue"
            }
		return className
	};
    const lastColumnClass = (index:number) => {
        let className= ""
        switch (index) {
            case 0:
            case 4:
                className="size-4"
                break;   
            case 1:
            case 3:
                className="size-5"
                break;            
            case 2:
                className="size-6"
                break;
            case 5:
                className="size-3"
            break;
            case 6:
            default:
                className="size-2"
            break;
            }
		return className
	};
</script>
<div class="container">
    {#if visible}
    <Row last={false}/>
    {/if}
    {#each Array(15) as _, index (index)}
        <div class="row">
            <div class="cell size-3"></div>
            <div class="cell size-2 {index!==7 ?  'blue': ''}"></div>
            <div class="cell {index==6 || index==14 ?  'size-7 blue': index==13 ?  'size-9' : 'size-7'}"></div>
            {#if index < 6 }
            <div class="cell size-6"></div>
            <div class="cell size-{7 - index}"></div>         
            {:else if index==6}   
            <div class="cell size-8"></div>
            <div class="cell size-{7 - index} blue"></div>         
            {:else if index==7}
            <div class="cell size-7"></div>
            <div class="cell size-2 blue"></div>
            {:else }
            <div class="cell size-{14 - index} {index==13 || index==14 ? 'blue': ''}"></div>
            <div class="cell size-2 {index!==13 && index!==14 ? 'blue': ''}"></div>            
                
            {/if}
            
            <div class="cell size-2 {index<6 ?  'blue': index>=8 && index<=12 ? `size-${index-5}`: index==13 ? `size-5`: index==14 ?`size-7`:''}"></div>
            <div class="cell {index>=8 ?  'size-2 blue': blueColumnClass(index)}"></div>
            {#if index == 14 }
                <div class="cell size-5 blue"></div>
                <div class="cell size-2 blue"></div>
            {:else if index > 7 }
                <div class="cell size-2"></div>
                <div class="cell size-2"></div>
                <div class="cell size-2 blue"></div>
            {:else }
                <div class="cell size-2 {secondHalfColumnClass(index)}"></div>
            {/if}
            <div class="cell {lastColumnClass(index)}"></div>
        </div>
    {/each}
    {#if visible}
    <Row last={true}/>
    {/if}
</div>
<style lang="scss">
.container{
    .row {
        .cell {
            transition: .2s all;
            animation: slideLeft 1s calc((var(--delay) - 1) * 100ms - 150ms) reverse both;
            &:hover {
                cursor: pointer;                
            }
            &.blue {
                &:hover{
                    background-color: var(--pink);
                    translate:-100%;
                }
            }
            &:hover:not(.blue){
                    background-color: var(--pear);
                    translate:-100%;
                }
        }
    }
 }

 @keyframes slideLeft {
  0% {
    translate: 0;
  }
  100% {
    translate: 0, 100%;
  }
}
</style>
