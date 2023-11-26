<script>
    import "../app.css";
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
                        }
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
                }

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
            ]
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
            ]
        }
    ];

    function handleClick(event) {
        console.log(event.detail.menuItem);
    }

    function logout() {
        console.log("Log Out");
    }
</script>

<div class="bodyContainer">
    <div class="sideNav">
        <Menu
            {menu}
            menuName={"AssetSphereSideMenu"}
            on:menuClicked={handleClick}
        />
    </div>
    <div class="demoContent">
        <slot />
    </div>
    
</div>
