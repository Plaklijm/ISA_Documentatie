>Downloaded ALSV4 Refactored
>
>Started Dev Document
>
>Reverse engineering started:
		Made a basic overview about the ALS System, written down: Character dependency graph, States, Settings, Utility, Modifiers. Written down all the script files to get an idea of how the system in a global view worked
>
>Made an overview about the Character Movement Component (CMC)
>Followed Zippy tutorials about the Character Movement Component:
		 Written the logic behind the CMC down. He explained a lot more, for example he went pretty deep into networking and multiplayer. Because the CMC has a robust system for that. But because I made a non networked game I could've skipped this part, but it helped a lot into understanding the logic behind the CMC and made it easier to understand what part of the ALS system I didn't need and what parts I did need.
>
>When I had a global basic understanding of how this system worked I followed the [Zippy](Resources) tutorial, with this I created a basic Locomotion system where you could walk around, jump, and crouch. I used this as the basis of the eventual big project. 
>
>Made new Project with the name ISA, based on the Zippy project. 
>
>Refactored the code and started to develop this system further
>
>Made IDE switch, from visual studio 2022, to Jetbrains Rider. This was done in order to improve my workflow with Unreal Engine, The moment I switched I could notice the difference:
>		Better Intellisense, in visual studio this was so slow that I couldn't depend on it. This was very noticeable because I'm not  really familiar with the syntax UE uses. So this was a huge help, Rider also helped with recompiling the engine, because the codebase is huge, and you need to recompile it pretty often (I code mostly with the editor closed to prevent compile glitches in blueprints) and if you need to rebuild the editor a few times you can notice the performance difference.
>		
>Started working on the [[GameplayTag system]]
>
>Added simple Debug system where I could see what state the player is currently in. Used in the build in engine Debug mode.
>
>Further improvements regarding the [[GameplayTag system]] 
>
>I've changed the current ISACharacter to the ISACharacterBase class and made a new ISAPlayerCharacter class which inherent from the ISACharacterBase. This way I made a separate class that includes the whole [[Input System]]. And in here some switching of tags happen.
>
>Learned how to use breakpoints in Rider and fixed a nullptr bug that way. For this you need to build the editor in DebugGame mode and compile it in Debug mode. This way when you hit play you get sent into the IDE for you to follow your  breakpoints and figure out what variable is set with what value.
>
>Started work on the sliding system and with that the [[Animation System]]
> 
> Abandoned the sliding system. This was already somewhat implemented in the [Zippy](Resources) project, and connecting the 2 separate systems was not the order of the day so I went on and started working on the Mantle and Vault system (Action System).
>
>Changed the Vault system to work with root motion and therefor I was able to make use of the Motion Warping system
>
>Started working on the interaction system using C++ interfaces
>
>Moved from Interfaces to Delegates in C++ to make something interactable with a box collider
>
>Fixed Vaulting, you could vault through a wall, but this is no more and I Reworked the animation system. (Animation is not my strongest area. So I've decided to focus less on the robustness of the animation system in comparison to the codebase itself)
>
>Vaulting animation Height fixed, Sliding is also fixed. You can enter and exit a slide normally, animation is also added.
>
>Revisited the interaction system, moved back to an Interface instead of a Delegate, it seemed in hindsight a better option to go with an Interface. This way the system is more robust. With this new interaction system I started working on the Push and Pull boxes.
>
>Updated the door interaction system to work with the new interface protocol.
>
>Final revision: Little bug fixes and code clean-up.

