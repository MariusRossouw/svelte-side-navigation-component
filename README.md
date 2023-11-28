# svelte-side-navigation-menu-component

## Installation

1. Ensure you have node installed on your OS (v19 and above - recommended)
2. Navigate to the app where you would like to use the component and run the following in your terminal
```bash
npm install svelte-side-navigation-menu-component --save
```

## How to use the component

1. Inside the script tag of your .svelte file 
```javascript
import { Menu } from 'svelte-side-navigation-menu-component'
```
2. Inside an HTML element use the imported Menu component like so
```javascript
<Menu {menu} {role} menuName={"MySideNav"} on:menuClicked={handleClick}/>
```

## Props, handlers
1. ```{menu}``` Required, Array with all the menu items
2. ```{role}``` Optional, String to filter the menu items to be displayed
3. ```{menuName}``` Optional, String as a name for your menu
4. ```activeComponentID={"home"}``` Optional, String to set default menu item to be selected
4. ```on:menuClicked``` Optional, a function to handle menu item clicks (re-routing will happen if there is a route spesified inside the goto)


## Example
```+layout.svelte```
``` javascript
    <script>
    import Menu from "$lib/Menu/Menu.svelte";

    let menu = [
        {
            label: "Home",
            componentId: "home",
            goto: "/",
            roles: ["superAdmin", "admin"],
            subMenu: [],
        },
        {
            label: "Level 1.1",
            goto: "",
            roles: ["superAdmin", "admin"],
            subMenu: [
                {
                    label: "Level 2.1.1",
                    goto: "",
                    roles: ["superAdmin", "admin"],
                    subMenu: [
                        {
                            label: "Level 3.1.1",
                            goto: "/",
                            roles: ["superAdmin", "admin"],
                            subMenu: [],
                        },
                    ],
                },
                {
                    label: "Level 2.1.2",
                    goto: "/",
                    roles: ["superAdmin", "admin"],
                    subMenu: [],
                },
                {
                    label: "Level 2.1.3",
                    goto: "/",
                    roles: ["superAdmin", "admin"],
                    subMenu: [],
                },
                {
                    label: "Level 2.1.4",
                    goto: "/",
                    roles: ["superAdmin", "admin"],
                    subMenu: [],
                },
            ],
        },
        {
            label: "Level 1.2",
            goto: "",
            roles: ["superAdmin", "admin"],
            subMenu: [
                {
                    label: "Level 2.2.1",
                    goto: "/",
                    roles: ["superAdmin", "admin"],
                    subMenu: [],
                },
                {
                    label: "Level 2.2.2",
                    goto: "/",
                    roles: ["superAdmin", "admin"],
                    subMenu: [],
                },
            ],
        },
        {
            label: "Level 1.3",
            goto: "",
            roles: ["superAdmin"],
            subMenu: [
                {
                    label: "Level 2.3.1",
                    goto: "/",
                    roles: ["superAdmin"],
                    subMenu: [],
                },
                {
                    label: "Level 2.3.2",
                    goto: "/",
                    roles: ["superAdmin"],
                    subMenu: [],
                },
            ],
        },
    ];

    let role = 'superAdmin'

    function handleClick(event) {
        console.log(event.detail.menuItem);
    }
</script>

<div class="bodyContainer">
    <div class="sideNav">
        <Menu {menu} {role} activeComponentID={"home"} menuName={"MyTestSideNav"} on:menuClicked={handleClick} />
    </div>
    <div class="demoContent">
        <slot />
    </div>
</div>

<style>
    .bodyContainer {
        width: 100%;
        height: 100%;
        display: flex;
    }

    .sideNav {
        display: flex;
        position: relative;
        left: 0px;
        top: 0px;
        bottom: 0px;
        flex-direction: column;
        gap: 8px;
        min-width: 240px;
        max-width: 240px;
        height: 100vh;
        background-color: #f9fafb;
        z-index: 2;
        margin: 0px;
        padding: 0px;
    }

    .demoContent {
        min-height: 100%;
        display: flex;
        flex-direction: column;
        gap: 28px;
        width: 100%;
        height: 100%;
        background-color: #f6f7f8;
    }
</style>
```


## Styling
Can be set with variables associated with every element
```css
--menuItemHoverBackground
--menuItemHoverColor
--menuItemActiveBorderLeft
--menuItemActiveBackground
--menuItemActiveColor
--menuItemColor
```

## Feedback and recommendations
Please send me feedback or recommendations for improvements at mariusrossouwcr@gmail.com. I would love to here from you. [Donations](https://www.paypal.com/paypalme/MariusFRossouw) are welcome but not necessary.


