<script lang="ts">
    import FileGrid from "$lib/index.svelte";

    const thumbnails=["carouselmobile1.png","ailist1.jpg","ailist2.jpg"];

    let selectedIndex=$state<number|null>(0);
</script>

<style>
    * {
        all: unset;
        box-sizing: border-box;
    }
    div {
        display: inline-block;
    }

    :global(.PortfolioFileGridFile) {

        width: 100px;
        height: 100px;

        border-radius: 5px;

        border: white solid 1.5px;
        box-shadow: 0 0 0 1px red;
        margin: 10px;

        cursor: pointer;

        object-fit: contain;
    }

    :global(.PortfolioFileGridFileSelected) {
        box-shadow: 0 0 0 4px red;
        cursor: default;
    }
</style>

<div style="min-width: 100%;">

    <FileGrid
        files={thumbnails}
        selectedIndex={selectedIndex}
        overrideFileClass={(isSelected)=>
                (isSelected ? "PortfolioFileGridFile PortfolioFileGridFileSelected" : "PortfolioFileGridFile")}
        onclick={newIdx => selectedIndex = newIdx}
    />

</div>