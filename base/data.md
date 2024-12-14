# Data

## Data Type

UltimateShop has 2 data types, they are: Player Data and Server Data.

Player data saves player self data, like each product buy times and sell times, cooldown times, and other things.

Server data saved server total product buy times, sell times and so on. Random placeholder's data will also saved in server data.

## Save&#x20;

For player data, we will auto save player data into database when player leave the server.

For server data, we will auto save server data when you are trying to stop the server normally. (Not directly close the console window, you need use /stop command in server)

Data not saved will be lost after server crash, so enable auto save feature if you don't want this.
