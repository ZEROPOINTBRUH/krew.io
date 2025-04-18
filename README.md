# krew2
This is the repository for a cleanup of Krew.io.

**Running in development** (using grunt-nodemon as a watchscript)
``npm run dev``

**Running in production** (using pm2 to keep process alive)
``npm run prod``

Running in production mode serves to ``localhost:8200``.
Running in dev mode serves to ``localhost:8080``.

In production, Nginx proxies the local webfront port to 443 and redirects 80 to 443. 

### Admin Commands
 ```
 !!login
 ```
 - Set playerEntity.isAdmin to ``true`` (otherwise other admin commands won't work).

 ```
 !!say <message>
 ```
 - Send an admin message to all players online.

 ```
 !!whois <seadog123>
 ```
 - Get player ID of specified seadog (in this case seadog123).

 ```
 !!kick <Identifier> [reason]
 ```
 - Disconnect a player's socket connection (kick them) and display reason on his screen.
 - Identifier can be either a playerID or displayname.
 - Reason is optional.

 ```
 !!ban <Identifier> [reason]
 ```
 - Disconnect a player's socket connection (kick them) and display reason on his screen.
 - Additionally adds them to the permanent ban list, barrciading them from using their account.
 - Identifier can be either a playerID or displayname.
 - Reason is optional.

 ```
 !!unban <Identifier>
 ```
 - Removes a user from the permanent ban list and sends a webhook to Discord.
 - Identifier can be either a playerID or displayname.
 - Reason is optional.

 ```
 !!nick <name>
 ```
 - Set the name in the chat to a specified string (for easier admin communication).

 ```
 !!restart
 ```
 - Saves the current game progress of all players which are logged in. Then, disconnects all players from the server.
 - Detailed information about how to smoothly restart the server is located further down in this document.

 ### Mod Commands
 ```
 //login
 ```
 - Set playerEntity.isMod to ``true`` (otherwise other mod commands won't work).

 ```
 //report <Identifier> [reason]
 ```
 - Report a player (sends him a warning and a webhook message to Discord. When a player gets reported the second time, he is kicked from the server).

 ```
 //mute <Identifier> [reason]
 ```
 - Mute a player (for 5 minutes) and display a message to him telling him that he has been muted. Sends a webhook message to Discord with the reason.

 ```
 //tempban <Identifier> [reason]
 ```
 - Temporarily ban a player.

 ```
 //ban <Identifier> [reason]
 ```
 - Permanently ban an account. This player will be unable to use this account

## Smooth Server Restart
 - Login to the game with your user account.
 - Authenticate yourself as admin in the chat:
 ```
 !!login
 ```

 - Save the current progress of all players and "kick" them from the game.
 ```
 !!update
 ```
 - The game will automatically kick all players and pull the latest commit from GitHub. Once done, it will restart itself and allow players to join back.

## Documentation

#### netType (network types):
 ```
 -1: Entity
 0: Player
 1: Boat
 2: Projectile
 3: Impact
 4: Pickup ( Fish / crab / shell / cargo / chest)
 5: Island
 6: Bot
 ```

#### Ship states:
 ```
 -1: Starting
 0: Sailing
 1: Docking
 2: Finished Docking
 3: Anchored
 4: Departing
 ```

#### Projectiles:
 ```
 0: Cannonball
 1: Fishing Hook
 ```

#### Weapons:
 ```
 -1: Nothing
 0: Cannon
 1: Fishing Rod
