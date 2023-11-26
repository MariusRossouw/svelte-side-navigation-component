<script>
    import {getContext} from "svelte"
    import { createEventDispatcher } from 'svelte'
    import { goto } from "$app/navigation";

    export let menuItem;
    export let type;
    export let paddingLeft

    let pl = JSON.parse(JSON.stringify(paddingLeft))

    if(!menuItem.componentId) {
        menuItem.componentId = crypto.randomUUID()
    }

    let activeComponentId = getContext('active')

    const dispatch = createEventDispatcher()

    function setActive() {
        $activeComponentId = menuItem.componentId
        dispatch('menuClicked', {
			menuItem
		})
		if(menuItem.goto && menuItem.goto != "") {
			goto(menuItem.goto);
		}
    }

    $: isActive = $activeComponentId === menuItem.componentId
</script>


<li class={type}>
    <button style="margin-left: -15px;" on:click={() => { setActive(menuItem)}}  class:active={isActive}
        >
        {#if menuItem.label}
            <span style="margin-left: {pl+'px'}">
                {menuItem.label}
            </span>
        {:else}
            Please Provide Label
        {/if}
    </button>

</li>


<style>
    

    li.menuVertical {
        margin-left: 0px;
        list-style-type: none;
        text-align: left;
        width: 100%;
        display: inline-block;
    }

    li.menuVertical :hover {
        background: lightgray;
    }

    li.menuVertical .active {
		font-weight: bold;
        border-left: solid 3px blue;
        background: lightgray;
	}

    li.menuVertical button {
        margin-left: calc(pl-15)px;
        border: none;
        width: 100%;
        padding: 10px;
        text-align: left;
        background: transparent;
        border: none;
        color: black
    }

    li.menuVertical button:hover {
        cursor: pointer;
    }

</style>