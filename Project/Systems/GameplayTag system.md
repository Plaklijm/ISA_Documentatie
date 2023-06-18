Unreal uses a robust system called GameplayTags, This way you can declare and define tags used by your locomotion system, or whatever you need it for. The way it works is that you declare your tags with a name in a namespace in a separate header file (this way all the GameplayTags are confined to one file, making it easier to add/remove and keep overview) and define them in your CPP file. In your CPP file you also declare the hierarchy they abide by. 
Example:
- ISA.LocomotionMode.Grounded <- you can separate this tag in 3 parts:
	Family.Genus.Spicies <- example of the hierarchical properties of the tag system	
	- ISA <- this is the broadest identifier tag, here you can define what family the tags are in. For example: Humanoid 
	- LocomotionMode <- The second tag is used to get something out of the main tag, here you can narrow the use case for the tag you're after.
	- Grounded <- this is the most specific of the tags. This is the one I use to get if the player is grounded or not.
When you have declared the tags in your .h and .cpp file you also need to let the engine know what tags have been added, this can be done in the DefaultGameplayTags.ini file in the config folder. You also need to add the GameplayTags module to the Build.cs file so when the engine is build, it uses the GameplayTag system and recognizes the tags you added. 
(*I was making this system and the engine couldn't recognize the tags I added, turned out I needed to add the module to the build file, took me 30 min to fix, but now I know for the next time*)

---

#### Gameplay tags used in my system:

ISALocomotionModeTags
- ISA.LocomotionMode.Grounded
- ISA.LocomotionMode.InAir

ISAStanceTags  
- ISA.Stance.Standing
- ISA.Stance.Crouching

ISAGaitTags  
- ISA.Gait.Walking  
 - ISA.Gait.Running  
- ISA.Gait.Sprinting
  
ISALocomotionActionTags  
- ISA.LocomotionAction.Rolling
- ISA.LocomotionAction.Mantling
- ISA.LocomotionAction.Sliding

With these tags I can monitor and define the states the player is in. It is a version of the Finite State Pattern but in another way. Using this system every system the player uses can be aware of the state of the player. For example the [[Animation System]] Can now see what state the player is in and play animations accordingly.

---

#### Tag Functions:

The Tags get switched in multiple functions, but there are some main ones which handle them:
1. Getters, when called these get the current tag. 
	- for example: GetLocomotionMode() { return LocomotionMode; }
2. Setters, when called these set the tag to whatever you want the new tag to be. 
	-  these have systems in them so you cant set the CurrentTag to the NewTag. Depending on if its necessary these setter also make a PreviousTag, This can then be send to a Notify function.
3. Notify, when called this will notify the system a Tag has been changed. 3.
	-  for example: NotifyLocomotionModeChanged{ here you can apply logic where the current and previous mode are known. Like Roll on the ground when the previous is InAir and current is Grounded.}
4. Apply, when called this applies certain logic based on the Tag. 
	-  for example: ApplyDesiredStance{Makes the player Crouch or UnCrouch when certain parameters are met. Like when InAir you UnCrouch}
5. Calculate, When called this calculates a certain Tag. 
	-  For example: CalculateActualGait{Calculates the actual gait the player is in, this can differ because when you go from sprinting to walking, you wont be in the sprinting Gait unless you have accelerated enough to be in the Sprinting gait}
