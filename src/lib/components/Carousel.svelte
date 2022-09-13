<script lang="ts">
import Portrait from "./Portrait.svelte";

    type ImageType = {
        title: string,
        src: string;
    }

    type IPortrait = {name: string, role: string, imageReference: string};

    export let images: IPortrait[]

</script>

<ul class="flex overflow-x-auto gap-6 snap-x snap-mandatory">
    {#each images as { name, role, imageReference }}
        <li class="shrink-0 snap-center">
            <!--<img {name} src={imageReference} alt={name} />-->
            <Portrait {name} {role} {imageReference}></Portrait>
        </li>
    {/each}
</ul>