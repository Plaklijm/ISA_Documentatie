### Mantle/Vault System
The Mantle/Vault system is a pretty basic system based upon Motion Warping. This is a feature in UE5 that is still in Beta but it is far enough to be experimenting with it. It takes a root motion Animation Montage where you set certain motion warp notifies. Then when you have new positions you can set the new location of the animation to play to. The system will then automatically warp your root motion animation to match the new locations.

You can split this system up into 5 steps:
1. Forward Trace
	- First the line trace is calculated where it should be send from, then trace forward to see if there is a wall in front of the player, this is done in 3 traces, when one hits it continues to the next step
2. Trace wall Thickness
	- The hit result of the Forward trace is used to set new traces, these traces check the thickness of the wall and determine if it is vaultible or not
3. Check Landing position
	- You send out one last trace after the last thickness trace, this one will determine the landing place of the player. 
4. Set variables
	- The first location of the thickness trace will be the vault start position, then the last of the thickness trace will be the vault middle position and the last trace will be the vault end position. These are stored in a separate DataAsset made for everything related to vaulting.
5. Setup Vault
	- And finally the logic is put to work and the MovementMode is set to MOVE_Flying, and the collision is turned off, then an Animation montage of the vaulting animation is played and when the animation is done playing, the MovementMode is set to MOVE_Walking and the collision is turned on again.
![[Pasted image 20230531152459.png]]

With this system it is possible to vault dynamically. The vault isn't bound to any form of object or size. You can set a maximum amount of traces which will determine how far you can vault. Anything in between is calculated and warped. This means you get results like this:
![[Pasted image 20230604195408.png]]
![[Pasted image 20230604195521.png]]
The above picture is vaulting over a thick wall, the one below is vaulting over a thin wall. 








#### Interaction System

The interaction system is handled via the InteractionBase class. In this class I declare a dynamic multicast delegate (Unreal Engine's own macro). The interaction system is handled via this Delegate. In the BeginPlay of the base class the delegate is declared with a function that is called when OnComponentBeginOverlap is called on a box collider. This OverlapStarted function gets called and then it broadcasts the function call to every listener. In this case is the player a listener and a blueprint exposed function is called. Then in blueprints the function handles the correct animation and motionwarp target. As an example I implemented this functionality by opening a door. 

This system was the old one. When I developed this I quickly came across the limitations of using delegates. It is a very powerful tool to use, but for an all-round interaction system its not really that easy and straightforward to use. That's why I rewrote this system to use Interfaces instead. This way I can define new base classes for interactables and add some standard functions that every interactible should have. 