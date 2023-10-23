
- Working on the digital binder app so far made nice progress however some of the core features that I will need to support is to export or import decks. 
  
  Currently the exporting can be looked at here: https://www.moxfield.com/decks/vKenUyAq5Eaneqf1Dazp1w There is an export button and check that out for future reference 
- [[Export/import Cards]]

Make the UI fancy with some CSS magics. 
import { useHover } from "@mantine/hooks";
import { useMouse } from "@mantine/hooks";


### Prices and Marketplaces

Currently I don't really understand the relation to the marketplaces and the cards. I will have to make it work somehow.. not sure how Just investigating now. 


`PurchaseUris` - Table with URLs to marketplaces
`Prices` - List of prices, probably will need to update this one with another source?

Now I've implemented the prices and the currencies, however the things that is missing is different card markets. However my current plan is to load the prices from an external source, for example: https://github.com/bedoherty/MagicTCGPriceAPI 

