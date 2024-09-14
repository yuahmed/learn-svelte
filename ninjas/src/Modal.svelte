<!-- a popup -->

<script>
  export let showModal = false;
  export let isPromo = false;
</script>

{#if showModal}
  <!-- fyi, backdrop takes up the entire screen; z=1 -->
  <div class="backdrop" class:promo={isPromo} on:click|self>
    <div class="modal">
      <slot name="title"></slot>
      <slot></slot>
    </div>
  </div>
{/if}

<style>
  .backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.8);
  }

  .modal {
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;
    text-align: center;
    background: white;
  }

  .promo .modal {
    background: crimson;
    color: white;
  }
</style>
