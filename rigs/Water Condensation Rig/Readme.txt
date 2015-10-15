Sooo this is the Rig I posted about earlier this week. My original goal was to clean the whole thing up a bit and release it in a few weeks but I got annoyed with trying to fix bugs, which I have no clue where they come from. Therefore you guys get it now and can do with it what you want. If you find fixes for any of the Issues in it please message them to me and i'll try to implement them or do it yourself (I think you can do this on GitHub). This is my first Thinking Particle Setup (as you can probably tell from all the messy Xpresso work) so be prepared for a lot of inefficiencies.

Demo Video: [Link](https://vimeo.com/141888961)

Download: 

**Tutorial on how to use the thing:**

1. Set one Polygon Selection, where you want the Droplets to appear and one, where your want the Streaks to appear (Use the provided Geometry for Reference).
2. Drag you Geometry, you want to have the Droplets appear on into the Base Object Slot in the Droplets tab.
3. Drag the Selection, where your want the Droplets to appear into the Droplet Selection Box
4. Play with the Settings in the Droplets Tab.
5. You can just move the „Remove Droplets“ Effectors Position inside the Rigs Null to change, were you want the Droplets to be removed.
6. I suggest turning both Visibility options off before proceeding to the next step because this will increase Viewport Performance dramatically.
7. Move on to the Streaks tab and drag the selection, where you want the Streaks to appear into the Streak Start Selection Box.
8. Play with the setting in the Streaks tab until you like the result. Press play to see how the Simulation looks.
9. If you cannot get the simulation to look right try changing the Position of the Attractor Position Null. Also try playing with the "Streak Attraction Variation" and "Follow Pos".
10. Move on to the Bake tab and press Ready to Bake.
11. Open the Rigs Null and go to Streaks -> Bake. There you will find 7 Cloners with a Morgraph Cache Tag on them. 
12. Select all of the Cache Tags ans Press Bake. [Reference](http://imgur.com/881v3ML)
13. Once it is finished go back to the Rig and tick the „Turn TP Calculations“ as well as the „Remove Droplets on Stroke Path“ Boxes.
13. *Standard:* You would need to create you own materials for the Standard Renderer because with all the layers of Refraction / blurry Reflections it renders too slow for me to give you guys a setup, which looks good enough. Just mimic the way the Octane Shader is built inside the Standard Materials.
14. *Octane:* Select the "Bake Texture Droplets" Tag, choose a file path and press bake. Select the "Bake Texture Streaks" Tag, choose a file path and press bake. [Reference](http://imgur.com/a/5bUGO) Go into Photoshop and composite the Layers together according to the Images and the .psd file. Go into the „Octane Glas Mix“ Material and load the two Images into the Image Texture Nodes in the Amount Slot of the Mix Material and Color Correction Texture Slot of the "clear glass" Material [Reference](http://imgur.com/rRtev37). If you want to animate the Rig as I have in the demo video you need to bake the "Bake Texture Streaks" Tag every frame manually (go one frame forward, bake, repeat) because the inbuilt option to bake the Animation doesn't seem to recalculate the entire Scene every frame.

**Known Issues:**

* **When you import the Scene into other project files the Thinking Particle Setup breaks. The Issue here seems to be that Cinema doesn't copy the links for the Thinking Particle Groups over to the new file and therefore all Ports connected to them are broken. I have not been able to find a fix for this and see this issue as the major Downfall of this Rig.**
* When you load / reload the Scene the Matrix Objects generating the Thinking Particles Break. (You will see particles all over the Object)
**Temporary Fix:** Go to the „Particle Emission“ Null (Streaks -> Particle Emission) Open up it’s Xpresso tag and replace the 4 Matrices Primary 1-3 & Middle on the Right with the Inputs „Selection“ , „Seed“, „Count“. Use the broken Object nodes as reference for where to plug the ports into.     [Reference](https://imgur.com/a/QH5xI) This to annoyingly be done every time you reload the file.
* Particles will randomly fly off the surface
**Fix:** Particles are being affected by the Motion Inheritance too much. To compensate for this either lower „Streak Direction Variation“ / „Follow Position“ and / or increase the „Surface Attraction Strength“.
* Particles are passing trough your Surface
**Fix:** Change the Primary and / or Secondary Collision Detection to Geometry. Having all of them on Geometry might cause your Cinema 4D to crash.


**What every button does:**

*Droplets*
    
    Amount:
    This Value defines the Amount of Droplets, which are generated. The Value does not represent the actual amount. The Amount scales exponentially, so be careful with large numbers here.
    
    Base Object:
    Drag the Object you want the Droplets to appear on in here.
    
    Droplet Selection:
    You need to create a Polygon selection tag to set, where the Droplets appear on. 
    
    Droplets Offset:	
    This Value defines how far the the Clones are offset in the local z direction from the Surface you defined.
    
    Size Multiplier:
    This multiplies the Scale of the Clones.
    
    Size Blend:
    Value blends from 0 - 2 how many of the larger vs. smaller clones appear. A Value of 1 will have the default distribution, while 0 will only show the larger ones and 2 only the small ones.
    
    Layer Visibility Offset:
    When you open the Rig Null you will find the an Effector named „Remove Droplets“ changing its position will remove the droplets according to a Gradient. This offset allows you to remove more of the bigger Droplets closer to the Effector.
    
    Random Seed:
    This Value changes the random distribution of the Clones on the Surface.

    Visible in Editor / Render:
    These Checkboxes make the Cloners invisible in the Editor / Render. When both are off the Cloners will no longer be calculated (This dramatically increases Viewport Performance).
    
    
*Streaks*
    
    Streak Drop:
    Drag the Geometry in here you want to be used for the tips of the Streaks. You can use the already existing  Objects as reference for you own.
    
    Streak Start Selection:
    Drag a Polygon Selection here to define, where The Streaks will start.
    	
    Streak Amount:
    This Value multiplies the Amount of Streaks Generated. 
    
    Streak Size:
    This Value multiples the Scale of the Geometry you have set previously.
    
    Streak Direction Variation:
    The Streaks (Thinking Particles) follow two rotating Nulls to give them some random direction. This Value controls the Size of a Falloff, which is controlling the Strength of this effect.
    
    Follow Postion:
    This Value is very similar to the Streak Direction Variation as it controls the overall strength of the Particles following the rotating Nulls.
    
    Surface Attraction Strength:
    The Particles are not actually sticking to the Surface but rather are following a circular attractor, which can be controlled with the „Attractor Position“ Null. This Value multiplies the Strength of this Effect.
    
    Friction Offset:
    When you increase this Value the Friction the Particles have of the Surface is increased.
    
    Alignment Smoothing:
    When this Value is increased it prevents the Particles form quickly changing their Orientation to align with the surface they are colliding with. 

    Middle Streaks Amount:
    These Streaks are the Tiny ones indicated by the yellow dots. The Value is a multiplier of their amount
   
    Split Time Offset:
    This Value offsets the time, when the secondary Streaks separate from the primary ones.
    
    Random Seed:
    This Value changes the random distribution of the Particles in the Selection.
    

*Bake*
    
    This only bakes the Animation of the Streaks. It needs to be baked for consistency as well as the Proximal shader to work.
    
    Ready to Bake:
    This will enable the Cloners in the Bake Null as well as hide the Thinking Particles in the Viewport.
    
    Turn TP Calculations Off:
    This will turn all the calculations of the Thinking Particles off. Use it only one you have baked the Animation. If you want to make changes later to the Animation after having deleted the Cache of the Cloners you need to uncheck this box to see the Streaks again.
    
    Remove Droplets on Streak Path:
    This only works after having baked the Animation and enables a Shader Effector with a Proximal shader to remove the Droplets, where the particles have been.
    

*Expert Settings*
    
    Proximal shader detail:
    This will increase the amount of Trail particles generated. It can be useful if you are getting circular artifacts in the Proximal shaders texture, where the Particles are moving fast.
    
**Thanks a lot Guys. I hope you enjoy the Rig**

TL;DR: click the Download Link and watch the Spaghetti Monster in the Xpresso Tags