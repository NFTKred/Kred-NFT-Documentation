This guide shows how you build your own app using the Coin.Kred API.

### Home Page
<p align="center">
  <img width="80%" src="https://files.readme.io/68ba12d-CK_Explore.PNG" title="Explore">
</p>  

Our home view is the Explore tab.   We've created this with three calls to the [/coins](https://docs.coin.kred/v1.0/reference#coins)  method, sorting respectively by likes, creation date, and circulation.  Each of these calls can be paginated, so that the groups of coins are bound to individual carousels and can be browsed by the user.

<p align="center">
  <img width="40%" src="https://files.readme.io/d79c8a4-Spacecoin.png" title="Batched coin">
</p>  

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
