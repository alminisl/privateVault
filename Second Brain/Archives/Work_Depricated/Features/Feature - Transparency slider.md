Working on this now, its easy enough I just have to add the slider component in the right place and find the opacity attribute for the layer

Currently tasks are like this:

-   Figure out how the slider is being added to the menu and how to add it
-   Connect the opcaity setting with the slider and number input..

Where is it rendered?

-   In the `BoundMenu.ts` and the `handleEntered` function after I press the "threedot menu"
-

Where does the Menu Items come from?

-   In the components menu you can enter `Layers` and there are the `Layer Actions`
  ![[Pasted image 20210423150816.png]]  
    

Still have to figure out where and how to inject the `Slider` here or in the Actions

-   In the end what I did is simply in the [[Second Brain/🖥️ Coding/Coding/LayerTreeNode]] added the `children` props and then just passed that down in `MenuButton` as `children={<Slider /}`

Apr 23, 2021

> Hi Almin, MenuButton does not forward children to the underlying bound menu. You'll need to either do that manually like in Iwtm.tsx, or else add a prop to MenuButton for this purpose. Regarding the slider itself, remember that it needs to show transparency, not opacity (the inverse). Also, keep in mind that the layer list shows both layers and sublayers, and that not every type of layer/sublayer can support a transparency slider (e.g. tiled map services do not). The logic to calculate all that should live in the model classes. So maybe add a transparency property to LayerListItemBase that has type `number | undefined`.

So as far I understand I have to find the `LayerListItemBase` and add a transparency prop here. ALso I don't understand where I should put the 

1. First step is to figure out how to pass down the Component and where to insert it.
2. After that look up the Slider in MUI and checkout how its being used

> I mean that the IWTM decomposes `MenuButton` into `Button` + `BoundMenu`, which among other things allows it to pass in children to BoundMenu, which isn't possible via MenuButton.

I made some changes document this here.. 

#### Something I Learned is that the `node` is the `LayerItemBase` interface. So I have to extend the node with `transperacy` prop. 
Extending this, Updates and new things about [[Second Brain/🖥️ Coding/Coding/transparency]] its not what I thought, I need to investigate more but this is something related to opacity but as it seems they are not the same thing. 

Finding the correct way how transparency relates to opacity is the next step! 

Most of the things I did is in the node (baseItem class) and just used that as the "model" class mentioned by eric. 



Today I want to check all the acceptence criteria:

- [x]   Oscar can manually adjust the transparency of a layer within GXW somewhere from the Layer List / TOC

- [x]   The mechanism for adjusting transparency is WCAG AA compliant

- [x]   Oscar-facing interface refers to Layer Transparency as a 0-100 value where 0 is opaque and 100 is completely transparent

- [x] Where Esri's JavaScript 4.x api supports it we will display the transparency slider on a group layer (we will respect whatever default behavior the API enforces, we will not try to 'fix' or 'change' it. We suspect it will not affect the transparency settings of the sub layers, but do some form of combined calculation for transparency) ✅ 2022-08-31

- [x]   Where Esri's JavaScript 4.x api does not support it, we will show no transparency component.

- [x] Oscar-modified transparency is respected by save/load projects feature ✅ 2022-08-31

- [x]   We are NOT providing an option for Clara to 'disable' Oscar-facing layer transparency


Got introduced to [[Second Brain/🖥️ Coding/Coding/falsy]] values in react now.. when conditionally rendering a component. 

Maybe using the `??` [[Second Brain/🖥️ Coding/Coding/operator]] will help in this case..
No need for the operator in the end. 

Still whats left is to rename transparency to opacity.. Transperancy is the way it should be FYI! 

Next up some feedback from Eric and I will probably add that to the knowledge base.

**17.05.2021 - Working on latest feedback**

Today I have still some feedback left and will have to fix this. 

The thing I refactored so far is making [[Second Brain/🖥️ Coding/Coding/abstract]] props for a class. These props are now in the `base` class and other classes which extend this base class need to implement those abstract props and functions.

`useWatchAndRerender` This is the key to making the variables on the frontend work. I have to dig deeper into figuring out what this function does. 


**18.05.2021**

One of the things I should consider more is going thru the changes and removing the unnssecary things I left in the code.

**19.05.2021**

Working on [[Testing]]