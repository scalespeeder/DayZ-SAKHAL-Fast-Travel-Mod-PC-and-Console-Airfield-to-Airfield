1.26 DayZ Sakhal Plane Airfield Fast Travel Teleport Mod For PC & Console, Changelog & Terms Of Use

Limited Testing on PC Local Server & Xbox Remote Server Version 1.26 OCT 2024.

Thanks to @King_Alobar_& JinieJ for the idea!

Created by @scalespeeder. Please report bugs & errors to scalespeeder@gmail.com with screenshots.

TERMS OF USE
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS
OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN
AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH
THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Using these modded xml & json files could break the functioning of your DAYZ server, requiring a reinstall that would wipe
all player progress.

Using these modded xml & json  files neccessitates increased regular restarts to prevent server crashing.

It is suggested you thoroughly test your server after applying these files to ensure proper
functioning of your server.

DESCRIPTION OF WHAT THE MOD DOES

These files & code snippets create a simple fast-travel system on your DayZ Sakhal Community Server, between makeshift & the main airfields on Sakhal. (See supplied image).
Players simply have to enter the delapidated aircraft, log off the server, log back on & they will be transported to the next airfield.

There is an optional NPC pilot who will stand next to the planes.

Please note that if the server is full & a log-on queue is in effect, the player will be at the back of that queue.

INSTRUCTIONS

Download these files from my Github or Mega. On github click on the green "Code" button & "download zip". On Mega click on the green "download" button & "download as a zip file".
Save the files in their own folder somewhere easily accesible on your PC.

-----

Stop your server.

-----

Ensure your DayZ Server has activated the cfggameplay.json. For console users on Nitrado Servers, go to "General Settings" on your server and tick "Enable cfggameplay.json" & save.

On PC Servers add or edit the following line to your serverDZ.cfg:

enableCfgGameplayFile = 1;

(On some PC servers, including Nitrado, the serverDZ.cfg is "hidden", so you need to enable "expert mode" in settings,
then go to "expert settings", which is the serverDZ.cfg. Stop the server before making changes this way.)

-----

On console, go to your Nitrado dashboard, then to your server, then to the file-browser, then to the "custom" folder inside the mission folder, and upload "fast-travel-1-nw-coast-to-se-coast.json" "fast-travel-2-se-coast-to-main-af.json"
"fast-travel-3-main-af-to-w-penin.json" "fast-travel-4-w-penin-to-se-island.json" "fast-travel-5-se-island-to-sw-island.json" "fast-travel-6-sw-island-to-nw-coast.json" & "sakhal-planefast-travel-objects.json"

On PC, create a custom folder inside your mission file, (eg mpmissions\dayzOffline.sakhal\custom )then repeat the above uploads.

The "sakhal-planefast-travel-objects.json" file adds the planes to the airfields.

The 3 "fast-travel" json files tell the server where the fast travel points are, and where the player should teleport to.

-----

Next, open your cfggameplay.json file and after

"wetnessWeightModifiers": [1.0, 1.0, 1.33, 1.66, 2.0] add a comma to the end, so it looks like this:

"wetnessWeightModifiers": [1.0, 1.0, 1.33, 1.66, 2.0],

then paste in this line:

"playerRestrictedAreaFiles": ["pra/warheadstorage.json","custom/fast-travel-1-nw-coast-to-se-coast.json","custom/fast-travel-2-se-coast-to-main-af.json","custom/fast-travel-3-main-af-to-w-penin.json","custom/fast-travel-4-w-penin-to-se-island.json","custom/fast-travel-5-se-island-to-sw-island.json","custom/fast-travel-6-sw-island-to-nw-coast.json"]

The section should now look something like this:

"WorldsData":
	{
		"lightingConfig": 0,
		"objectSpawnersArr": ["custom/cherno-plane-fast-travel-objects.json"],
		"environmentMinTemps": [-3, -2, 0, 4, 9, 14, 18, 17, 13, 11, 9, 0],
		"environmentMaxTemps": [3, 5, 7, 14, 19, 24, 26, 25, 18, 14, 10, 5],
		"wetnessWeightModifiers": [1.0, 1.0, 1.33, 1.66, 2.0],
		"playerRestrictedAreaFiles": ["pra/warheadstorage.json", "custom/fast-travel-1-nw-coast-to-se-coast.json","custom/fast-travel-2-se-coast-to-main-af.json","custom/fast-travel-3-main-af-to-w-penin.json","custom/fast-travel-4-w-penin-to-se-island.json","custom/fast-travel-5-se-island-to-sw-island.json","custom/fast-travel-6-sw-island-to-nw-coast.json"]
	},

We are actually taking advantage of the code designed for the Sakhal Military Bunker, which on Sakhal is used to make sure you don't get stuck in
the bunker if the doors close - the server teleports you to a safe location when you log off & on. We can use this to create our fast travel system.

-----

Next in the cfggameplay.json file look for the "objectSpawnersArr" line.

Edit it to look like this to spawn in the planes:

	"objectSpawnersArr": ["custom/sakhal-planefast-travel-objects.json"],
	
If you already refer to some custom object spawner files, it should look something like this:

	"objectSpawnersArr": ["custom/sakhal-planefast-travel-objects.json","custom/some-other-file-name.json"],
	
-----

If you'd like to make the logging off & on process faster for your players, open your globals.xml file, find the login / logoff timers and edit them
to look like this:

 <var name="TimeLogin" type="0" value="5"/>
 <var name="TimeLogout" type="0" value="5"/>
 
remember to save and re-upload if you need to.
 
-----

If you don't want the NPC pilot standing by the planes, you could now simply restart your server and the fast travel system would be in place.

-----

To add the NPC pilots,

add the following code to your types.xml file, near the top, after <types>

<!--pilot npc-->
 
 <type name="SurvivorM_Mirek>
        <nominal>0</nominal>
        <lifetime>3600</lifetime>
        <restock>0</restock>
        <min>1</min>
        <quantmin>-1</quantmin>
        <quantmax>-1</quantmax>
        <cost>100</cost>
        <flags count_in_cargo="0" count_in_hoarder="0" count_in_map="1" count_in_player="0" crafted="0" deloot="0"/>
    </type>
	
<!-- end of pilot npc-->

remember to save and re-upload if you need to.

-----

add the following code to your cfgspawnabletypes.xml file, near the top, after <spawnabletypes>

<!--pilot npc clothes -->

<type name="SurvivorM_Mirek">
    <attachments>
        <item name="ZSh3PilotHelmet" />
    </attachments>
      <attachments>
        <item name="BomberJacket_Black" />
    </attachments>
    <attachments>
        <item name="Jeans_Blue" />
    </attachments>
    <attachments>
        <item name="MilitaryBoots_Black" />
    </attachments>
</type>

<!-- end of pilot npc clothes -->

remember to save and re-upload if you need to.

-----

add the following code to your cfgeventspawns.xml file, near the top, after <eventposdef>

<!-- pilot NPC spawns-->
		
		<event name="ItemNPC1">
        <pos x="7515.427734375" z="13264.4560546875" a="0" /> <!--NW Coast Makeshift AF NPC-->        
		</event>
		<event name="ItemNPC2">
		<pos x="13700.421875" z="7921.4580078125" a="0" /> <!--SE Coast Makeshift AF NPC-->  
		</event>
		<event name="ItemNPC3">
		<pos x="7223.31982421875" z="6992.1201171875" a="0" /> <!-- Main Airfield NPC -->
		</event>
		<event name="ItemNPC4">
		<pos x="982.7946166992188" z="7394.05078125" a="0" /> <!-- W of Military Peninsula Makeshift AF NPC  -->
		</event>
		<event name="ItemNPC5">
		<pos x="11966.7998046875" z="2169.159912109375" a="0" /> <!-- Far SE Island Makeshift AF NPC  -->
		</event>
		<event name="ItemNPC6">
		<pos x="2258.268798828125" z="3436.818359375" a="0" /> <!-- SW Island Makeshift AF NPC  -->
		</event>
		
<!-- end of pilot NPC spawns-->

remember to save and re-upload if you need to.

-----

add the following code to your events.xml file, near the top, after <events>

<!--pilot npc events -->

<event name="ItemNPC1"> <!--NW Coast Makeshift AF NPC-->  
    <nominal>1</nominal>
    <min>1</min>
    <max>1</max>
    <lifetime>2500</lifetime>
    <restock>0</restock>
    <saferadius>0</saferadius>
    <distanceradius>0</distanceradius>
    <cleanupradius>200</cleanupradius>
    <flags deletable="0" init_random="0" remove_damaged="1"/>
    <position>fixed</position>
    <limit>child</limit>
    <active>1</active>
    <children>
        <child lootmax="0" lootmin="0" max="1" min="1" type="SurvivorM_Mirek"/>
    </children>
</event>

<event name="ItemNPC2"> <!--SE Coast Makeshift AF NPC-->  
    <nominal>1</nominal>
    <min>1</min>
    <max>1</max>
    <lifetime>2500</lifetime>
    <restock>0</restock>
    <saferadius>0</saferadius>
    <distanceradius>0</distanceradius>
    <cleanupradius>200</cleanupradius>
    <flags deletable="0" init_random="0" remove_damaged="1"/>
    <position>fixed</position>
    <limit>child</limit>
    <active>1</active>
    <children>
        <child lootmax="0" lootmin="0" max="1" min="1" type="SurvivorM_Mirek"/>
    </children>
</event>

<event name="ItemNPC3"> <!-- Main Airfield NPC -->
    <nominal>1</nominal>
    <min>1</min>
    <max>1</max>
    <lifetime>2500</lifetime>
    <restock>0</restock>
    <saferadius>0</saferadius>
    <distanceradius>0</distanceradius>
    <cleanupradius>200</cleanupradius>
    <flags deletable="0" init_random="0" remove_damaged="1"/>
    <position>fixed</position>
    <limit>child</limit>
    <active>1</active>
    <children>
        <child lootmax="0" lootmin="0" max="1" min="1" type="SurvivorM_Mirek"/>
    </children>
</event>

<event name="ItemNPC4"> <!-- W of Military Peninsula Makeshift AF NPC  -->
    <nominal>1</nominal>
    <min>1</min>
    <max>1</max>
    <lifetime>2500</lifetime>
    <restock>0</restock>
    <saferadius>0</saferadius>
    <distanceradius>0</distanceradius>
    <cleanupradius>200</cleanupradius>
    <flags deletable="0" init_random="0" remove_damaged="1"/>
    <position>fixed</position>
    <limit>child</limit>
    <active>1</active>
    <children>
        <child lootmax="0" lootmin="0" max="1" min="1" type="SurvivorM_Mirek"/>
    </children>
</event>

<event name="ItemNPC5"> <!-- Far SE Island Makeshift AF NPC  -->
    <nominal>1</nominal>
    <min>1</min>
    <max>1</max>
    <lifetime>2500</lifetime>
    <restock>0</restock>
    <saferadius>0</saferadius>
    <distanceradius>0</distanceradius>
    <cleanupradius>200</cleanupradius>
    <flags deletable="0" init_random="0" remove_damaged="1"/>
    <position>fixed</position>
    <limit>child</limit>
    <active>1</active>
    <children>
        <child lootmax="0" lootmin="0" max="1" min="1" type="SurvivorM_Mirek"/>
    </children>
</event>

<event name="ItemNPC6"> <!-- SW Island Makeshift AF NPC  -->
    <nominal>1</nominal>
    <min>1</min>
    <max>1</max>
    <lifetime>2500</lifetime>
    <restock>0</restock>
    <saferadius>0</saferadius>
    <distanceradius>0</distanceradius>
    <cleanupradius>200</cleanupradius>
    <flags deletable="0" init_random="0" remove_damaged="1"/>
    <position>fixed</position>
    <limit>child</limit>
    <active>1</active>
    <children>
        <child lootmax="0" lootmin="0" max="1" min="1" type="SurvivorM_Mirek"/>
    </children>
</event>

<!--end of pilot npc events -->

remember to save and re-upload if you need to.

-----

Now you can just re-start your server and the fast-travel system will be in place. Enjoy!

Thanks, Rob.
