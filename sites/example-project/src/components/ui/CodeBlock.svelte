<script>
  export let source;
  export let copyToClipboard = false;
  import Copy from "./Deployment/CopyIcon.svelte";
  import Success from "./Deployment/CopySuccessIcon.svelte";
  let copied = false;

  const toggleCopied = function () {
    copied = false;
  };

  async function copy(){
    try {
        await navigator.clipboard.writeText(source);
        copied = true;
        setTimeout(toggleCopied, 1500);
    } catch (e) {}
  };
</script>

<pre>
<code>{#if source}{source}
{:else}<slot />
{/if}
</code>
{#if copyToClipboard}
<button
  type="button"
  class="container"
  class:copied
  on:click={() => {
    if (source !== undefined) {
      copy(source);
    }
  }}>
{#if copied}
<Success color=var(--green-500)/>
{:else}
<Copy/>
{/if}
</button>
{/if}
</pre>

<style>
  pre {
    overflow: scroll;
    background: var(--grey-100);
    border: 1px solid var(--grey-200);
    border-radius: 5px;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: space-between;
  }

  pre code {
    display: block;
    background: none;
    border: none;
    padding: 0.8em 0.8em;
    color: var(--grey-900);
    font-size: 0.7em;
  }

  pre button.container {
        opacity: 0;
        transition: all 200ms ease-in-out;
        box-sizing: border-box;
        background-color: var(--grey-100);
        border-radius: 4px 4px 4px 4px;
        border: 1px solid var(--grey-300);
        padding: 0.25em 0.35em 0.25em 0.35em;
        color: var(--grey-300);
        size: 0.75em;
        width: 2.4em;
        height: 2.4em;
        cursor: pointer;
        user-select: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        margin: 0.5em;
        display: flex;
        align-items: center;
        justify-content: center;
    }



  pre:hover button.container {
        opacity: 1;
        transition: all 200ms ease-in-out;
        box-sizing: border-box;
        background-color: var(--grey-100);
        border-radius: 4px 4px 4px 4px;
        border: 1px solid var(--grey-300);
        padding: 0.25em 0.35em 0.25em 0.35em;
        color: var(--grey-300);
        size: 0.75em;
        width: 2.4em;
        height: 2.4em;
        cursor: pointer;
        user-select: none;
        -webkit-user-select: none;
        -moz-user-select: none;
        margin: 0.5em;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    pre button.container:hover {
        border-color: var(--grey-500);
        background-color: var(--grey-100);
        color: var(--grey-500);
        transition: all 200ms ease-in-out;
    }
    


    pre button.container.copied {
        border-color: var(--grey-500);
        background-color: var(--grey-100);
        color: var(--green-500);
        transition: all 200ms ease-in-out;
    }
</style>


