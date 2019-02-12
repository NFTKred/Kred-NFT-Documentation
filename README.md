This guide shows how you build your own app using the Coin.Kred API.

### Home Page
<p align="center">
  <img width="80%" src="https://files.readme.io/68ba12d-CK_Explore.PNG" title="Explore">
</p>  

Our home view is the Explore tab.   We've created this with three calls to the [/coins](ref:coins)  method, sorting respectively by likes, creation date, and circulation.  Each of these calls can be paginated, so that the groups of coins are bound to individual carousels and can be browsed by the user.

