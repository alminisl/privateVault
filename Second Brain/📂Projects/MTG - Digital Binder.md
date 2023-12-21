#project #private

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

## Current progress 

Working on the binder app. The feature set should be simple and straight forward as it is. 

- make collections
- add cards to collection
- Edit card infos - Quantity, set image 

## Loading images

this is currently a problem I'm facing, as I propagate some images thru prop drilling and I also make it so that I save the image into the DB. I want to make this process a bit smoother. I don't want it to work like it does now. 

Also one issues is when I add a new card I kinda have the problem that I cand change the print. 

## TODO 

- <mark style="background: #FF5582A6;">High</mark> Add Search for them in the library and add separate ADD TO LIBRARY buttons / popups
- So for now I have a cool feature ide, and thats TOURNAMENTS adding ladders + custom made games and decks. Also you can select your deck and deck view and see how many games you won with what deck. You can maybe later on add more statistics about this. 

- Something smaller: 
	![[Pasted image 20230820005129.png]]
	- add indicator that shows how many cards you have 
	- show indicator how many cards you have by color
	- Maybe add commander card ? 

- <mark style="background: #FF5582A6;">High</mark> In general when changig card prints - add loader for when changing the card art
- <mark style="background: #FFB86CA6;">Medium</mark> Add NOTES to cards and Decks - so that we can keep track of what is important in our decks and maybe add it as side-deck
- <mark style="background: #FF5582A6;">High</mark> sync costs of cards 

### Learnings

Add the Database and the app to Kubernetes and add grafana and prometheus - maybe the Friday 


## From base note


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

