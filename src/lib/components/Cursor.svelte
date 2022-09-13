<script lang="ts">
    import { spring } from 'svelte/motion';

    let coords = spring({ x: 0, y: 0}, {
        stiffness: 0.01,
        damping: 0.8
    })

    let size = spring(10)
</script>

<span class="fixed left-[{$coords.x}px] top-[{$coords.y}px] text-[{$size}px] z-50" 
    on:mousemove="{e => coords.set({ x: e.clientX, y: e.clientY })}"
    on:mousedown="{() => size.set(30)}"
    on:mouseup="{() => size.set(10)}">
    🦀
</span>