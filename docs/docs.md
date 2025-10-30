---
title: Documentation
icon: material/file-document
---

# Main Documentation
---
Server Addons are a great environment within SCP:RP custom servers for lots of customisable server functionality.  
Addons use Lua script, so it is heavily recommended you get a basic grasp of how lua works and are comfortable with it.  
This page should help you understand all the different functions provided for you, to help you interact with the server.

Some functions have symbols next to them to let you know about limitations, such as requiring an online SSUH.

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
---
#### `f(name: string / instance: Instance)`  
This function allows you to both find an instance from the map via name or set an instance's parent to the workspace.
???+ info "Returns:"
    The instance found, or nil if no such instance found. If an instance is supplied then nil is returned.
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
    An array of all the instances found with that tag.
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

### Character
### Tool
### Team
### Display
### Web
### Misc
### Events
