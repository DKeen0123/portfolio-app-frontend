<script>
  export let header;
  export let innerText;
  import { fly, fade } from "svelte/transition";
  let visible = false;

  const handleClick = () => {
    visible = !visible;
  };
</script>

<button on:click={handleClick} class="btn-description">
  <p>{header}</p>
  <svg
    version="1.1"
    class={visible ? 'rotate' : ''}
    id="chevron-right"
    x="0px"
    y="0px"
    viewBox="0 0 256 256">
    <g>
      <g>
        <polygon
          points="79.093,0 48.907,30.187 146.72,128 48.907,225.813 79.093,256
          207.093,128 " />
      </g>
    </g>
  </svg>
</button>
{#if visible}
  <div transition:fade id="description">
    <p transition:fly={{ y: -200, duration: 350 }}>
      {@html innerText}
    </p>
  </div>
{/if}

<style>
  #description {
    background-color: #f1f1f1;
    padding: 16px;
    overflow: hidden;
    /* margin-top: 2px; */
  }

  #chevron-right {
    fill: white;
    height: 18px;
    width: 18px;
    transition: transform 0.25s;
  }

  .rotate {
    transform: rotate(90deg);
  }

  .btn-description {
    outline: none;
    display: flex;
    justify-content: space-between;
    width: 100%;
    padding-left: 16px;
    padding-right: 16px;
    align-items: center;
    font-size: 14px;
    color: white;
    background-color: #777;
    cursor: pointer;
    border: none;
  }
</style>
