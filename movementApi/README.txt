      
apiMove by shauno1992

V1.5 - Turtle awareness! (sortof)

/###########\
|DESCRIPTION|
\###########/

This first commit also carries with it the (near) functionally complete movement (api?) program that I've
created. I decided that the turtle doesn't need to use GPS (see the wiki) to know it's location (along 
with a ridiculous amount of computers). The turtle knows where it starts and that is all that matters right? 

Currently the API is able to correctly save the turtles location regardless of it's location, or its current 
action!  (untested with custom functions, but so long as the functions are using the api to move this 
shouldn't change!). The API saves the coordinates of the turtle upon calling the base function moveTurtle(),
which as you can see (take a look) calls saveCoordinates() every single time something changes (either the 
turtles location OR variable changes).Saves are located inside a folder created by the api. Users supply an
ID to the init() function (which is needed in order to use this api!), which is then used for the folder 
name, to avoid other program conflicts and ensure no corruptions of data etc. 

The location the turtle is placed is considered the "home" of the turtle. 0,0,0,0 are the home coordinates, 
in the program they are in the form x,y,z,dir. Facing is the direction which is a number between and inclusive 
of 0 and 3. For the "home" location, 0 is forward, 1 is right, 2 is backwards and 3 is left. 

The turtle basically calls a function that saves it's current coordinates (along with some other variables) 
that allow it to know if something has gone wrong, particularly in the case of the minecraft world shutting
down  or the turtle unloading (not being in loaded chunks). 

Upon loading it's saved variables and coordinates the turtle will then update its coordinates to the correct 
coordinate and avoid becoming lost! (In all cases of movement or turning, the turtle will start it's move/turn 
function but not update and then save it's new coordinates, meaning the turtle thinks it hasn't actually moved,
therefore becoming lost!)  

/#########\
|FUNCTIONS|
\#########/

Other ease of use functions included are basic forward, back, up, down, turn left and turn right functions, 
each with both a default amount of one (move forward 1 for example) and with an overloaded function for a 
custom distance (move forward x).

Other notable functions:
offsetTurtle(dir,sideOffset,forwardOffset,locTable)
~ This function offsets the turtle by the side and forward offsets. These can be user inputted for custom 
  user-specified values!

getTarget(dir,num,locTable)
~ This functions gets the correct target value for the turtle to move or turn, which is determined by the 
  turtles current direction (the direction it's facing), the number of spaces/turns required, and the 
  direction the turtle is moving or turning (front, back, left, right, up, down). It then returns the correct
  x,y,z or direction value + num (in the parameters of the function). This could probably do with some optimizing!

getDirection(dir,locTable)
~ This function returns a string of either "x","y","z" or "turn". Used for determining whether the turtle 
  has moved/turned the correct number of times in the move functions. 

updateFacing(dir,locTable)
~ This function simply updates the turtles facing direction variable for it's coordinates depending on whether 
  it turns left or right. Also checks for overlap, and sets the result accordingly (if dir=3 and turtle turns 
  right, it adds 1 to the dir value. Similarly it minuses 1 for left turns. Another check then makes sure it's 
  between 3 and 0 and if it isn't it sets the value accordingly)

faceDirection(dir,locTable)
~ This functions makes the turtle face a direction specified by the parameter dir. 

turnAround(locTable)
~ This function makes the turtle turn around by turning it twice either left or right. Attempted to have this 
  randomised, doesn't seem to work very randomly!

isHome(locTable)
~ Checks for the turtle to be at coordinates 0,0,0,0. Returns false if its not, true if it is. 

goHome(locTable)
~ Tells the turtle to go to 0,0,0 and then face the direction 0.

goToCoords(x,y,z,locTable)
~ Moves the turtle to the x,y,z coordinates specified by the parameters. Systemically checks each direction 
  (0,1,2,3) and either moves forward, backward or turns depending on the coordinates the turtle is located at. 

printLocation(locTable)
~ Prints the location of the turtle. Used in the move() function for displaying coordinates.

/#################################\
|SETUP - API Installation (sortof)|
\#################################/

1. Place a turtle (if you're aiming for a special turtle, mining, lopping etc use those!)
2. Label the turtle! E.G. label set foo in the turtles terminal. This ensures you don't lose your program!
3. Type: edit prog. (substitute prog for the name of your program)
4. Press ctrl, navigate to save, press enter!
5. Navigate to the directory as follows the following format:
   drive:\installPath\modPack\minecraft\saves\worldName\computer\computerNumber
   Explanations:
   ~ drive: the hard disk letter that your FTB/Technic/minecraft is installed in. 
     Mine is E:\ for example (for vanilla minecraft %appdata%)
   ~ installPath: the location your launcher/modpack is installed in. Mine is 
     E:\Games\Feed the Beast
   ~ modPack: the particular mod pack you're using. For FTB the folders can include Unleashed and Unhinged. 
     Mine is E:\Games\Feed the Beast\Unleashed
   ~ worldName: the name of the world you select when you load your singleplayer world). 
     Mine is E:\Games\Feed the Beast\Unleashed\minecraft\saves\Flat Test World
   My entire path is : E:\Games\Feed the Beast\Unleashed\minecraft\saves\Flat Test World\computer\0
   This path contains my program files (and also yours if you have made any!) for making generic programs for a turtle.
6. You can either place apiMove directly in this folder, OR create a folder and place the API inside that. 
   TAKE NOTE OF THE FOLDER NAME FOR LATER STEPS!
7. The api is "installed" so to speak!

/###############\
|SETUP - API Use|
\###############/

Ensure the API is properly "installed" as in the above setup step! This part of the setup will entail a 
tutorial of sorts!

/########################\
|SETUP - API Use (MANUAL)|
\########################/

Check the README-MANUAL.txt file!


/##########################\
|SETUP - API Use (PASTEBIN)|
\##########################/

1. Open your already labelled turtles terminal
2. paste in this to the terminal:
   



   
 
   
   


