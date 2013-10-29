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

/########################\
|SETUP - API Use (MANUAL)|
\########################/

1. In the computers "home" directory (see step 5 of the above setup step) create a new file called prog.
   NOTE: Please ensure you can see file extensions and that the file is simply prog. any extension
   (such as .txt) can cause problems with this tutorial! (google is your friend if you cannot find out
   how to see file extensions!)
2. Open this file with a text editor.
3. 

################(COPY THE LINE BELOW THIS LINE)###################
-- This line is ignored because of the dashes preceeding this text! You can type messages using these comments --
-- Variables --
-- This ID is used to give your save location a unique ID removing the chance of conflicting programs --
-- Change this variable to anything you wish (making sure it's enclosed in double quotes) --
local ID = "myID"
local locTable={ ["x"]=0, ["y"]=0, ["z"]=0, ["dir"]=0}

print("Welcome to this tutorial!")
print("We shall load the api now!")

-- this lets the terminal display the message for 2 seconds before moving on, by "pausing" the os for 2 seconds.
os.sleep(2)   
-- think of os.sleep() as a pause function --

--Check to see that the api exists!--
--NOTE: Please make sure that the text in the double quotes below is the location of your apiMove file --
--NOTE: If you have your apiMove inside a folder, replace the API part with the name of that folder --
-- E.G. if(fs.exists("folderName/apiMove")==false)then
--NOTE: If you have your apiMove in the "home" location (see step 5 again to find this) then simply replace "API/apiMove" with "apiMove" --
-- E.G. if(fs.exists("apiMove")==false)then

if(fs.exists("API/apiMove")==false)then
   print("ERR: Api not found! Check your api Location!")
   return
end

-- If you don't get the printout saying it wasn't found, you've successfully found the api in the location you've supplied! --

os.loadAPI("API/apiMove")
print("apiMove loaded")
os.sleep(2)


--We have to initialise the api with our ID so it can store the ID for saving our coordinates uniquely --
print("Init apiMove")
apiMove.init(ID)
print("apiMove initialised!")

-- This section automatically loads the API coordinates into a table called locTable (defined above) --
-- If they aren't found (they won't be the first time this is run, the turtles current position will be defined as the "home" position --
print("Loading api coordinates..")
if(apiMove.loadCoordinates(ID,locTable)==false)then
   print("No coordinates found!")
else
   print("Coordinates Loaded!")
end
os.sleep(2)


-- This functions checks if the turtle is at 0,0,0,0 and then asks if you would like to send the turtle home! --
-- NOTE: This will only work upon moving the turtle (using the api), quitting then reloading the world, and then finally running this program --
if(apiMove.isHome(locTable)==false)then
   print("Should I go home first? (y/n)")
   input=io.read()
   if(input=="y")then
      print("Moving home now!")
      apiMove.goHome(locTable)
      print("I should be home!")
   end
end
os.sleep(2)

--Start taking in user input to move the turtle --

print("Starting program!")
os.sleep(2)
clearScreen()
while true do
   print("Please enter some coordinates!")
   while true do
      print("X: ")
      x = io.read()
      if(tonumber(x)~=nil)then
         print("Thank you!")
         break
      else 
         print("ERR: Please try again!")
      end
   end
   os.sleep(1)
   clearScreen()   
   while true do
      print("Z: ")
      z = io.read()
      if(tonumber(z)~=nil)then
         print("Thank you!")
         break
      else 
         print("ERR: Please try again!")
      end
   end
   os.sleep(1)
   clearScreen()
   while true do
      print("Y: ")
      y = io.read()
      if(tonumber(y)~=nil)then
         print("Thank you!")
         break
      else 
         print("ERR: Please try again!")
      end
   end
   os.sleep(1)
   clearScreen()
   while true do
      print("Please enter a direction to face! (0-4 where 0 = original direction when turtle started)")
      dir = io.read()
      if(tonumber(dir)~=nil)then
         print("Thank you!")
         break
      else 
         print("ERR: Please try again!")
      end
   end
   os.sleep(2)
   clearScreen()
   print("Coords entered were: ("..x..", "..z..", "..y..")")
   print("Moving there now!")
   apiMove.goToCoords(tonumber(x),tonumber(y),tonumber(z),locTable)
   apiMove.faceDirection(tonumber(dir),locTable)
end
os.sleep(1)

apiMove.saveCoordinates(locTable)
print("End of test")
