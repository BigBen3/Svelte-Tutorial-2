<script>
   
    export let showModal = false;
    export let isPromo = false;
</script>

{#if showModal}
<!--this div will have an additional class name based on the value of isPromo if it is tru it gets promo if it is false it gets nothing-->
<!--event fowards to the parent which is the app.svelte and then calls it when you define hte modal-->
<!--the self is an event modiffer it makes it so that the click is only called when you click on that specific div-->
<div class="backdrop" class:promo={isPromo} on:click|self>
    <div class="modal">
        <!--sltos are like props but let you pass more data and more complex data -->
    <slot></slot>
 
    </div>
</div>

{/if}


<style>
    .backdrop {
        width: 100%;
        height: 100%;
        position: fixed;
        background: rgba(0,0,0,0.8);
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