<script>
    import MenuItem from "./MenuItem.svelte";
    import { createEventDispatcher } from "svelte";
    export let role;
    export let menu;
    export let menuName;
    export let type;

    export let paddingLeft
    let originalPaddingLeft = JSON.parse(JSON.stringify(paddingLeft))

    const dispatch = createEventDispatcher();

    function handleMenuClicked(menuItem) {
        dispatch("menuItemClicked", {
            menuItem,
        });
    }

    menu.forEach((item) => {
        item.expanded = false;
    });
</script>


{#each menu as menuItem}
    <!-- 
        Limit menuItems to the correct role
    -->
    {#if (menuItem.roles && menuItem.roles.indexOf(role) > -1) || role === "ALL"}
        
            <!--
                MenuItem with no children
            -->
            {#if menuItem.subMenu === undefined || (menuItem.subMenu && menuItem.subMenu.length === 0)}
                <MenuItem
                    {type} {menuItem} {paddingLeft}
                    on:menuClicked={handleMenuClicked(menuItem)}
                />
            <!--
                MenuItem with children
            -->
            {:else if menuItem.subMenu.length > 0}
                <!--
                    MenuItem with children collapsed
                -->
                <li class={type}>
                    <button
                        class="dropdown {menuItem.expanded ? 'active' : ''}"
                        on:click={() => {
                            menuItem.expanded = !menuItem.expanded;
                        }}
                    >
                        <span style="margin-left: {paddingLeft+'px'}">
                            {menuItem.label}
                        </span>
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            width="12"
                            height="12"
                            viewBox="0 0 24 24"
                            ><path
                                d="M7.33 24l-2.83-2.829 9.339-9.175-9.339-9.167 2.83-2.829 12.17 11.996z"
                            /></svg
                        >
                    </button>
                </li>
                <!--
                    Expanded menuItem with children
                -->
                {#if menuItem.expanded === true}
                    <svelte:self
                        {type}
                        paddingLeft={originalPaddingLeft+15}
                        menu={menuItem.subMenu}
                        {role}
                        {menuName}
                        on:menuItemClicked
                    />
                {/if}
            {/if}
    {/if}
{/each}

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

    li.menuVertical button {
        margin-left: -15px;
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

    li.menuVertical button.dropdown svg {
        float: right;
        height: 9px;
        width: 9px;
    }

    li.menuVertical button.dropdown.active svg {
        rotate: 90deg;
    }
    
</style>
