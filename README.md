java c
31263 / 32004 Game Development
Lab Week 8
Getting Started
1. Download the corresponding week’s zip file from this week’s module on Canvas.
2. Unzip the project folder and open it in Unity. If there are any warnings about difference in versions, just continue. If this causes any red errors in the console once the project opens, notify the tutor.
3. Within the weekly folders there are image and executable files starting with “Status…”. These files give you a preview of what is expected for each point percentage below.
a. If you are on Mac and the Status-100Percent App file won’t run, hold control and click (right click) then select Open, if there is a security warning, acknowledge it an press open again.
i. If you still have trouble, you may need to change the permissions of the file with the following command in a Terminal window: chmod -R +x Status-100Percent-Mac.app/Contents/MacOS
b. If you are running the Windows executable on the lab computers, you need to copy the entire executable folder into Windows(C:)/Users//AppLockerExceptions. From there you can double run the .exe file.
Tasks
Points                                                                                       Requirements
40%
Scene Set-up
• Drag the Floor prefab from the Project Window into the Hierarchy Window and make sure its position and rotation are zeroed.
• Drag the Player prefab into the Hierarchy Window and make sure its position and rotation is zeroed and scale is set to 1.
o Change the Y position to 0.12 to have the character standing on top of the floor.
• Create an Empty Gameobject in the Hierarchy View called BackgroundMusic
o Attach an AudioSource component.
o In the Inspector Window with the BackgroundMusic gameobject selected, next to AudioClip to see valid audio clips in the Project Window. Select the BackgroundMusic audio clip.
o Make sure “Play on Awake” and “Loop” are ticked in the Inspector Window.
There is no ProgressEvaluator for this week. Please view the Status-100Percent video and executable, as well as the other Status images, to check your own progression.
50% (P)
CharacterMovement Script. Variables and Methods
• Create a new script. called CharacterMovement
• In CharacterMovement:
o Create the following member variables
 private Vector3 movement;
 private float movementSqrMagnitude;
o Create the following methods
 void GetMovementInput() {}
 void CharacterPostion() {}
 void CharacterRotation() {}
 void WalkAnimation() {}
 void FootstepAudio() {}
o In Update(), call all of the above methods in the above order.
o Delete the Start() method
• Attach the CharacterMovement component to the Player gameobject.
60% (P)
Movement Vector
• Go to the Input Manager window and make sure that:
o The Horizontal Axis has Positive Button is set to “d” and Negative Button set to “a”, Gravity 3 and Sensitivity 3.
o The Vertical Axis has Positive Button is set to “w” and Negative Button set to “s”, Gravity 3 and Sensitivity 3.
• In the GetMovementInput() method of the CharacterMovement script.
o Set the x value of the movement vector variable to the value of the Horizontal input axis (tip: see Input.GetAxis(….)
o Set the z value of the movement vector variable to the value of the Vertical input axis.
o Store the squared magnitude of the movement vector in the movementSqrMagnitude variable (tip: see Vector3.sqrMagnitude)
o Print the movement vector out to the console.
70% (C)
Position and Rotation
• In CharcterMovement, create a public variable called walkSpeed with a default value of 1.75f.
• In CharacterPosition() in the CharacterMovement script.
o Move the current gameobject in the direction specified by the movement vector and Transform.Translate().
o Press play and use the a,s,w,d to move.
o Combine the movement vector with the walkSpeed variable and make it frame. rate independent when moving the game object.
o Press play and move around
• In CharacterRotation()
o Set the Player gameobject’s rotation using the direction specified by the movement vector (without the walkSpeed variable or frame. rate independence).
(tip: see Quaternion.LookRotation(…) )
o Press play and move around
• Notice that the position update is all wacky now with the rotation
o This is because the Transform.Translate() defaults to local space translation, which is affected by an object’s rotation.
o Set Transform.Translate() to use Space.World.
o Press play and move around.
• Notice the warnings and that the character pops back to facing forward after stopping its movement.
o Only do the rotation if the movement vector is not a zero vector.
o Press play and move around.
• Notice that the Player moves faster when moving diagonally than moving just vertically or just horizontally.
o This is because a vector of (1,0,0) (e.g. moving positively in the x-axis) has a magnitude of 1. However the vector (1,0,1) (e.g. moving diagonally in positive x and z) has a magnitude of about 1.4.
o In GetMovementInput(), after setting the x and z variables of the movement vector but before the sqrMagnitude of the movement vector is stored:
 Use Vector3.ClampMagnitude(…) to clamp the magnitude of the movement vector to 1.0f.
80% (D)
Animation
• Comment out the console printing of the movement vector.
• Add an Animator component to the Player gameobject.
o Press the circle button next to Controller to see valid AnimatorControllers in the ProjectWindow. Assign the MovementAnimator controller.
o Press the circle button next to Avatar and select PlayerAvatar.
o Make sure “Apply Root Motion” is unticked, “Update Mode” is normal, and
“Culling Mode” is set to “Cull Update Transforms”.
• Go to the menu option “Window->Animator” and dock the Animator Window somewhere such that you can see the Game View and the Animator Window at the same time.
• Select the Player gameobject to see the state machine of the MovementAnimator
• Select the Parameters tab in the Animator Window and create a new parameter called MovingSpeed.
o Select the transition line that is pointing between the states PlayerIdle to Walking.
 In the Inspector, untick “Has Exit Time”
 In the Inspector, under Conditions, add a new condition that MovingSpeed is Greater than 0.1.
o Select the transition line that is pointing between the states Walking to PlayerIdle.
 In the Inspector, untick “Has Exit Time”
 In the Inspector, under Conditions, add a new condition that MovingSpeed is Less than 0.1.
• In CharacterMovement, create a public variable to store the animator of the Player gameobject.
• In the WalkAnimation() method
o Set the Movin代 写31263 / 32004 Game Development Lab Week 8Java
代做程序编程语言gSpeed parameter of the Player’s MovementAnimator to have the value of the movementSqrMagnitude.
• Press play.
90% (HD)
Footstep Audio
• Add an AudioSource component to the Player gameobject in the Hierarchy Window.
o Set the AudioClip of the AudioSource to be Footstep01 (found under Audio Clips -> FX in the Project Window).
o Set the Pitch of the AudioSource to be 1.1 and make sure Play On Awake and Loop are unticked.
• In CharacterMovement, create a public AudioSource variable called footstepSource and assign the newly added audio source to it.
• In the CharacterMovement script, create a public array of AudioClips call footstepClips.
o In the Hierarchy Window, set this array to a size of 2 and assign Footstep01 and Footstep02 from the Project Window.
• In CharacterMovement, also create a public AudioSource reference to the background music audio source.
• In the FootstepAudio() method:
o If the movementSqrMagnitude is greater than 0.25f and the audio source isn’t already playing a clip then:
 Associate the other clip in the footstepClips array with the audio source.
• This way, the audio flip-flops from one clip to the other (i.e. there is a right foot clip and a left foot clip)
 Set the volume of the audio source to the movementSqrMagnitude variable.
 Play the audio source
 “Duck” the background music volume by reducing it to 0.5f.
o Otherwise, if movementSqrMagnitude is less than or equal to 0.3f and the footstepAudioSource is playing then:
 Stop the footstepAudioSource from playing.
 Return the background music to 1.0f;
• Press play (with headphones or speakers)
100% (HD)
Collisions
• Player’s Collider:
o Select the Player gameobject. Notice that there is currently no collider on the player.
 It is not actually interacting with the floor of the game, it is just that our animation and positioning makes it look that way.
o Add a CapsuleCollider component to the Player.
 Give this a Center of (0,1,0) and a Height of 2
 In the Scene View, with the Player selected, you should see a green capsule that roughly encompasses the character model.
o Add a Rigidbody component
 Set the Constraints of this Rigidbody to freeze the x, y and z rotation. This will stop our character from falling / rolling over due to gravity and the nature of our rounded bottom capsule collider
• Trigger:
o Create a new Cube primitive GameObject and place it at position (-2.5,1.5,0)
 Rename this to “Trigger Box”
o Notice that this Cube already has a BoxCollider component on it.
 Make this Collider a Trigger.
o In the CharacterMovement script, use the OnTriggerExit() method so that when the player STOPS colliding with the trigger, the following is printed to the console “Trigger Exit:  : ” where  is the name of the gameobject that the trigger is attached to and  is the current position of that gameobject. E.g. the output may be “Trigger Enter: Trigger Box : (-2.5, 1.5, 0)”
o Press play and walk through the trigger.
• Rigidbody Collider:
o Create a new Cube primitive GameObject and place it at position (2.5,1.5,0)
 Rename this to “Physics Box” and add a Rigidbody component to it.
 Add a Rigidbody component to this Physics Box
o In your CharacterMovement script, use the OnCollisionEnter() method so that when the player BEGINS colliding with the box, the following is printed in the console “Collision Enter:  : ” where  is the position of one of the touching points of the collision (see Collision.contacts, just use the first element of the array)
 Note the difference between the method parameters for OnTrigger…() methods and OnCollision…() methods.
• Static Collider:
o Create another Cube primitive, place it (0,1.7,4) and with scale (5,3,1)
o Rename this to “Wall”.
 Create new tag called “Impassable” and give the Wall gameobject this tag.
 Notice that the attached BoxCollider is affected by the scale of the gameobject so it is automatically stretch to fit the scale of the wall.
 Also notice that without a Rigidbody component, this Wall is now a Static Collider
o In CharacterMovement, use the method OnCollisionStay() to detect when a gameobject with the tag “Impassable” has been collided with and print out “Collision Stay: ” in the console.
o Press play and walk into the wall
• Raycasting
o Create a new Cube primitive and place it at (0, 1, -4)
 Rename this “Enemy” and give it a new tag called “Freeze”
o Create a new method called RaycastCheck() that returns a bool
 In this method, perform. a Raycast from the Player’s position plus (0,1,0) (because otherwise the raycast would shoot from the feet and not be high enough for the enemy), facing forward from the Player, and with a distance of 5 units.
 If the raycast hits something
• Print to the console “Raycast Hit: ” with the name of the first gameobject that was hit by the ray
• Check if that gameobject has has the tag “Freeze” and return true, otherwise return false
o In Update()
 Call RaycastCheck()
 If it returns false, perform. the actions as normal
 If it returns true, prevent the position, animation, and audio from being updated, but allow the rotation to occur as normal.
 The resulting behaviour is that the player cannot move towards the Enemy (see Status-100Percent)
• CLEAN, EFFICIENT, ELEGANT CODE!
Bonus
Submit your work on Canvas before continuing. Follow the instructions on the last page.
This part is optional. If you completed the above activity very quickly, try this. It is not graded, but it will enhance your skill.
Jumping, falling and walking up slopes (without using the in-built CharacterController)
• For this challenge, implement character jumping.
• Explore Mixamo ( https://www.mixamo.com/ ) to find a suitable jump animation and a falling animation.
o Use the character model from this week’s lab to create new animations for it in Mixamo - https://youtu.be/9H0aJhKSlEQ
• For jumping, only allow jumping when the character is on the ground
o Instead of using a Rigidbody component to handle gravity, instead move the character upwards (using the movement vector) for certain amount of time to achieve the jump
o Make sure to do the reverse downward motion to sync up with your animation
• For falling, if the player is not on the ground and traveling in the downwards direction, use a downwards raycast to detect if the player will be falling by a threshold distance (e.g. more than the normal jump height).
o If so, play the falling animation and move the player downwards.
o Try to simulate acceleration so that the speed is increasing the longer the character is falling.



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
