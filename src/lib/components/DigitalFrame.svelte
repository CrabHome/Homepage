<script lang="ts">
    import Portrait from "@lib/components/Portrait.svelte"
    import { onMount } from "svelte";
    import { fade } from 'svelte/transition'
    import Carousel from "@lib/components/Carousel.svelte";

    type IPortrait = {name: string, role: string, imageReference: string};

    const extraSmallMediaQuery: string = '(max-width: 639.9px)'
    const smallMediaQuery: string = '(min-width: 640px)';
    const mediumMediaQuery: string = '(min-width: 768px)';
    const largeMediaQuery: string = '(min-width: 1024px)';

    const jens = {imageReference: "/portraits/jrsemiportrait.jpg", name: "Jens Rage", role: "dev"}
    const jenszoom = {imageReference: "/portraits/jrportrait.png", name: "Jens Rage", role: "dev"}
    const kajsa = {imageReference: "/portraits/kbsemiportait.jpg",name: "Kajsa Bogen",  role: "CEO"}
    const kajsa2 = {imageReference: "/portraits/kbsemiportait.jpg",name: "Kajsa Bogen",  role: "CEO"}
    const portraitCollection: IPortrait[] = [jens, jenszoom, kajsa, kajsa2];

    let portraitQueue: IPortrait[] = [];

    let visible: boolean = false;

    let mediaQueryExtraSmallDevice: MediaQueryList;
    let mediaQuerySmallDevice: MediaQueryList;
    let mediaQueryMediumDevice: MediaQueryList;
    let mediaQueryLargeDevice: MediaQueryList;

    const screenChanged = (event: MediaQueryListEvent) => {
        determineGridLayout(event.media, event.matches);
    }

    const initiateLayout = (extraSmallQueryResult: MediaQueryList, smallQueryResult: MediaQueryList, mediumQueryResult: MediaQueryList, largeQueryResult: MediaQueryList) => {
        if(largeQueryResult.matches){
            determineGridLayout(largeQueryResult.media, largeQueryResult.matches)
        }else if (mediumQueryResult.matches){
            determineGridLayout(mediumQueryResult.media, mediumQueryResult.matches)
        }else if (smallQueryResult.matches){
            determineGridLayout(smallQueryResult.media, smallQueryResult.matches)
        }else{
            determineGridLayout(extraSmallQueryResult.media, extraSmallQueryResult.matches)
        }
    }

    const determineGridLayout = (media: string, matches: boolean) => {
        console.log(media, matches)
        if (media === extraSmallMediaQuery && matches) {
            setGrid(1);
        }else if (media === smallMediaQuery) {
            if (matches) setGrid(2);
            else setGrid(1);
        }else if (media === mediumMediaQuery) {
            if (matches) setGrid(3);
            else setGrid(2);
        }else if (media === largeMediaQuery) {
            if (matches) setGrid(4);
            else setGrid(3);
        }
    }

    const setGrid = (size: number) => {
        portraitQueue = portraitCollection.slice(0, size)
    }

    
    onMount(() => {
        mediaQueryExtraSmallDevice = window.matchMedia(extraSmallMediaQuery);
        mediaQuerySmallDevice = window.matchMedia(smallMediaQuery);
        mediaQueryMediumDevice = window.matchMedia(mediumMediaQuery);
        mediaQueryLargeDevice = window.matchMedia(largeMediaQuery);

        mediaQueryExtraSmallDevice.onchange = (event) => { screenChanged(event); }
        mediaQuerySmallDevice.onchange = (event) => { screenChanged(event); }
        mediaQueryMediumDevice.onchange = (event) => { screenChanged(event); }
        mediaQueryLargeDevice.onchange = (event) => { screenChanged(event); }

        initiateLayout(mediaQueryExtraSmallDevice, mediaQuerySmallDevice, mediaQueryMediumDevice, mediaQueryLargeDevice);

        visible = true;
    });
</script>

<div>

    {#if visible}
        <div transition:fade class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 justify-items-center overflow-hidden">
            {#each portraitQueue as portrait}
                <Portrait name={portrait.name} role={portrait.role} imageReference={portrait.imageReference} />
            {/each}
        </div>
    {/if}

    <!--
    <Carousel images={portraitCollection}/>
    -->

</div>