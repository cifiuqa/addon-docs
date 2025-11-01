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
## Instance Functions

!!! abstract "Abstract"

    This section of the documentation contains functions for instances i.e. parts or models.
---
### `f(name: string / instance: Instance)` { data-toc-label="f" id="f" }  
This function allows you to both find an instance from the map via name or set an instance's parent to the workspace.
???+ info "Returns:"
    `1.` Instance: The instance found, or nil if no such instance found.
    `2.` nil: If an instance is supplied then nil is returned.
???+ example "Example Usage:"
    `1.` Find instance from name:  
    ``` { .lua }
    -- This simply fetches a part named "ExamplePart".
    local part = f("ExamplePart")
    ```
    ??? warning "Warning: One instance"
        When using f(), it will only return one instance, similar to the behaviour of :FindFirstChild().
    ??? note "Note: Searches all descendants"
        f() will look for the instance beyond just the workspace, but all of its descendants, so even a part inside of a model would be found.
    `2.` Set instance's parent to workspace:
    ``` { .lua }
    local part = Instance.new("Part")
    -- This sets the part's parent to the workspace, also making it visible to players.
    f(part)
    ```
    ??? warning "Warning: Order of parenting"
        If you plan to have a hierarchy of parts made by a script, you may need to set the highest instance's parent first, before setting other instance's parents to avoid their data being automatically discarded.
---
### `getTagged(tag: string)` :material-clock:{ .incomplete title="This function cannot be used yet. This particular function is not in the game yet, additionally tags do not save when saving a map." } { data-toc-label="getTagged" id="getTagged" }  
This function allows you get an array with all the instances with a certain tag. A tag is a way of simply categorising instances.  
To add a tag to an instance you can use `:AddTag(tag: string)` and `:RemoveTag(tag: string)` to remove one.
???+ info "Returns:"
    **Array**: all instances found with specified tag.
???+ example "Example Usage:"
    ``` { .lua }
    -- Retrieves list of all parts with tag.
    local parts = getTagged("ExampleTag")
    local String = ""
    for _, part in ipairs(parts) do
        -- Compiles all part names into a string.
        String ..= ", "..part.Name
    end
    -- Then announces this string.
    announce("Found parts: "..String)
    ```
---
## Player Interactions
---

!!! abstract "Abstract"

    This section of the documentation contains functions for player interactions i.e. usernames and gamepasses.

---
### `getPlayers()` { data-toc-label="getPlayers" id="getPlayers" }
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
    -- Retrieves list of usernames of current players.
    local players = getPlayers()
    for i, plr in ipairs(players) do
        -- Loops through all users and announces their username.
        announce("Found user: "..plr)
    end
    ```
---
### `getPlayerScore(username: string)` { data-toc-label="getPlayerScore" id="getPlayerScore" }
This function allows you to get the current amount of points a specific user has.
???+ info "Returns:"
    **Number**: the amount of points currently owned.
???+ example "Example Usage:"
    ``` { .lua }
    -- Retrieves player's score.
    local points = getPlayerScore("shotpaper7")
    if points >= 500 then
        -- If the score meets a threshold, "You Win!" is announced.
        announce("You win!")
    end
    ```
---
### `setPlayerScore((username: string), [score: number = 0])` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="setPlayerScore" id="setPlayerScore" }
This function allows you to set the current amount of points for a specific user.
???+ example "Example Usage:"
    ``` { .lua }
    -- Sets a player's score to 1000.
    setPlayerScore("shotpaper7", 1000)
    ```
---
### `getUserId(username: string)` { data-toc-label="getUserId" id="getUserId" }
This function lets you fetch the user ID from a username.
???+ info "Returns:"
    **Number**: the user ID of the specified user.
???+ example "Example Usage:"
    ``` { .lua }
    local userId = getUserId("shotpaper7")
    -- Announces a player's user ID.
    announce("User ID: "..userId)
    ```
---
### `ownsAsset(username: string, id: number)` { data-toc-label="ownsAsset" id="ownsAsset" }
This function allows you to determine if a user has an asset or not.
???+ info "Returns:"
    **Boolean**: true/false based on if the user has the asset.
???+ example "Example Usage:"
    ``` { .lua }
    if ownsAsset("shotpaper7", 14844522007) then
        -- Announces a message if the user has the asset.
        announce("User has asset!")
    end
    ```
---
### `ownsGamepass(username: string, id: number)` { data-toc-label="ownsGamepass" id="ownsGamepass" }
This function allows you to determine if a user has a gamepass or not.
???+ info "Returns:"
    **Boolean**: true/false based on if the user has the gamepass.
???+ example "Example Usage:"
    ``` { .lua }
    if ownsGamepass("shotpaper7", 197234145) then
        -- Announces a message if the user has the gamepass.
        announce("User has gamepass!")
    end
    ```
---
### `getPlayerIsInGroup(username: string, id: number)` { data-toc-label="getPlayerIsInGroup" id="getPlayerIsInGroup" }
This functions allows you to determine if a user is in a group or not.
???+ info "Returns:"
    **Boolean**: true/false based on if the user is in the group.
???+ example "Example Usage:"
    ``` { .lua }
    if getPlayerIsInGroup("shotpaper7", 32725804) then
        -- Announces a message if the user is in the group.
        announce("User is in group!")
    end
    ```
---
### `getPlayerRoleInGroup(username: string, id: number)` { data-toc-label="getPlayerRoleInGroup" id="getPlayerRoleInGroup" }
This function allows you to get the role a user has in a specified group.
???+ info "Returns:"
    **String**: The role the user has.
???+ example "Example Usage:"
    ``` { .lua }
    if getPlayerRoleInGroup("shotpaper7", 32725804) == "Owner" then
        -- Announces a message if the user has a specific role in the group.
        announce("User is owner in group!")
    end
    ```
---
## Character Interactions
---
!!! abstract
    This section of the documentation contains functions for character interactions i.e. health.
---
### `kill(username: string)` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="kill" id="kill" }
This function allows you to easily kill a player's character.
???+ example "Example Usage:"
    ``` { .lua }
    kill("shotpaper7") -- Kills specified user.
    ```
---
### `damage(username: string, amount: number)` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="damage" id="damage" }
This function allows you to damage a player's character by a specified amount.
???+ note
    This function supports negative numbers for the amount, meaning you can heal users by a specified amount.
???+ example "Example Usage:"
    `1.` (Damage)
    ``` { .lua }
    damage("shotpaper7", 50) -- Damages user by 50 HP.
    ```
    `2.` (Heal)
    ``` { .lua }
    damage("shotpaper7", -50) -- Heals user by 50 HP.
---
### `heal(username: string)` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="heal" id="heal"}
This function allows you to heal a user to full health.
???+ example "Example Usage:"
    ``` { .lua }
    heal("shotpaper7") -- Heals user to max health.
    ```
---
### `getPlayerHealth(username: string)` { data-toc-label="getPlayerHealth" id="getPlayerHealth" }
This function allows you to determine how much health a player currently has.
???+ info "Returns:"
    **Number**: The amount of health a user has. (Normally between 0-100.)
???+ example "Example Usage:"
    ``` { .lua }
    local health = getPlayerHealth("shotpaper7")
    if health >= 50 then
        -- Announces a message if the user has at least 50 health.
        announce("Health is above 50%!")
    end
    ```
---
### `setPlayerHealth(username: string, amount: number)` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="setPlayerHealth" id="getPlayerHealth" }
This function allows you to set a player's health.
???+ example "Example Usage:"
    ``` { .lua }
    -- Sets users health to 50 HP (by default this would be 50%).
    setPlayerHealth("shotpaper7", 50)
    ```
---
### `getPlayerMaxHealth(username: string)` { data-toc-label="getPlayerMaxHealth" id="getPlayerMaxHealth" }
This function allows you to determine the max amount of health a player can have.
???+ info "Returns:"
    **Number**: The max health the player currently has, set by setPlayerMaxHealth() or :maxhealth.
---
### `setPlayerMaxHealth(username: string, amount: number)` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="setPlayerMaxHealth" id="setPlayerMaxHealth" }
This function allows you to set a player's max health.
???+ example "Example Usage:"
    ``` { .lua }
    -- Allows the user to have up to 150 health, default is 100.
    setPlayerMaxHealth("shotpaper7", 150)
    ```
---
### `getPlayerPosition(username: string)` { data-toc-label="getPlayerPosition" id="getPlayerPosition" }
This function allows you to get the CFrame position of a player's HumanoidRootPart. (In other words, tells you where player is.)
???+ info "Returns:"
    **CFrame**: CFrame of the specified user. You can get the position of a CFrame (convert it to Vector3) by using CFrame.Position
???+ example "Example Usage:"
    ``` { .lua }
    local part = f("ExamplePartName")
    -- Fetches the player's CFrame and multiplies it by another CFrame for relative movement.
    -- In this case, it would have a CFrame 5 studs in front of the player.
    position = getPlayerPosition * CFrame.new(0, 0, -5)
    part.CFrame = position
    ```
---
### `setPlayerPosition(username: string, position: Vector3/CFrame)` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="setPlayerPosition" id="setPlayerPosition" }
This function lets you set a player's position to a Vector3 or CFrame.
???+ example "Example Usage:"
    `1.` Set position via CFrame:
    ``` { .lua }
    local part = f("ExamplePartName")
    -- Fetches the specified part's position (CFrame).
    local targetCFrame = part.CFrame
    -- Teleports the player to the part's CFrame.
    setPlayerPosition("shotpaper7", targetCFrame)
    ```
    `2.` Set position via Vector3:
    ``` { .lua }
    local part = f("ExamplePartName")
    -- Fetches the specified part's position (Vector3).
    local targetPosition = part.Position
    -- Teleports the player to the part's Position.
    setPlayerPosition("shotpaper7", targetPosition)
    ```
    ???+ note
        By using CFrame rather than Vector3, you also specify rotation, meaning you can choose whether or not you should set the player's rotation as well.
---
### `playEmote((username: string / target: Instance), id: number, [loop: boolean = false])` :material-alert:{ .buggy title="This function may be hard to understand or give unintended results. Please be cautious." } { data-toc-label="playEmote" id="playEmote" }
This is a much more complicated function, this allows you to play emotes and animations on rigs and characters.  
You can choose to set username or target, username would let you animate a player, and target lets you animate rigs.  
For the target, you can provide a Humanoid, Animator, AnimationController or an instance with a Humanoid as a descendant. This would also allow you to animate custom SCPs and much more.
???+ question
    To my current knowledge, this function only allows for emotes from the catalog, not custom animations made with the likes of Moon Animator. If you have any further info about this please contact me `@aquific`. Thank you!
???+ info "Returns:"
    **Tuple**: Containing:
    `1.` **Function**: function to stop the emote, simply call it like stopFunction().
    `2.` **Function**: function to change the speed of the emote, adjustSpeedFunction(1.5).
???+ example "Example Usage:"
    `1.` Player animation:
    ``` { .lua }
    playEmote("shotpaper7", 138498832987078, true)
    ```
    `2.` Rig animation:
    ``` { .lua }
    local rig = f("RigName")
    playEmote(rig, 138498832987078, true)
    ```
    ???+ note
        Using rigs seems to very buggy at the moment. The only reliable method I have found is by unanchoring all parts of the rig except for the HumanoidRootPart, but this may be patched in the future.

## Tool
---
!!! abstract
    This section of the documentation contains functions to interact with player tools and guns.
---
### `getTools(username: string)` { data-toc-label="getTools" id="getTools" }
This is a function which gives you a list of all the items a player currently has.
???+ info "Returns:"
    **Array**: List of all items currently possessed.
    ??? example
        ``` { .lua }
        {
            "Clipboard",
            "L4 Keycard"
        }
???+ example "Example Usage:"
    ``` { .lua }
    -- This simply gets the array of tools.
    local tools = getTools("shotpaper7")
    -- This then converts the array into a string, separating each item with ", "
    local toolString = table.concat(tools, ", ")
    -- This then shows the string.
    announce("User has: " .. toolString)
    ```
### `giveTool(username: string, (toolName: string / toolInstance: Tool))` :material-keyboard-return:{ .no-return title="This function returns nothing, therefore any attempts to get a return will give nil." } { data-toc-label="giveTool" id="giveTool" }
This function allows you to give a user either a built in SCP:RP tool, or a custom tool (via a Tool instance).
???+ example "Example Usage:"
    `1.` SCP:RP Built-in Tool
    ``` { .lua }
    giveTool("shotpaper7", "L4 Keycard")
    ```
    `2.` Custom Tool
    ``` { .lua }
    -- This initiates the main tool instance, this is what roblox uses to handle tools.
    local tool = Instance.new("Tool")
    tool.CanBeDropped = false
    tool.Name = "Custom Tool"

    -- This initiates the handle. This is required for a visible tool.
    local handle = Instance.new("Part")
    handle.Name = "Handle"
    handle.Anchored = true
    handle.CanCollide = false
    -- This simply prevents it from being manipulated. The actual handle appears normally.
    handle.CFrame = CFrame.new(9999, 9999, 9999)

    -- The tool must be parented to workspace, as there is no access to ReplicatedStorage.
    f(tool)
    handle.Parent = tool

    -- This finally gives the player the custom tool.
    giveTool("shotpaper7", tool)
    ```
### `getPlayerKeycard(username: string)` { data-toc-label="getPlayerKeycard" id="getPlayerKeycard" }
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
 
## Team

!!! abstract

    This section of the documentation is for functions related to teams.
 
## Display

!!! abstract

    Body
 
## Web

!!! abstract

    Body
 
## Misc

!!! abstract

    Body
 
## Events

!!! abstract

    Body
 
