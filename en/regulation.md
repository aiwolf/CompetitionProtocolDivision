# 4th International AIWolf Competition Protocol Division Regulation

2022/06/06 Ver. 1.2.0-en

## Werewolf game rules for the 4nd International AIWolf Competition

### No-Reveal Game

In this competition, the player's role is not showed upon its death.

### Number and Types of Roles

The games played by the agent will include villages with 15 players and 5 players. Depending on the size of the game, the role distribution is as follows.

| Number of Players | Villagers | Seer | Medium | Bodyguard | Werewolves | Possessed |
|-|-|-|-|-|-|-|
| 15 Players | 8 | 1 | 1 | 1 | 3 | 1 |
| 5 Players | 2 | 1 | 0 | 0 | 1 | 1 |

### Description of the Roles

#### Roles of the Villager Team:

There are four roles aligned with the villager team: Villager, Seer, Medium, and Bodyguard.

- **Villager**: Has no special abilities.
- **Medium**: When a player is eliminated from the game by voting, the Medium is informed of whether that player was a werewolf or a human in the following day. The watcher receives no information if there was not a vote in the previous day.
- **Seer**: At the end of each day (including the first day), the seer can choose one player to “Divine.” The seer will be informed whether this player is a werewolf or a human. If the seer’s target has already been eliminated in the past, the seer will receive no information.
The seer can know the latest elimimated player before deciding the target of divination.
- **Bodyguard**: At the end of each day, the bodyguard can choose one other player to “Guard.” That player is not affected by the werewolves’ attack. 
If the bodyguard chooses the dead as the target of his guard, nothing will happen.
The bodyguard can know the latest elimimated player before deciding who to guard.

#### Roles of the Werewolf Team:

There are two roles aligned with the werewolf team: Werewolf and Possessed.

- **Werewolf**: At the end of each day, the werewolves vote on a human player. The player with the highest number of votes is Attacked. Also, only the werewolves can use the “whisper” channel to exchange information while hidden from human players.
- **Possessed**: The Possessed has no abilities, like the Villager. However, the Possessed wins with the Werewolf team. Seers and Mediums identify the Possessed as human. Also, the possessed can NOT use the "whisper" channel.

### Conversation between agents

#### Turn System

Conversation happens in turns. Each player can broadcast one message at each turn (or choose not to broadcast a message). The order in which the players broadcast within a turn is random, so each player only knows the messages already broadcast up to that point.

A player may broadcast up to 10 messages in one day. This limit does not include "Skip" and "Over" messages. The "talk" phase of a day ends when every player broadcasts "Over," or when every player broadcasts "Skip" three times in a row. Alternatively, the "talk" phase of a day also ends after 20 turns have passed.

#### Conversation on the first day

No conversation takes place on the first day of a game.

#### Werewolf Whisper

The werewolves can use the “whisper” channel after the elimination vote if finished and before the attack vote. Although there is no elimination or attack vote on the first day, the whisper channel can still be used. The werewolf agents can use the first day “whisper” to discuss general strategies such as fake role claims.

If there is only one werewolf in the game, no whisper takes place. Please be careful that the server will not send whisper requests to the agent in this situation (for example, the whisper method in the sample Java agent does not get called).

### Voting and Revoting for Elimination

The vote to eliminate a player from the game happens at the end of the day phase (after the talk phase).
If a player votes for an invalid player, such as a dead player, the vote will be randomly chosen.
Werewolves, Seers, and Bodyguards can use the information of which agent was eliminated by voting when making their decisions during the night phase.

If there is a tie, the vote is repeated one time. In this case, there is no extra conversation. If there is still a tie in the second vote, then the eliminated player is chosen randomly from the tied players. During a revote, all players have a vote, and they can vote in anyone, not just the players tied in the first vote.

### Voting and Revoting for Attack

If there is a tie in werewolf attack vote, one revote is allowed and there is no whisper before the revote.
If there is still a tie in the second vote, then the attacked player is chosen randomly from the tied players.

If a werewolf player votes for an invalid player, such as a dead human, the vote will be invalid.
If the votes of all werewolves are invalid, the target of the attack will be randomly chosen from the alive humans.

## Preliminary Contest and Final Contest

### Game Set

We define a “Game Set” in this competition as 100 games played among the same set of agents. The procedure of a Game Set is as follows:

1. A group of 5 or 15 agents is chosen randomly from the participants.
2. The roles of the players is chosen randomly, and a single game is played.
3. Step 2 is repeated 100 times.

One instance of each agent will be created and used for the entirety of one set. This means that, within one set, each agent will have the same `AgentId`, and can maintain state information between games. Agent instances will be destroyed between sets.

### Agent Update Period and Preparatory Games (Daily Contest):

Participating teams can update their registered agents
between the agent registration and the start of the preliminary contest,
and between the end of the preliminary contest and the start of the final contest.
During the agent update period,
preparatory games (Daily Contest) will be held for the target agents
(all agents before the preliminary contest,
the passed agents after the preliminary contest).
In the preparatory games, each team will play in at least one Game Set,
and only the team of which agent ran without error
can participate in the next preparatory games.
The team disqualified due to an error can rejoin the preparatory games
by registering an improved agent.
It is possible to download the game log of the preparatory games that the team has participated in
and the agent log containing the texts that the agent writes into stdout.
***Please use the preparatory games to verify that your agent works correctly in the server environment, and to improve your agent.***

You can see the Daily Contest Results for [15 player games](http://aiwolf.org/daily15/index.html) and for [5 player games](http://aiwolf.org/daily05/index.html).

### Preliminary Contest:

In the preliminary contest, all participating teams will play at least a minimum number of Game Sets. The 15 teams with highest winning rate will be selected for the Final Contest. To increase the statistical significance of the difference between winning ratios, the number of Game Sets played will be as high as time allows. Participating teams will play an equal number of 5 player Game Sets and 15 player Game Sets.

### Final Contest:

The 15 teams selected from the preliminary contest will participate in the Final Contest. They will play as large a number of Game Sets as time allows, with the roles randomized in each game. The winners will be decided by the winning rate. Finalist teams will play an equal number of 5 player Game Sets and 15 player Game Sets.

## How to submit an agent

### Team Registration:

People who wish to participate in this contest should access the [contest webpage](http://contest.aiwolf.org/) and create a team account in it. Creating a team account counts as the registration.

### Agent Submission

After registering a team, you should upload an agent that is capable of playing all game roles and game set sizes in the “My Page” section of the contest webpage above. The files to be submitted depend on the programming language used:

#### Java Agent

Submit a single “.jar” file. If you are using libraries for machine learning or other things, please include them in your jar file. It will automatically create the necessary classpaths.

Also, include any data files that you may need in the jar archive, and read them from there. For example, if you need to read the file `/data/foo.txt` inside the jar archive, you can use `InputStream is = getClass().getClassLoader().getResourceAsStream(“data.foo.txt”)` to create an input stream that reads your data.

Please be aware that there may be conflicts if you include the following files in your jar file `aiwolf-client.jar`, `aiwolf-server.jar`, `aiwolf-common.jar`, `aiwolf-viewer.jar`, `jsonic-xxxx.jar`. This may cause problems when running your agent. So avoid including files that use these names in your jar file.

The recommended Java version is 17. If you use versions other than that, your agent may not run correctly.

#### C# Agent

A self-contained console application should be submitted (not a dll, as in previous years). Set the runtime to `linux-x64`, and zip the contents of the directory where it was published. Make sure that the executable file is in the root directory of the zip file. There is no restriction on the file name. Indicate the name of the executable file when submitting. Make sure that your program can understand and proccess the following command line parameters:

- `-h hostname`: set the name of the aiwolf server to connect to;
- `-p port`: set the port number to connect to;
- `-n name`: set the name of the agent;

If your agent needs to read any data files, include them in the assembly as resouces, and read them as streams during execution using the method `Assembly.GetManifestResourceStream`.

#### Python Agent

Submit a zip file. In the root directory of your zip file, you should include the main script to be executed (this is different from previous years). There is no restrictions to the file name. Indicate the name of the main script when submitting. Make sure that the main script can understand and proccess the following command line parameters:

- `-h hostname`: set the name of the aiwolf server to connect to;
- `-p port`: set the port number to connect to;
- `-n name`: set the name of the agent;

### Source Code Submission

In addition to the files described above, teams that are selected to the Final Contest must submit the source code of their agents, and a document describing the algorithm used. Even teams that submitted python agent must re-submit their scripts at this stage. The method of submission for the source code and algorithm document will be explained to the finalists after the preliminary contest.

Failing to submit the source code or algorithm document will disqualify a finalist team.

### Open Source License

The source code of the agent will be released as open source software after the competition.
Therefore, please apply an open source license to your source code
that allows free distribution of the source code,
and freedom of copying, modification, and redistribution of the source code.
When you fill out the participation confirmation form,
you will be asked to answer that license.
For reference, the most popular open source licenses in recent years
are Apache License 2.0 and MIT License.
If you are wondering what to choose,
it will be a good idea to choose the MIT License.

The "source code" in this competition refers to
the source code of the agent program written in Java, C\#, Python, etc.
and the setting parameters of the easy-to-use
[AIWolf agent generator](https://aiwolf-generator.herokuapp.com/).

## Forbidden activities

During the competition, the following points are forbidden, and may be cause for disqualification. At the organizer’s sole discretion, we may contact a team to try and solve the problem.

- Runtime error by an agent during a Game Set in the Preliminary or Final Contests.
- Broadcasting a message not allowed by the AIWolf Protocol (A message that cannot be created by the Java ContentBuilder class)
- Writing to files (reading from files is only permitted for: reading files the agent’s jar file, C# Assembly’s resources, or the files included in the python’s zip)
- Connecting to a network (other than the server indicated by the `-h`, `-p` parameters)
- Creating new threads;
- Starting new processes;
- Taking more than 100ms to respond to a request from the server
- Submitting the same agent as another team (“similarity” as judged by the organizers. Both teams will be disqualified)

## About running player programs (Java)

In this section, we explain how to prepare an agent based on the JAVA sample agent. The process is similar for C# and Python. The 4th competition will use [platform version 0.6.x](http://aiwolf.org/en/server). An agent can participate by implementing the `org.aiwolf.common.data.Player` interface defined in the AIWolfCommon.jar.

### Methods that need to be implemented in the Player Interface (Java)

A class inheriting the Player interface needs to implements 11 methods. These methods are divided in the following 4 groups:

- Methods for organizing information: `initialize`, `update`, `dayStart`, `finish`
- Methods for targeted actions: `vote`, `attack`, `guard`, `divine`
- Methods for dialogue: `talk`, `whisper`
- Methods for naming: `getName`

#### Methods for organizing information (initialize, update, dayStart, finish)

These methods are used to process information, and do not need to return anything.

- `initialize(GameInfo, GameSetting)`: This method is called by the server once at the start of the game. The passed arguments are the current state of the game `GameInfo`, as well as the information about the setup of the game (number of players and roles) `GameSetting`.
- `update(GameInfo)`: This method is called before each invocation of all other methods (except initialize). The passed argument `GameInfo` contains the latest information about the game state. When this method is called before finish it will also provide the full list of players and their roles.
- `dayStart()`:  It is called once before each day phase.
- `finish()`: It is called when the game is ended.

#### Methods for targeted actions (vote, attack, guard, divine)

Methods that must return the ID of the agent to be targeted by the action. In the case of Attack, Guard, Divine, these methods will only be called on agents with the respective roles.

- `vote()`: Returns the player to be voted out of the game on that day.
- `attack()`: Only for werewolves. Return the player to be voted for attack on that night.
- `guard()`: Only for the bodyguard. Return the player to be protected on that night.
- `divine()`: Only for the seer. Return the player to be investigated on that night.

#### Methods for communication (talk, whisper)

Methods must return the message to be broadcast in String format. In this contest, only messages following the AIWolf protocol are considered valid (i.e., messages that can be constructed by the `org.aiwolf.client.lib.ContentBuilder` class – see section 5.3)

- `talk()`: Returns a message that will be broadcast for all active players.
- `whisper()`: This method is only called for werewolf players. Returns a message that will be received only by werewolves.

#### Naming Methods (getName)

- `getName():` Returns the name of the player (in String format). The name of the player is displayed on the Game’s log.

### Timing for invoking each method.

The methods described in the previous section (except for `getName()`) are called following the flowchart below. For clarity, the chart does not include the `update()` method, which is called before every other method, with the exception of `initialize()`.

![](images/timing_en.png)

### Valid Broadcast Strings

In this competition, all dialogue among agents must be composed of strings that can be created by the `org.aiwolf.client.lib.ContentBuilder` class. There are 23 kinds of messages, listed below.

- estimate：X believes that Y’s role is Z. (EstimateContentBuilder)
- comingout：X declares that Y’s role is Z.(ComingoutContentBuilder)
- divination：X divines Y. (DivinationContentBuilder)
- divined：X divined Y, and the result was Z (Human or Wolf)(DivinedResultContentBuilder)
- identified：X used the medium power, and identified Y as Z (Human or Wolf)(IdentContentBuilder)
- guard：X protects Y. (GuardCandidateContentBuilder)
- guarded：X protected Y. (GuardedAgentContentBuilder)
- vote：X votes for Y. (VoteContentBuilder)
- voted ：X voted for Y. (VotedContentBuilder)
- attack：X votes for Y to be attacked.（AttackContentBuilder）
- attacked ：X attacked Y. (AttackedContentBuilder)
- agree：X agrees with broadcast T. (AgreeContentBuilder)
- disagree：X disagrees with broadcast T. (DisagreeContentBuilder)
- request：X requests Y to do Z (RequestContentBuilder)
- inquire：X inquires Y  about Z (InquiryContentBuilder)
- because：X states sentence Z because of reason Y (BecauseContentBuilder)
- and：X states A and B and ... (AndContentBuilder)
- or：X states at least one of A or B or ... ( OrContentBuilder)
- xor：X states either A or B (XorContentBuilder)
- not：X negates Y (NotContentBuilder)
- day：X states that Y happened on day T (DayContentBuilder)
- over：I have nothing else to say (if all players broadcast OVER, the Talk Phase ends)(OverContentBuilder)
- skip：I will say nothing now (even if all other players broad cast OVER, the Talk Phase does not end) (SkipContentBuilder)

### About the Player class package

Please create an unique Player class. Avoid just rewriting the sample classes such as `org.aiwolf.sample.player.SampleRoleAssignPlayer`.

Also, please include your Player Class in an independent package. The recommended package naming convention is to use the reverse order of your email's address. (For example, if your e-mail address is contestant@example.com, and your Player class is MyPlayer, the header of your class would probably look like this:

```
package com.example.contestant;
Import org.aiwolf.sample.lib.AbstractRoleAssignPlayer;

public class MyPlayer extends AbstractRoleAssignPlayer {

}
```

In this case, when submitting your source code, you should write the following in the “class path” section:

```
com.example.contestant.MyPlayer
```

## Using other Programming Languages

Besides Java, we accept entries in Python and C#(.NET). When using these languages, please check their respective libraries. Using TCP-IP libraries for socket communication, and making sure that the correct messages are passed back and forth between server and client, it is possible to participate in the game. When in doubt, please contact the organizing committee: gm@googlegroups.com

However, please note that the contest will be executed in a linux machine, so if you do your development in a different environment, make sure that your code is portable. Clients that cannot run on the server environment will be automatically disqualified. To avoid this situation, please test your agent in the preparatory Games. Also, we made available a docker image of the contest server. Please use it to validate your agent.

## Changes

These regulations are subject to change at any time. Changes will be announced at the [project page](http://aiwolf.org/en), the [development mailing list](aiwolfdev@googlegroups.com) and our [Slack Channel](https://aiwolfen.slack.com).

## Change History

2019/02/09 -- ver 1.0.0 -- Translated from the 4th AI Wolf competition  
2019/05/09 -- ver 1.1.0 -- Clarification about the practice contest, clarification about reading from files, other minor changes.  
2020/03/29 -- ver 1.2.0 -- Updated rules for 2020 (non-synchronous broadcast, Java 11)  
2022/05/05 -- ver 2022 1.1.0 -- Updated rules for 2022, to parity with Japanese version 2022 1.1. Folded section 1.5 into 1.2 (removed section 1.5), highlighted parts about the preparatory games, added information about commandline parameters, clarified other sections of the text.  
2022/05/15 -- ver 1.1.1 -- Minor change to C# file explanation: Removed some redundant text  
2022/05/18 -- ver 1.1.2 -- Ported the regulation to Markdown format  
2022/06/06 -- ver 1.2.0-en -- Add description of open source license.
