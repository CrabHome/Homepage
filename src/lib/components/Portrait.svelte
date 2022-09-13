<script lang="ts">
    export let imageReference: string;
    export let name: string;
    export let role: string;
</script>

<div class="flex relative w-2/5 sm:2/3 md:w-3/4 lg:w-4/5 text-center shadow-xl">
    <img src={imageReference} alt="Portrait image of team member {name}">
    <h2 class="absolute whitespace-nowrap text-3xl text-orange-400 left-1/2 -translate-x-1/2 drop-shadow-2xl">{name}</h2>
    <p class="absolute whitespace-nowrap text-1xl text-orange-400 left-1/2 top-[14%] -translate-x-1/2 ">{role}</p>
</div>

<style>
  
</style>