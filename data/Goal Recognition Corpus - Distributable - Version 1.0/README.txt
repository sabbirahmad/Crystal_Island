README.txt

Crystal Island: Outbreak 
Goal Recognition Corpus

Date: 29 October, 2014
Version: 1.0

North Carolina State University
Department of Computer Science

Disclaimer: All records in the attached dataset were obtained from human subjects who used the Crystal Island game-based learning environment. Research activities involving data from human subjects require approval by an Institutional Review Board (IRB). This is true even in cases where the human subject data has been anonymized, as is the case with this dataset. While North Carolina State University has received permission to distribute this dataset, any research conducted by an outside organization is subject to their own IRB procedures.


INTRODUCTION
------------

This dataset consists of student interaction logs from Crystal Island: Outbreak, a game-based learning environment for middle school microbiology. Crystal Island: Outbreak was developed by students and staff in North Carolina State University's Department of Computer Science. The game is built on Valve Software's Source engine, the 3D game platform for the popular Half-Life 2 series of games. The enclosed dataset was used in goal modeling work described in the following article.

Eun Young Ha, Jonathan Rowe, Bradford Mott, and James Lester. Goal Recognition with Markov Logic Networks for Player-Adaptive Games. In Proceedings of the Seventh International Conference on Artificial Intelligence and Interactive Digital Entertainment, Palo Alto, California, pp. 32-39, 2011. 

We sincerely hope that others find this corpus useful, and write original research publications about models trained/tested on the data. However, we ask that you please cite the above article in any publication that directly references/utilizes/discusses the corpus. Data in this corpus was collected during a human-subject study in Fall 2009. Participants were 8th grade students from a suburban public middle school. The study's design and procedure is described in the following article.

Jonathan Rowe, Lucy Shores, Bradford Mott, and James Lester. Integrating Learning, Problem Solving, and Engagement in Narrative-Centered Learning Environments. International Journal of Artificial Intelligence in Education, 21(1-2), 115-133, 2011.


To watch a video that showcases many of Crystal Island: Outbreak's features, see the following URL.

https://vimeo.com/110378867

Included in this package are screenshots of several of the key features of Crystal Island. These are included to aid in understanding the game environment and associated interaction dataset.

We thank you for your interest in the Crystal Island goal recognition corpus. Please direct any questions or requests to Jonathan Rowe - jprowe@ncsu.edu 




CORPUS OVERVIEW
---------------

The corpus consists of 175 log files. Each filename begins with a prefix in the following format: SessionX-StationY. These prefixes are unique player identifiers; Session1-StationA is a distinct player from Session1-StationAA, who is distinct from Session3-StationC. 

In some cases, a single player will have multiple log files, as indicated by a suffix _1, _2, _3, etc. Students possess multiple log files if their software was restarted (e.g., software crashes, computer battery issues) during the study. In this version of Crystal Island, student progress was not saved across restarts. Therefore, players began the game from the narrative's beginning any time they required a restart. It should be noted that in our original goal recognition work (Ha, Rowe, Mott, & Lester, 2011), we did not treat initial logs and post-restart logs differently. 

The files' content is stored in pipe-separated format. Each row in a file is an instance of a player action or game event. The instances are drawn from several categories:


MOVE - Indicates a player's transition between two locations in Crystal Island's virtual environment. The virtual environment is divided into 39 discrete locations. It should be noted that a single room within a building may be a single location, or divided into multiple locations (e.g., dininghall-front and dininghall-back-souptable). Similarly, the outdoor camp is divided into multiple locations. From the player's perspective, boundaries between discrete locations are invisible; the virtual environment appears to be one continuous physical space.

DIALOG - Indicates a turn of conversational dialogue between the player and a non-player character (NPC). A turn can consist of a question asked by the player (via dialogue menu), or a spoken response by the NPC.

QUIZ - Indicates a quiz exchange presented through the in-game smartphone. Includes instances of player responses to quizzes, as well as feedback messages about the correctness of the player's response.

PDAUSE - Indicates user interaction with the in-game smartphone (aka PDA). This could correspond to manipulating the virtual phone's mainscreen, viewing a text-based "field manual" app about the game's microbiology curriculum, responding to a virtual message from an NPC, or viewing a text-based note that the player previously wrote.

PICKUP - Indicates picking up an object, such as a piece of food, crate, medicine bottle, or cactus.

DROP - Indicates dropping an object.

OPEN - Indicates opening a door to a building, or the refrigerator in the dining hall.

WORKSHEET - Indicates an interaction with the diagnosis worksheet. There are two types of logged WORKSHEET events. One logged event occurs when a player updates a single dropdown option in their diagnosis worksheet. Another logged event occurs when a player closes the diagnosis worksheet, which results in a logged dump of the entire worksheet's state.

TALK - Indicates initiating a conversation with an NPC. This occurs when the player approaches an NPC and left-clicks. Instances immediately following a TALK event are DIALOG events, i.e. the locutionary acts in the conversation. 

TESTCOMPUTER - Indicates an interaction with the testing equipment (i.e., food scanner) in the camp laboratory. Players can specify what type of lab test they wish to run (e.g., test an object for pathogenic contaminants), as well as the reason for their lab test (e.g., because the sick NPCs ate this type of food). Players are initially allocated five lab tests. If they exhaust their supply of lab tests, they can earn more by answering microbiology-themed questions presented through the in-game smartphone. Note: the object being tested is *not* recorded in this instance type.

LABELING - Indicates an interaction with the cell labeling activity in the laboratory.

TESTOBJECT - Indicates the result of a lab test (e.g., the milk tested positive for pathogenic contaminants). Always preceded by a TESTCOMPUTER instance. Also indicates which object was tested (unlike TESTCOMPUTER instances).

RETRIEVEITEM - Indicates retrieving an object from the player's backpack (i.e., a single-item inventory). The backpack enables the player to hold an item while keep her "hands" free to open and close doors while navigating in the environment.

STOWITEM - Indicates stowing an object in the player's backpack.

GOALCOMPLETE - Indicates a problem-solving goal has been completed. There are seven goals explicitly logged in the game. The seven goals were identified collaboratively by the project's computer science and education teams during the early design of the game. The goals involve holding conversations with key NPCs, successfully testing the disease's transmission source in the laboratory, and solving the mystery. While other actions in the game could be designated as additional "goals", all of our goal recognition work to date has focused on this original seven.

BOOKREAD - Indicates reading a virtual book about microbiology concepts.

CLOSE - Indicates closing a door to a building, or the refrigerator in the dining hall.

SOLUTION - Indicates which disease (Influenza or Salmonellosis) has been randomly selected as the mystery's solution at the onset of gameplay. 






FORMAT OF CORPUS DATA
----------------------

In this section, we describe specific details about the log data's format, broken down by category. 

Different categories of player actions/game events store different types of data in each column and row. In other words, the data within each row and column is heterogeneous, both in terms of data type (e.g., integer, float, string) as well as role. The reasons for this heterogeneity are in part practical, and in part historical, but they require that the pipe-separated attributes of each instance be interpreted on a case-by-case basis. We summarize the formats for each category below.



MOVE | <timestamp> | <previous action - deprecated> | <current action - deprecated> | <previous location> | <current location>------DIALOG | <timestamp> | <dialog menu subtype> | <timestamp for menu opening> | <timestamp for player clicking menu option> | <duration between menu open and player click> | <menu option chosen> | <text in menu option>or

DIALOG | <timestamp> | <dialog menu subtype> | <npc name> | <text of npc utterance>------QUIZ | <timestamp> | <quiz subtype> | <timestamp for receiving/opening question> | <timestamp for closing/answering question> | <duration between receiving and answering question> | <attempt # on question> | <was student response correct/incorrect> | <student response>or 

QUIZ | <timestamp> | <quiz subtype> | <timestamp for receiving answer/feedback msg> | <timestamp for closing answer msg> | <duration between receiving and closing feedback msg>------PDAUSE | <timestamp> | <smartphone screen viewed> | <button press type> | <timestamp for opening this smartphone screen> | <timestamp for closing this smartphone screen> | duration between opening and closing smartphone screen>------PICKUP | <timestamp> | <previous action - deprecated> | <current action - deprecated> | <previous location> | <current location> ------DROP | <timestamp> | <previous action - deprecated> | <current action - deprecated> | <previous location> | <current location>------OPEN | <timestamp> | <previous action - deprecated> | <current action - deprecated> | <previous location> | <current location>------WORKSHEET | <timestamp> | <worksheet section> | <worksheet field> | <entry in field>

or 

WORKSHEET | <timestamp> | <close worksheet subtype> | <timestamp for opening worksheet> | <timestamp for closing worksheet> | <duration between opening and closing> | <final diagnosis section prefix> | <final-entry 1> | <final-entry 2> | <final-entry 3> | <final-entry 4> | <symptom section prefix> | <symptom-entry 1> | <symptom-entry 2> | <symptom-entry 3> | <symptom-entry 4> | <tested objects section prefix> | <tested-object-entry 1> | <tested-object-entry 2> | <tested-object-entry 3> | <tested-object-entry 4> | <object contaminants section prefix> | <object-contaminants-entry 1> | <object-contaminants-entry 2> | <object-contaminants-entry 3> | <object-contaminants-entry 4> | <hypothesis topic section prefix> | <hypothesis-topic-entry 1> | <hypothesis-topic-entry 2> | <hypothesis-topic-entry 3> | <hypothesis match section prefix> | <hypothesis-match-entry 1> | hypothesis-match-entry 2> | <hypothesis-match-entry 3> | <hypothesis explanation section prefix> | <hypothesis-explanation-entry 1> | <hypothesis-explanation-entry 2> | <hypothesis-explanation-entry 3>------TALK | <timestamp> | <previous action - deprecated> | <current action - deprecated> | <previous location> | <current location>------TESTCOMPUTER | <timestamp> | <test computer subtype> | <hypothesis about transmission source> | <justification for lab test> | <timestamp for opening lab test computer> | <timestamp for closing computer / running test> | <duration between opening test computer and running test> | <number of remaining lab tests available>------LABELING | <timestamp> | <lesson (practice) activity> | <timestamp for opening labeling activity> | <timestamp for submitting labels> | <duration between opening and submitting labels> | <entry 1> | <entry 2> | <entry 3> | <entry 4> | <entry 5> | <entry 6> | <is correctly labeled?>

or 

LABELING | <timestamp> | <slide (actual) activity> | <timestamp for opening labeling activity> | <timestamp for submitting labels> | <duration between opening and submitting labels> | <entry 1> | <entry 2> | <entry 3> | <is correctly labeled?>------TESTOBJECT | <timestamp> | <tested object> | <test result>

or

TESTOBJECT | <timestamp> | <testing error message>------RETRIEVEITEM | <timestamp> | <duration object held in backpack> | <object retrieved>------STOWITEM | <timestamp> | <object being stowed>------GOALCOMPLETE | <timestamp> | <goal completed> | <timestamp for prior goal> | <duration of time between this goal and prior goal>------NOTES | <timestamp> | <note interface subtype> ------BOOKREAD | <timestamp> | <book file name> | <timestamp for opening book> | <timestamp for closing book> | <duration of viewing open book>------CLOSE | <timestamp> | <previous action - deprecated> | <current action - deprecated> | <previous location> | <current location>------SOLUTION | <disease afflicting team>

------