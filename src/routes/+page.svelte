<script>
    import Menu from "$lib/Menu/Menu.svelte";

    let menu = [
        {
            label: "Home",
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
        <Menu {menu} {role} menuName={"MyTestSideNav"} on:menuClicked={handleClick} />
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
