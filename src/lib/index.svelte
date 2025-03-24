<script lang="ts">
    const { fileDir, files, onclick, overrideFileClass, selectedIndex, overrideFileGridContainerClass} : {
        fileDir?: string,
        files: string[],
        onclick?: (fileIndex: number)=>void,
        overrideFileClass?: (isSelected: boolean) => string,
        selectedIndex: number|null,
        overrideFileGridContainerClass?: string,
    } = $props();

    const FileFullUrl = (fileSrc: string): string => {
        if(fileDir)
            return fileDir + fileSrc;

        return fileSrc;
    }

    const getFileClass = (isSelected: boolean): string => {
        if(overrideFileClass)
            return overrideFileClass(isSelected);

        return isSelected ? "file selected" : "file";
    }
</script>

<style>
    * {
        all: unset;
        box-sizing: border-box;
    }
    div {
        display: inline-block;
    }

    .file-grid {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        flex-wrap: wrap;
    }

    .file {
        width: 100px;
        height: 100px;

        border-radius: 5px;

        border: white solid 1.5px;
        box-shadow: 0 0 0 1px black;
        margin: 10px;

        cursor: pointer;

        object-fit: contain;
    }
    .file.selected {
        box-shadow: 0 0 0 4px black;
        cursor: default;
    }
</style>

<div class={(overrideFileGridContainerClass ? overrideFileGridContainerClass : "file-grid")}>
    {#each files as iterFile,i}
        <input type="image" src={FileFullUrl(iterFile)}
               class={getFileClass(selectedIndex !== null && i === selectedIndex)} alt={iterFile}
               onclick={()=>onclick(i)}
        />
    {/each}
</div>