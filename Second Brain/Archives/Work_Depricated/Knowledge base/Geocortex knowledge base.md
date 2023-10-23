# PR Feedback and learning new things

#TODO - Write all the findings from the PRs here and specific things like components and differences between react nodes and react components.

-   I can use the `?` [[Second Brain/🖥️ Coding/Coding/Links/operator]] directly on a property - IconComponent?: also React.component can be set as a type of the prop which then allows us to bas image, icon or whatever we want, and there is no need for a seperate showThumbnail.
    
    -   The `.?` operator can be used for function and arguments too
-   **Empty or null values -** usully just use `null` and not `undefined`
    
-   NEVER push package-lock.json
    
-   Check if props are being used
    
-   The UI code should have as little logic as possible. Typically this kind of code would live in the model, and the onClick handler would just invoke code in the model to perform all or most of the work.
    
-   It's important to distinguish between React components (class or function), and React nodes (instances of components, or string, null, etc). Since the prop is typed as React.Component, you need to give it an actual component instead of a node. The easiest thing to do is just wrap it in an anonymous function, like this:
    
    ```
    () => <Image ... />
    ```
    
    Then you won't need the type cast.
    
-   `{ Component ? Component : null }` Can simplify to `{IconComponent ?? null}`. Out of curiosity does the linter flag this when you update? It's supposed to catch this.
    

## Serialization and deserialization of settings in the app

// TODO add more information about this

## Need to make a branch from Release If I want to release

## Related to [[45493 - Label rotation is not rendered as defined by the map service]]

There were issues with the `sublayer.load()` method however I have no idea why this caused so much issues. I just know that there was the [[Second Brain/🖥️ Coding/Coding/Links/modifiers]] `supportsDynamicLayers` and it was set to `true` always and that caused the issue. Removing that loading (and some temporary code) fixed it. 


## How to check if layer is sublayer or just layer?
Currently I'm using this `this.layerExtension.supportsSublayers` not sure if this is the best way to do this

## add information about the branches and the testing when they are being tested and when I should merge it
[[Second Brain/🖥️ Coding/Coding/Links/Deployment]]

