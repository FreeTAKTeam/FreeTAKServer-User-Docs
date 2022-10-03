# About Mil-STD-2525 and COTS
The original 'NATO symbol'  are expressed as a set of Military Symbols for Land Based Systems. The COT system is only partially overlapping with 2525. on a list of 3000+ COTS , 1000 are directly traceble to mil 2525.



|**Pos**|**Type**|**Value**|
| :- | :- | :- |
|1|en: Coding scheme|<p>S - Warfighting<br>I - Intelligence<br>O - Stability Operations<br>E – Emergency Management<br>WO – Weather</p><p>G – Tactical Group</p>|
|2|en: Affiliation|P - Pending<br>U - Unknown<br>A - Assumed Friend<br>F - Friend<br>N - Neutral<br>S - Suspect<br>H - Hostile<br>G - Exercise Pending<br>W - Exercise Unknown<br>D - Exercise Friend<br>L - Exercise Neutral<br>M - Exercise Assumed Friend<br>J - Joker<br>K - Faker<br>O - None Specified|
|3|en: Battle Dimension|**If** ***Coding scheme*** **is S or I:**<br>P - Space<br>A - Air<br>G - Ground<br>S - Sea Surface<br>U - Sea Subsurface<br>SF - Special Operations Forces<br><br>**If** ***Coding scheme*** **is O:**<br>V - Violent Activities<br>L - Locations<br>O – Operations<br>I - Items<br>P - Individual<br>G - Nonmilitary Group or Organization<br>R – Rape<br><br>**If** ***Coding scheme*** **is E:**<br>I - Incident<br>N - Natural Events<br>O - Operations<br>F - Infrastructure|
|4|en: Status|A - Anticipated/Planned<br>P - Present<br>C - Present/Fully Capable<br>D - Present/Damaged<br>X - Present/Destroyed<br>F - Present/Full to Capacity|
|5-10|en: Function ID|<p>Any number of char before the first “dash”, it express also the hierarchy</p><p>(Hundreds of options)</p>|
|11|en: Symbol Modifier 1|<p>A - Headquarters<br>B - Task Force HQ<br>C - Feint Dummy HQ<br>D - Feint Dummy/Task Force HQ<br>E - Task Force<br>F - Feint Dummy<br>G - Feint Dummy/Task Force<br>H – Installation</p><p>M - Mobility<br>N - Towed Array</p>|
|12|en: Symbol Modifier 2|A - Team/Crew<br>B - Squad<br>C - Section<br>D - Platoon/Detachment<br>E - Company/Battery/Troop<br>F - Battalion/Squadron<br>G - Regiment/Group<br>H - Brigade<br>I - Division<br>J - Corps/Mef<br>K - Army<br>L - Army Group/Front<br>M - Region<br>N – Command<br><br>**If** ***Symbol Modifier 1*** **is M:**<br>O - Wheeled/Limited<br>P - Wheeled<br>Q - Tracked<br>R - Wheeled and Tracked<br>S - Towed<br>T - Rail<br>U - Over the Snow<br>V - Sled<br>W - Pack Animals<br>Y - Barge<br>Z – Amphibious<br><br>**If** ***Symbol Modifier 1*** **is N:**<br>S - Towed Array (Short)<br>L - Towed Array (Long)|

## Example 2525

Equipment Manufacture is part of ‘WAR.GRDTRK.INS.EQTMNF’ code is

S\*G\*IE----H\*\*\*\*
![image](https://user-images.githubusercontent.com/60719165/193574795-14a3dfce-ff51-457b-a4bc-e6196cdef2fe.png)


|S|\*|G|\*|IE|H|||||||
| :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- | :- |
|War|Affiliation|Ground|Battle Dimension|Function ID|installation|||||||

Test code [here:](https://www.spatialillusions.com/milsymbol/example.html#angular)

## Example COT

Equipment manufacture	Building is part of Gnd/Structure/Factory

|**Atom**|** **|**Affiliation**|** **|** Ground **|** **|** Infrastrucure **|** **|** Equipment **|	
| :- | :- | :- | :- | :- | :- | :- | :- | :- |
|a|-|.|-|G|-|I|-|E|	

