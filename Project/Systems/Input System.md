For this project the EnhancedInputSystem is used. It is the new and updated version which comes standard in UE5.1 of the old Input system. In this system you can change the mapping easily and add with much ease new inputs. You have complete control over how the action is recognized in play mode. You can change the modes from hold to pressed and so many more. I used a mix of this to get the correct inputs for my system. This way I can manipulate the Gaits and Stances necessary in the ISAPlayerCharacter. When input is given the Input_On(ActionName) is called. 

I'll take the Input_OnCrouch function as an example:  
- InputAction Crouch is set with Pressed trigger (this means it only triggers when the key is pressed)
- System checks which stance you are currently in -> GetStance
- If you are standing, the DesiredStance is set to crouching and vice versa.
- Then in the SetDesiredStance the ApplyDesiredStance is called, in here its more logic to see if you can actually crouch, depending on if you are Grounded or InAir or if you want to roll.
- Calls Crouch or UnCrouch function accordingly

Some Input_OnAction have multiple use cases. This way you save on the amount of buttons you have to use to control your player. For example the Jump action also activates the Mantle logic when you are close to a wall. Otherwise you will go into the normal use case so in this case that will be jumping.

This way the complete input system is implemented in C++, whereas in the [Zippy](Resources) prototype project it was implemented trough blueprints. 

---