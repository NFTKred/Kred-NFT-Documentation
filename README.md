## Building an App With the Kred NFT API

This guide shows how you build your own app using the Kred NFT API.

### Home Page
<p align="center">
  <img width="80%" src="https://files.readme.io/68ba12d-CK_Explore.PNG" title="Explore">
</p>  

Our home view is the Explore tab.   We've created this with three calls to the [/coins](https://docs.coin.kred/v1.0/reference#coins)  method, sorting respectively by likes, creation date, and circulation.  Each of these calls can be paginated, so that the groups of coins are bound to individual carousels and can be browsed by the user.

<p align="center">
  <img width="80%" src="https://files.readme.io/01f0755-CK_Marketplace.PNG" title="Marketplace">
</p>  

The Marketplace tab is created using a single call to a specialised method [/marketplace](https://docs.coin.kred/v1.0/reference#marketplace).  This call merges, filters, and sorts active sales and auctions to present a single unified view.  We use pagination again to provide infinite scroll, preloading pages on desktop to ensure smooth loading of additional coins.

<p align="center">
  <img width="80%" src="https://files.readme.io/71e2144-CK_Collection.PNG" title="Collection">
</p>  

The Collection tab shows the user's own collection of coins - coins they have created, bought at sale or auction, claimed from giveaways, been gifted by other users.  This view is another call to [/coins](https://docs.coin.kred/v1.0/reference#coins), simply specifying the user, and supporting infinite scroll.

The same call can be used to embed the user's collection in other pages - their Engagement Profile, blog, or other home page.

<p align="center">
  <img width="80%" src="https://files.readme.io/ee9e8ab-CK_Newsfeed.PNG" title="Newsfeed">
</p>  

The Newsfeed tab combines several functions: A feed of coin activity related to the user - coins created, requests from other users, coins received and sent, sold and auctioned.  This is provided by the [/messages](https://docs.coin.kred/v1.0/reference#messages) call, requesting the user's timeline.  The [/messages](https://docs.coin.kred/v1.0/reference#messages) call can also be used to view messages relating to any single coin (or batch of coins if the coins are in a mesh network).

The Pending widget uses [/remind](https://docs.coin.kred/v1.0/reference#remind) to list reminders for actions started but not yet complete.

The Search Contact widget uses the SocialOS Contact API (documented separately).

<br><br>

### Batches and Coins

<p align="center">
  <img width="80%" src="https://files.readme.io/f8a39eb-CK_Batch1.PNG" title="Batched View">
</p>  

Clicking on a coin that is part of a batch brings up the batch view.  We use the *batched* parameter in [/coins](https://docs.coin.kred/v1.0/reference#coins) and [/marketplace](https://docs.coin.kred/v1.0/reference#marketplace) to show a single entry for each batch along with the number of coins available (total in the Explore tab, and just the number on sale in the Marketplace tab).

<p align="center">
  <img width="40%" src="https://files.readme.io/d79c8a4-Spacecoin.png" title="Batched coin">
</p>  

From the batch view we can edit certain details for all coins in the batch:

Add and edit tags using [/tag](https://docs.coin.kred/v1.0/reference#tag)
Hide or show the coins using [/hide](https://docs.coin.kred/v1.0/reference#hide) and [/show](https://docs.coin.kred/v1.0/reference#show)
Make the coins private or public using [/private](https://docs.coin.kred/v1.0/reference#private) and [/public](https://docs.coin.kred/v1.0/reference#public)
Showcase the coins (if the user has showcase privileges) using [/showcase](https://docs.coin.kred/v1.0/reference#showcase) and [/unshowcase](https://docs.coin.kred/v1.0/reference#unshowcase) 
Update metadata such as the coin description and link using [/meta](https://docs.coin.kred/v1.0/reference#meta)

Specifying the batch on these API calls allows you to update all the coins in the batch that you own.

<p align="center">
  <img width="80%" src="https://files.readme.io/d5db70a-CK_Batch2.PNG" title="Batch edit">
</p>  

We can give a coin from this screen, either directly to an on-platform user using [/send](https://docs.coin.kred/v1.0/reference#send) or to any user via Email, SMS, or Twitter using [/hold](https://docs.coin.kred/v1.0/reference#hold).

[/hold](https://docs.coin.kred/v1.0/reference#hold) uses a two-step processes, reserving the coin, creating a secure code, and notifying the recipient via the designated method.  The recipient can then log in to the app, which will use the [/claim](https://docs.coin.kred/v1.0/reference#claim) method to accept the sent coin.

<p align="center">
  <img width="80%" src="https://files.readme.io/a983ee9-CK_Coin1.PNG" title="Coin popup">
</p>  

Clicking on an individual coin brings up the coin popup using [/coin](https://docs.coin.kred/v1.0/reference#coin) and [/messages](https://docs.coin.kred/v1.0/reference#messages).  We can see the full version of the coin images here, and play videos if it's a video coin, and add comments to the message stream using [/comment](https://docs.coin.kred/v1.0/reference#comment)

<p align="center">
  <img width="80%" src="https://files.readme.io/2702006-CK_Coin2.PNG" title="Coin popup back">
</p>  

The image viewer can show the front and back images in full, play videos, and also show images included in the coin metadata.  No separate call is needed to retrieve metadata; it is automatically included in every call that returns coin details.

<p align="center">
  <img width="80%" src="https://files.readme.io/dcdfd52-CK_Coin3.PNG" title="Coin view">
</p>  

Clicking on the More button brings up a dedicated coin screen.  The coin is retrieved by a single call to [/coin](https://docs.coin.kred/v1.0/reference#coin).

The coin carousel at the top of the page is generated by a call to [/coins](https://docs.coin.kred/v1.0/reference#coins) for the wallet containing the specified coin.  The client code find the current coin in this list and uses that to center the carousel on the right coin.

The message stream is again retrieved by a call to [/messages](https://docs.coin.kred/v1.0/reference#messages).

We have additional buttons to auction, sell, and give coins using [/auction](https://docs.coin.kred/v1.0/reference#auction), [/sell](https://docs.coin.kred/v1.0/reference#sellf), and [/hold](https://docs.coin.kred/v1.0/reference#hold) or [/send](https://docs.coin.kred/v1.0/reference#send) respectively.

<p align="center">
  <img width="80%" src="https://files.readme.io/bae56e9-CK_Coin5.PNG" title="Coin edit">
</p>  

We can modify coin tags, settings, and metadata just as we do with batches, simply by specifying a coin parameter in place of the batch parameter.

Add and edit tags using [/tag](https://docs.coin.kred/v1.0/reference#tag)
Hide or show the coin using [/hide](https://docs.coin.kred/v1.0/reference#hide) and [/show](https://docs.coin.kred/v1.0/reference#show)
Make the coin private or public using [/private](https://docs.coin.kred/v1.0/reference#private) and [/public](https://docs.coin.kred/v1.0/reference#public)
Showcase the coin (if the user has showcase privileges) using [/showcase](https://docs.coin.kred/v1.0/reference#showcase) and [/unshowcase](https://docs.coin.kred/v1.0/reference#unshowcase) 
Update metadata such as the coin description and link using [/meta](https://docs.coin.kred/v1.0/reference#meta)

<p align="center">
  <img width="80%" src="https://files.readme.io/22fc7c4-CK_Coin6.PNG" title="Giveaway">
</p>  

You can generate a public giveaway URL [/giveaway](https://docs.coin.kred/v1.0/reference#giveaway) or a code for use requests [/request](https://docs.coin.kred/v1.0/reference#request).

<br><br>

### Designing and Minting Coins

From the menu, we can select Create a Coin to start the design and mint application flow.

<p align="center">
  <img width="80%" src="https://files.readme.io/2dba4ba-CK_Menu.PNG" title="Menu">
</p>  

This brings up the coin designer.


<p align="center">
  <img width="80%" src="https://files.readme.io/39b5815-CK_Create1.PNG" title="Coin designer">
</p>  

We use a JavaScript library to crop and scale the uploaded images at the client, to avoid direct uploads of very large images.

<p align="center">
  <img width="80%" src="https://files.readme.io/ca37376-CK_Create2.PNG" title="Image crop and scale">
</p>  

The design tool allows users to set the name, images, colours, and background pattern of the coin, set the value of the coin and the number of coins in the batch, and choose whether each coin in the batch has its own message stream, or if all coins are combined in a mesh.  Coins can also be marked as private and/or NSFW at this point.

These parameters are passed to [/draft](https://docs.coin.kred/v1.0/reference#draft) or [/mint](https://docs.coin.kred/v1.0/reference#mint) to either save the design or mint the coin.


<p align="center">
  <img width="80%" src="https://files.readme.io/8334a0b-CK_Create6.PNG" title="Coin details">
</p>  

The design is rendered immediately using SVG.

<p align="center">
  <img width="80%" src="https://files.readme.io/92bec75-CK_Create7.PNG" title="Coin render">
</p>  

Users can also specify royalties to be accumulated each time a coin is sold.  These are calculated as a percentage of the sale price.  Royalty collection takes place automatically once configured with the [/royalties](def:royalties) method.

<p align="center">
  <img width="80%" src="https://files.readme.io/9cb763d-CK_Designs1.PNG" title="Coin designs">
</p>  

By saving the coin using the [/draft](https://docs.coin.kred/v1.0/reference#draft) method the design is stored without immediately creating a coin, and the details are saved for retrieval by the [/drafts](https://docs.coin.kred/v1.0/reference#drafts) method.  Users can page through existing designs, modify them using the coin designer, and save them again using [/draft](https://docs.coin.kred/v1.0/reference#draft) or mint a coin using [/mint](https://docs.coin.kred/v1.0/reference#mint).

<p align="center">
  <img width="80%" src="https://files.readme.io/de87ae2-CK_Coin_Types0.PNG" title="Basic metadata">
</p>  

Users can add metadata to coins that is included with every API call that returns coin data.  Unlike key data (the name, appearance, and value of the coin) which is bound to the blockchain, metadata can be updated at any time via the [/meta](https://docs.coin.kred/v1.0/reference#meta) call.

<p align="center">
  <img width="80%" src="https://files.readme.io/9c8f561-CK_Coin_Types.PNG" title="Artist coin">
</p>  

Additional coin types can be defined with different sets of metadata fields.  These can be simply informative, as in the case of an artist coin intended to showcase an artist's work.

<p align="center">
  <img width="80%" src="https://files.readme.io/32ab726-CK_Coin_Types2.PNG" title="Artist coin">
</p>  

Or they can be active fields such as one-time redeemable offers in marketing campaigns.  These can be implemented using callbacks.

<p align="center">
  <img width="80%" src="https://files.readme.io/2d97ac4-CK_Designs2.PNG" title="Create coin from design">
</p>  

When a coin is minted, it is immediately listed on the blockchain.  With Stellar, this only takes around five seconds, and multiple coins can be batched and listed simultaneously.

<p align="center">
  <img width="80%" src="https://files.readme.io/521b7dc-CKD2.PNG" title="Blockchain">
</p>  

When minting a coin to the Stellar network - and with all Stellar operations - the API will wait for confirmation from Stellar before returning.  If the operation cannot be completed (insufficient funds, for example, or an issue with the network itself) the API will return an appropriate error status and no transaction will take place.


<p align="center">
  <img width="80%" src="https://files.readme.io/6f0914e-CKD3.PNG" title="Success">
</p>  

When operating on the Ethereum network, transactions are recorded first in the local database, and then submitted to the blockchain and monitored for success.  The API will return immediately and note the details of the transaction in progress.

A coin with an incomplete Ethereum transaction pending will have the transaction details included with the coin data and cannot have further transactions applied until the pending transaction either completes or fails.

<br><br>

### Sales and Auctions

<p align="center">
  <img width="80%" src="https://files.readme.io/656340e-CK_Sell1.PNG" title="Sell coin">
</p>  

Listing a coin for sale is simple: Just call the [/sell](https://docs.coin.kred/v1.0/reference#sell) endpoint with the coin and the price.  Your coin will immediately be listed in [/sales](https://docs.coin.kred/v1.0/reference#sales) and [/marketplace](https://docs.coin.kred/v1.0/reference#marketplace), and a message will be sent notifying users that the coin is for sale.  (The notification is automatic, but a separate message can be sent with [/post](https://docs.coin.kred/v1.0/reference#post) if desired.

<p align="center">
  <img width="80%" src="https://files.readme.io/bb2d382-CK_Auction1.PNG" title="Auction coin">
</p>  

Auctioning a coin is only slightly more involved.  The default auction process is a reverse auction, also known as a Dutch auction.  You specify a starting price and a minimum price, and the price ticks down every second until a buyer takes the offer or the auction expires.

<p align="center">
  <img width="80%" src="https://files.readme.io/7ce95bc-CK_Auction2.PNG" title="Auction run time">
</p>  

Auctions are listed in [/auctions](https://docs.coin.kred/v1.0/reference#auction) and [/marketplace](https://docs.coin.kred/v1.0/reference#marketplace).  If an auction expires without sale, it is automatically removed from the listings.

Sales and auctions can be cancelled at any time using [/cancel](https://docs.coin.kred/v1.0/reference#cancel).

<p align="center">
  <img width="80%" src="https://files.readme.io/277b716-CK_Marketplace.PNG" title="Marketplace">
</p>  

The [/marketplace](def:marketplace) call will automatically group coins for sale and auction in a given batch, showing the lowest price available from that batch.

<br><br>

### Tagging, Sorting, and Searching

<p align="center">
  <img width="80%" src="https://files.readme.io/063ee1c-CK_Tags.PNG" title="Tags">
</p>  

Users can specify an arbitrary set of tags against a coin, to help others to find mutual interests.

<p align="center">
  <img width="80%" src="https://files.readme.io/8a02e4d-CK_Coin_Audience.PNG" title="Audience and topic">
</p>  

Coins can also be grouped by audience and topic.  These can be pre-defined or user-defined as needed.  Audience and topic are defined as special tags, and can be filtered alongside any other tags.  A typical tag scheme would be audience:bloggers or topic:science.


<p align="center">
  <img width="80%" src="https://files.readme.io/abeac65-CK_Sort.PNG" title="Sorting">
</p>  

Calls returning multiple coins, including [/coins](https://docs.coin.kred/v1.0/reference#coins), [/marketplace](https://docs.coin.kred/v1.0/reference#marketplace), [/sales](https://docs.coin.kred/v1.0/reference#sales), and [/auctions](https://docs.coin.kred/v1.0/reference#auctions) support flexible sorting options to zoom in on the most relevant content.

<p align="center">
  <img width="80%" src="https://files.readme.io/c9c4951-CK_Search.PNG" title="Search">
</p>  

Users can search quickly by tag, using the tags parameter on calls like [/marketplace](https://docs.coin.kred/v1.0/reference#marketplace) and [/coins](https://docs.coin.kred/v1.0/reference#coins).  As a developer you can refine the selection using the any_tags and all_tags filters, which are applied in combination with user-specified tags.  This saves having to generate a complex AND / OR search query.

<p align="center">
  <img width="80%" src="https://files.readme.io/311a16b-CK_Search2.PNG" title="Search collection">
</p>  

Searching in a collection simply adds the user parameter to the same [/coins](https://docs.coin.kred/v1.0/reference#coins) call.

While search links are public and shareable, a search within your own collection will of course vary between users.

<p align="center">
  <img width="80%" src="https://files.readme.io/48424f9-CK_Search_Suggest.PNG" title="Search suggestions">
</p>  

Tag analytics methods such as [/toptags](https://docs.coin.kred/v1.0/reference#toptags), [/trendingtags](https://docs.coin.kred/v1.0/reference#trendingtags) and [/populartags](https://docs.coin.kred/v1.0/reference#populartags) can be used to provide search suggestions.  Top tags are relative to the current user (based on coins they have minted or collected), while popular and trending tags are global.
