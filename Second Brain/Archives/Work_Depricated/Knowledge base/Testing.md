We don't yet have React tests for the layer list, but I would like all new UI code to come with react tests. Search the code for "react-testing" for examples. In this case it would make sense to have a few tests that verify that:

-   Changing the slider adjusts the opacity of the layer, and of a sublayer
-   Changing the slider adjusts the number input
-   Changing number input adjusts the opacity of a layer, and of a sublayer
-   Changing the number input adjusts the slider
-   Programmatically setting the opacity updates the slider and number input

Current stepps is to make the testing file with everything needed... easier said than done.. 

- The point I'm stuck now is the Children. I have to create the children elements manually too like in `Tabs.test.tsx` I assume that this is the issue if not I'm out of ideas.

- `spyOn()` Creates a mock function similar to `jest.fn` but also tracks calls to `object[methodName]`. Returns a Jest [mock function](https://jestjs.io/docs/mock-function-api).
- https://stackoverflow.com/questions/58856094/testing-a-material-ui-slider-with-testing-library-react
- Got some more links, I think the issue is that I need to "simulate" a click on the button and then return whatever is happening there. 

First I want to check Erics theory about the portal thingy then I will move on to the issue at hand. 

**Erics pushed changes to the Brnach with working example**

Eric did a sample test and seems like its working, so what was I missing. 
- The test is made in `LayerListNode.tsx` and that is used to run the test
- Firstly I was missing the `userEvent` from the `react-testing` ([[Second Brain/🖥️ Coding/Coding/Links/React-testing]])classes. After that is added we can do `userEvent.click(MenuButton)` 
- The `MenuButton` was right the way I did it (FindByRole) 
- And the setup process sets the opacity.

**Rerender**

Turns out I will have to re-render the component because the values are not being applied when I change it (since it is using the `useWatchAndRender` function of GCX api)

Have to use this convention - https://medium.com/@pjbgf/title-testing-code-ocd-and-the-aaa-pattern-df453975ab80