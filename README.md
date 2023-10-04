# GreatTenYearExpedition
This is a total overhaul mod for Hearts of Iron IV, currently a WIP

If you would like to play it, download both the GreatTenYear folder and the .mod accompanying it, and place both with HOI4's mod folder 
(located at C:\Users\username\Documents\Paradox Interactive\Hearts of Iron IV\mod). As a side note, make sure to open the .mod file with notepad, notepad++ or VSCode, and edit the path to where your current
install of the GreatTenYear folder actually is.

If you would like to edit the mod at all, I will give a brief overview of how to do some basic actions, YouTube and the internet are great tools when you need more
information or help on a certain subject.

GFX, PORTRAITS and FLAGS:

All portraits for country leaders, generals and the portraits for the characters in the government need to be size 156x210 to function properly, these files also 
need to be in dds format. For leaders, place them into their corresponding country folder at "GreatTenYear\gfx\leaders". 

For example: I want to add a portrait of Kiki to the Sontisian Empire, first I would need to create a folder with the country's tag as its name, SOE in this case.
Next I would create the portrait, making sure its 156x210 and of the dds type, then I would save it into the newly made folder, keeping note of the file name for
later use.

Similarly, flags are placed at GreatTenYear\gfx\flags, and are categorized as large(82x52), medium(41x26) and small(10x7). Currently these are saved as .tga files.
And for a country, name each size with the country tag (EX: SOE), and place in their corresponding location. 
Flags can also be named so they work with a country only when it's a specific ideology, currently there's no implementation for this, but if you want to add some 
extra flags for when a country changes ideology, check vanilla HOI4 flags and how they are named.

CREATING CHARACTERS:

Characters are a relatively recent addition to HOI4, these are used to figure out what characters exist within game and give them to their respective countries as leaders or ministers.

Within the GreatTenYear\common\characters folder, there will be files named after country tags that will hold information about characters that belong to that country. Each character should be within it's own brackets, with their name, gender, portraits, and their 'stats'/information.
For example:

	#EMPRESS KIKI
	SOE_kiki = {  <---- This is the name of your new character, you will reference this
		name = SOE_kiki  <---- This is the name of your character from the localisation file
		gender = female

		portraits = {
			civilian = {
				large = "gfx/leaders/SOE/portrait_SOE_kiki.dds" <-- civilian is used for the country leader portrait,has to be large
			}
			
			army = {
				large = "gfx/leaders/SOE/portrait_SOE_kiki.dds" <-- Used if this character is a general/field marshal
			}
		}

		country_leader = { <-- This is the characters 'occupation' can be also a minister or general, check online for how to represent those
            ideology = despotism <-- MAKE SURE your character possesses an ideology thats in line with your country's! Otherwise it WON'T WORK.
            traits = { agrarian_activist portly_princess } <-- Character traits, list can be found at country_leader in common
            desc = "Fattest Empress Around"
        }

	}

Just to re-iterate, make sure if you're making a character a country leader, that their ideology is apart of the main ideology! Despotism is a sub-ideology of neutrality. You can find a list of the sub-ideologies online or in HOI4's main
files under the common/ideology folder.

Whenever adding a character portrait, ALWAYS USE THIS AS A BASE "gfx/leaders/SOE/portrait_SOE_kiki.dds", making sure to replace SOE with the country tag and the file name with your character's new portrait file name.

Now that the character is created in the file, go to GreatTenYear\localisation\english and open the
nsb_characters_l_english file, using Notepad++ or Visual Studio Code. Inside here, you can add what the name of a new 
character should be (EX: SOE_kiki:0 "Empress Kiki"). Now in game, this character will be called 'Empress Kiki' instead of
SOE_kiki.

To get this character into a country, you must recruit them, inside GreatTenYear\history\countries, find the country you want to add a new character to. Do 'recruit_character = character_name' wherever you see some of the same type, or after set_technology if this country doesn't have characters yet.
 

CREATING A NEW COUNTRY:

Creating a new country isn't very difficult, it will take a bit of time to do so, especially if its your first time. Follow this step by step and you should be able to
have a new country on the map with little to no problems. 

Step 0: (To make it easier, go into the game in debug mode, and locate the state ID where you would like to make the capital)

Step 1: Inside of the GreatTenYear\common\countries folder, create a new .txt file named after the country you want to make (EX: 'Sontisian_Empire'). You can copy an
already existed file, and then rename it, inside the file you can designate the graphical culture of this nation, along with it's color on the map in RGB format. There is also a 'colors.txt'
file that you will need to add your new country to so the color works on the map.
EX:
NEH = {
	color = rgb { 255 109 36 }
	color_ui = rgb { 255 109 36 }
}

Step 2: Inside of the GreatTenYear\common\country_tags folder, open the 02_countries.txt file. Inside this file is a list of the country tags currently in the game,
simply go to a new line and create a tag similar to what already exists there (EX: 'SOE = countries/Sontisian_Empire.txt'). Make sure your tag is 3 letters and fully
uppercase, along with it not being taken by any other nation.

Step 3a: (This one is important and can be tricky) Next head into GreatTenYear\history\countries, where there will be multiple files with all the countries in the game (along with some that aren't). The easiest way to continue is by copying an existing file, and then renaming it and starting from there, the naming scheme should be similar to the rest (EX: 'SOE - Sontisian Empire'). Inside of your newly named country file (assuming you copy and pasted an existing one) you will find a whole load of information, for our purposes here we just want to make 1 new country, so there's no need to edit a good amount of it until you want to further develop the nation.

Step 3b: Within the new file, change the capital(usually at the first line of the file) to the state ID that you found at step 0, if you haven't found this yet, go
do so and come back to this file. Next, scroll down until you see 'set_politics', change that to whatever ideology your country should be ruled by, (neutrality, 
fascism, communism, democracy). You can also change if there are elections or not. Next head to 'set_popularities', the only requirement here is that all the values
should add up to 100. After you canged those first two, you can change the ones of the same name in the 1939 start date(will be removed eventually).

Step 3c: IF you want a specific character to rule your country, follow this step, if not continue on. Go to the GreatTenYear\common\characters folder and create a new .txt file with your country's new tag. You can copy an existing file and rename it as well. Create your new character inside that file taking note of the name (refer to the CREATING CHARACTERS section above for further detail). Once thats complete, go back into GreatTenYear\history\countries and find your new country again. Right after 'set_technology' towards the top, do 'recruit_character = character_name' of course replacing the last part with the specific name of the character that you made in the characters file.

Step 4: Next head into the GreatTenYear\history\states folder, and locate the state ID that you want to make the capital of your new country. Once you find it
(using the file search function is easiest), go to the 'history =' section of the file, and change the 'owner' and 'add_core_of' to your new country's tag. You can
also edit the buildings on this specific state if you'd like, along with it's resources, but that is not required.

Step 5: Now to get our country to show up on the map, we must set its name, head to GreatTenYear\localisation\english, and locate the countries_l_english file. This can be edited easily using free programs like Notepad++ or Visual Studio Code. In this file you'll find a list of country tags, their ideologies and the names of
those countries. Each ideology needs 3 entries, one for the name on the map, its def, and the adjective of the country. 
(EX: 
SOE_neutrality:0 "Sontisian Empire"
SOE_neutrality_DEF:0 "Sontisian Empire"
SOE_neutrality_ADJ:0 "Sontisian" )
You can copy and paste an existing list of country names and edit them with your new country's information, make sure to get their tag correct, the other names are only used if the country becomes that ideology, so if you don't plan on having them change ideologies soon, you can leave them as whatever you'd like for now.

Step 6: Lastly we need to create the flag for our new country (Refer to the GFX, PORTRAITS and FLAGS section), head to GreatTenYear\gfx\flags, where you will find
many files with country tags as their name. For basic implementation, you will need 3 files of different sizes, large(82x52), medium(41x26) and small(10x7). Create
these new flags, and make sure each is saved as a .tga file in their respective size folder, large going into the flags folder itself, with medium and small in their 
own folders.

Step 7: Profit. Your country should be on the map in game now! If not, make sure the tag is correct in every step, and your files don't have any characters it can't
read like spaces (EX: Sontisian Empire.txt won't work, Sontisian_Empire.txt will work). Now you can add more states to your country in the same manner as finding
it's capital, take note of all the state IDs that your country should take up, and edit those in the state folder with the new owner.
