<script>
    import { onMount } from "svelte";
    import {writable} from "svelte/store"
    import {setContext} from "svelte"
    import { createEventDispatcher } from 'svelte'
    import MenuList from "./MenuList.svelte"

    const dispatch = createEventDispatcher()

    export let collapse = false
    export let type = "menuVertical"
    export let paddingLeft = 0;

    export let role = 'ALL';
    export let menu;
    export let menuName = Math.random().toString(36).substring(2) + Date.now().toString(36);

    export let activeComponentID = ""

    let activeComponentId = writable(null)

    setContext('collapse', collapse) // should only show one expanded submenu at a time
    setContext('active', activeComponentId) // the active menuItem

    onMount(() => {
        if(activeComponentID != "") {
            $activeComponentId = activeComponentID
        }
        // let a = localStorage.getItem(menuName);
        // if(a) {
        //     menu = JSON.parse(a);
        // }
        // let acId = localStorage.getItem(menuName+"ActiveComponentID");
        // if(acId) {
        //     $activeComponentId = acId
        // }
    });

    function handleMenuClicked(e) {
        // localStorage.setItem(menuName, JSON.stringify(menu));
        // localStorage.setItem(menuName+"ActiveComponentID", e.detail.menuItem.componentId);
        let menuItem = e.detail.menuItem
        dispatch('menuClicked', {
            menuItem
        })
    }

</script>

<div>
    <ul class={type}>
        <MenuList {type} {menu} {role} {menuName} {paddingLeft} on:menuItemClicked={handleMenuClicked}/>
    </ul>
</div>

<style>
    ul.menuVertical {
        margin-left: -25px;
        list-style-type: none;
        text-align: left;
        width: 100%;
        display: inline-block;
    }
</style>