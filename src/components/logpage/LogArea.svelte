<script>
  import { afterUpdate, tick } from 'svelte';
  import { logUpdate } from '../../Stores';
	
	let list = [];
	let element;

  let needsUpdate = true;

  logUpdate.subscribe(v => {
    needsUpdate = v;
  });

  const updateList = () => {
    console.log(needsUpdate)
    if (needsUpdate) {
      fetch('http://localhost:8000/api/v1/log/get?key=' + sessionStorage.getItem('auth'), {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      }).then(res => res.json()).then(res => {
        list = res.logs;
        logUpdate.set(false);
      });
    }
  }
	
	// Either afterUpdate()
	afterUpdate(() => {
		console.log("afterUpdate");
		if(list) scrollToBottom(element);
  });
	
	$: if(list && element) {
		scrollToBottom(element);
	}

  const scrollToBottom = async (node) => {
    node.scroll({ top: node.scrollHeight, behavior: 'smooth' });
  }; 
	
	function addLine(text) {
		list.push(text);
		list=list;
	}

  let clear;
  $: {
    clearInterval(clear)
    clear = setInterval(updateList, 500)
  }

</script>

<div bind:this={element} style="height:550px; width:100%; overflow:auto;">
	{#each list as item}
    <p>{item}</p>
  {/each}
</div>

<style lang=scss>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  p {
    font-size: 14px;
    color: $white;
    font-family: 'Roboto Mono', monospace;
  }

  textarea {
    width: 100%;
    height: 550px;
    background-color: $darkest;
    font-size: 14px;
    color: $white;
    border: none;
    resize: none;
    font-family: 'Roboto Mono', monospace;
  }

  .noselect {
   cursor: default;
   -webkit-user-select: none;
   -webkit-touch-callout: none;
   -khtml-user-select: none;
   -moz-user-select: none;
   -ms-user-select: none;
   -o-user-select: none;
}

.noselect:focus {
   outline: none;
}

</style>

