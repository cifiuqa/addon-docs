---
title: Documentation
icon: material/file-document
---

# Main Documentation
---
Server Addons are a great environment within SCP:RP custom servers for lots of customisable server functionality.  
Addons use Lua script, so it is heavily recommended you get a basic grasp of how lua works and are comfortable with it.  
This page should help you understand all the different functions provided for you, to help you interact with the server.

**Some functions have symbols next to them to let you know about limitations, such as requiring an online SSUH.**

---
## Environment
Server addons use a sandboxed version of Lua 5. This means that many typical things you may be able to do in Roblox normally (such as accessing services like Players or accessing player's characters) may not be possible with the current system.  
Modern LuaU functionality may also be unavailable, as LuaU is an expanded version of Lua. However, there is support for some operations such as +=, -=, *=, /= and ..= .  
!!! warning
    Functions that display messages to players undergo filtering and only function while the server host is in the server.
!!! warning
    When using "Run Once" in the server addons page, your code may only run for 10 seconds.

---
## API Reference
### Instance Functions

!!! abstract "Abstract"

    This section of the documentation contains functions for instances i.e. parts or models.
---
#### `f(name: string / instance: Instance)`  
This function allows you to both find an instance from the map via name or set an instance's parent to the workspace.
???+ info "Returns:"
    `1.` Instance: The instance found, or nil if no such instance found.
    `2.` nil: If an instance is supplied then nil is returned.
???+ example "Example Usage:"
    `1.` Find instance from name:  
    ``` { .lua }
    local part = f("ExamplePart")
    ```
    ??? warning "Warning: One instance"
        When using f(), it will only return one instance, similar to the behaviour of :FindFirstChild().
    ??? note "Note: Searches all descendants"
        f() will look for the instance beyond just the workspace, but all of its descendants, so even a part inside of a model would be found.
    `2.` Set instance's parent to workspace:
    ``` { .lua }
    local part = Instance.new("Part")
    f(part)
    ```
    ??? warning "Warning: Order of parenting"
        If you plan to have a hierarchy of parts made by a script, you may need to set the highest instance's parent first, before setting other instance's parents to avoid their data being automatically discarded.
---
#### `getTagged(tag: string)` :material-clock:{ .incomplete title="This function cannot be used yet. This particular function is not in the game yet, additionally tags do not save when saving a map." }  
This function allows you get an array with all the instances with a certain tag. A tag is a way of simply categorising instances.  
To add a tag to an instance you can use `:AddTag(tag: string)` and `:RemoveTag(tag: string)` to remove one.
???+ info "Returns:"
    **Array**: all instances found with specified tag.
    ??? example
        ``` { .lua }
        {
            PartWithTag: Instance,
            AnotherPartWithTag: Instance
        }
        ```
???+ example "Example Usage:"
    ``` { .lua }
    local parts = getTagged("ExampleTag")
    for i, part in ipairs(parts) do
        announce("Found a part!")
    end
    ```
---
### Player Interactions
---

!!! abstract "Abstract"

    This section of the documentation contains functions for player interactions i.e. usernames and gamepasses.

---
#### `getPlayers()`
This function allows you to fetch everyone's usernames.
???+ info "Returns:"
    **Array**: usernames of all online players.
    ??? example
        ``` { .lua }
        {
            "shotpaper7",
            "MetalTableIndex"
        }
        ```
???+ example "Example Usage:"
    ``` { .lua }
    local players = getPlayers()
    for i, plr in ipairs(players) do
        announce("Found user: "..plr)
    end
    ```
---
#### `getPlayerScore(username: string)`
This function allows you to get the current amount of points a specific user has.
???+ info "Returns:"
    **Number**: the amount of points currently owned.
    ??? example
        ``` { .lua }
        500
        ```
???+ example "Example Usage:"
    ``` { .lua }
    local points = getPlayerScore("shotpaper7")
    if points >= 500 then
        announce("You win!")
    end
    ```
---
#### `setPlayerScore((username: string), [score: number = 0])`
This function allows you to set the current amount of points for a specific user.
???+ example "Example Usage:"
    ``` { .lua }
    setPlayerScore("shotpaper7", 1000)
    ```
---
#### `getUserId(username: string)`
This function lets you fetch the user ID from a username.
???+ info "Returns:"
    **Number**: the user ID of the specified user.
    ??? example
        ``` { .lua }
        700047577
        ```
???+ example "Example Usage:"
    ``` { .lua }
    local userId = getUserId("shotpaper7")
    announce("User ID: "..userId)
    ```
---
#### `ownsGamepass(username: string, id: number)`
This function allows you to determine if a user has a gamepass or not.
???+ info "Returns:"
    **Boolean**: true/false based on if the user has the gamepass.
    ??? example
        ``` { .lua }
        false
        ```
???+ example "Example Usage:"
    ``` { .lua }
    if ownsGamepass("shotpaper7", 197234145) then
        announce("User has gamepass!")
    end
    ```
---
#### `ownsAsset(username: string, id: number)`
This function allows you to determine if a user has an asset or not.
???+ info "Returns:"
    **Boolean**: true/false based on if the user has the asset.
    ??? example
        ``` { .lua }
        false
        ```
???+ example "Example Usage:"
    ``` { .lua }
    if ownsAsset("shotpaper7", 14844522007) then
        announce("User has asset!")
    end
    ```
---
#### `getPlayerIsInGroup(username: string, id: number)`
This functions allows you to determine if a user is in a group or not.
???+ info "Returns:"
    **Boolean**: true/false based on if the user is in the group.
    ??? example
        ``` { .lua }
        false
        ```
???+ example "Example Usage:"
    ``` { .lua }
    if getPlayerIsInGroup("shotpaper7", 32725804) then
        announce("User is in group!")
    end
    ```
---
#### `getPlayerRoleInGroup(username: string, id: number)`
This function allows you to get the role a user has in a specified group.
???+ info "Returns:"
    **String**: The role the user has.
    ??? example
        ``` { .lua }
        "Owner"
        ```
???+ example "Example Usage"
    ``` { .lua }
    if getPlayerRoleInGroup("shotpaper7", 32725804) == "Owner" then
        announce("User is owner in group!")
    end
    ```
---
### Character

!!! abstract "Abstract"

    Body
 
### Tool
---
!!! abstract "Abstract"

    Body
---
#### `getPlayerKeycard(username: string)`
This function allows you to get the specified player's keycard level.
???+ info "Returns:"
    A string to represent keycard level.
    ??? example
        ``` { .lua }
        "L4"
        ```
???+ example "Example Usage:"
    ``` { .lua }
    local keycardLevel = getPlayerKeycard("shotpaper7")
    if keycardLevel == "O5" then
        announce("User has an O5 keycard!")
    end
    ```
 
### Team

!!! abstract "Abstract"

    This section of the documentation is for functions related to teams.
 
### Display

!!! abstract "Abstract"

    Body
 
### Web

!!! abstract "Abstract"

    Body
 
### Misc

!!! abstract "Abstract"

    Body
 
### Events

!!! abstract "Abstract"

    Body
 
