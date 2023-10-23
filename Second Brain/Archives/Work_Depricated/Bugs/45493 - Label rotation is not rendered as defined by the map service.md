-   Webmap and Layer issue? Not same wording?
-   Sent message to Eric waiting for feedback
-   The issue seems to be that we send `dynamicLayers` attribute and should not be sent:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8ae5dd6e-ac8a-4528-ac00-95ff97eb5b2c/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8ae5dd6e-ac8a-4528-ac00-95ff97eb5b2c/Untitled.png)

Thats the problem which needs to be solved on this..

-   Talk with scott for more info maybe?
-   Found the issue, its with the `ArcGisSublayerExtension.ts` in the API. The issue is that the renderer is being overwritten.
-   TODO: [](https://geocortex.visualstudio.com/Geocortex/geocortex-api-ts/_workitems/edit/43706)[https://geocortex.visualstudio.com/Geocortex/geocortex-api-ts/\_workitems/edit/43706](https://geocortex.visualstudio.com/Geocortex/geocortex-api-ts/_workitems/edit/43706)
    -   Make this work with my changes and debug it
-   On monday fix this so that I can work with Scotts and mine changes
-   In the end the "fix" was just removing the temporary code

- Removing the tests with `exportMap` property and hopefully this works now.

### Tests are failing

Currently 2 tests are failing and I have no idea why so the investigation should begin. 

The first test fails with the `sublayer.effectiveFullExtent` which does not exist. 
I don't understand why I cant make the console log appear in the tests itself

## What id scott fix? 

https://geocortex.visualstudio.com/Geocortex/_git/geocortex-api-ts/commit/39cc40f623c08b1f3f7a78d205b29519eb957d99?refName=refs%2Fheads%2F45493.label-rotation

Essentially the keys and the thingies he did on here