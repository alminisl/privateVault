So, the idea is to continue my developer log in here and not notion. becuase notion is bit heavy and too much features which I don't need. I just want something simple to write down notes and things Im currently stuck on. 


[[Second Brain/🖥️ Coding/Coding/Layer Presets]] is the ticket im working on currently. All the attributes are added, I just need to make the `original values` work. My current idea is to have an attribute in the layerPreset itself to save the original values for it in the attribute. 

something I learned is that I have the `LayerItemstoDtos` or something like that, it has `data` object and that `data` object is being used in `schema` to show / visible or not. 

Made a way to have the [[Second Brain/🖥️ Coding/Coding/no change]]

Note: The original value can be found in the `model.layerPreset.originalValue` so for reference I can use this. 

Updated [[Second Brain/🖥️ Coding/Coding/no change]] link with Erics comment. Essentially all changes should initially be "no changes".


Made a new way to store the `OriginalValues` but still need to figure out what kind of errors are happening. Currently the status is that I can't update the layerList when clicking on the layerPreset. 


- A new comment on a PR which is related to the menuItem. I think its because of the Accessability stuff, but I will check it again during the day.
- Fixed!! 

- [x] make the same changes for all the other attributes like I did in `sublayerVisibility`

## Hannes debugging session Still uptodate?
for the basemap picker settings for the copy basemaps stuff
- Issue is most probably with the `portalITem` which is empty 
- The portalItem was the problem and its fixed by doing


**20.8.21**

Today I continue with the layer presets, but today I tackle the UI Stuff.. I also try to configure lvim to use the lsp for TS and use it instead of VScode because of resource concerns lets see how it goes... 

The UI work will be hard I suppose Will have to make a lot of changes to the components.. 

The rest of the day I would like to finish and fix the tests left. SOme of the tests I have fixed, however, I still have to write additional tests for the attributes. 

**TODO**: Added bookmarks to the code and tests and that is what I should finish on monday first thing! 


**23.8.21**

- [x] Review the bookmakrs left
- [x] Extend the tests with the new attributes 
- [x] Tests for Web should be done

The thing remaining is to figure out what kind of tests I want for the API and `applyTo` method. 

Now lets think about the apply to method: 
- New attribute
- new attribute with original values

**24.8.21**

- Made the PRs work. Now the thing to do is to validate the PRs and fix potential issues
- Continue work on the Layer presets new UI thingies.. 

[[Layer Presets UI]]

Issues with PC... 