csgo-retakes
=============

[![Build Status](https://travis-ci.org/splewis/csgo-retakes.svg)](https://travis-ci.org/splewis/csgo-retakes)

This is a CS:GO [Sourcemod](sourcemod.net) plugin that creates a competitive-minded gamemode called retakes. The idea is that the T players spawn in a bombsite with the bomb, while the CT spawn on rotation routes and try to retake the site and defuse the bomb.

**Note that this plugin is currently unreleased. There is no download unless you want to compile it yourself. Expect bugs.**

## For plugin developers

My goal is to keep the base retakes plugin as simple as possible. See [retakes.inc](scripting/include/retakes.inc) for how to extend the plugin.

Here are some examples of what could be done using those natives:
- different weapon allocation policies (by default, everyone gets an AK/M4, armor/helmet, and a kit)
- change how players get put into teams by changing their "round points" or the team ratios, or by changing who is in the waiting queue if the game is full
- change how the bombsite is chosen each round (by default one is randomly picked each round)

## Download
Stable releases are in the [GitHub Releases](https://github.com/splewis/csgo-retakes/releases) section.

There is no stable release yet.

## Installation

#### Requirements

**Only Sourcemod 1.7 is supported.** Releases are compiled using the 1.7 compiler and will not work on a server using an older version.

#### Instructions
Download the archive and extract the files to the game server. From the download, you should have installed the following (to the ``csgo`` directory):
- ``addons/sourcemod/plugins/retakes.smx``
- ``addons/sourcemod/translations``
- ``cfg/sourcemod/retakes``

#### Configuration
The file ``cfg/sourcemod/retakes/retakes.cfg`` will be autogenerated when the plugin is first run and you can tweak it if you wish.

You may also tweak the values in ``cfg/sourcemod/retakes/retakes_game.cfg``, which is executed by the plugin each map start.

Here are a few important cvars that are in ``cfg/sourcemod/retakes/retakes.cfg``:
- ``sm_retakes_maxplayers``: maximum number of players allowed in the game at once
- ``sm_retakes_ratio_constant``: what percentage of players go on the T team

## Building
The build process is managed by my [smbuilder](https://github.com/splewis/sm-builder) project. You can still compile retakes.sp without it in the normal fashion, however.

To compile, you will need:
- [SMLib](https://github.com/bcserv/smlib)

You should make sure you have a relatively recent version of smlib - some changes were made to accommodate sourcemod 1.7 changes.

## Creating and Editing Spawns

Here is how to operate the spawn editor:
- use ``sm_edit`` to launch into edit mode, this makes more spawn-editing commands avaliable (you shouldn't do this on a live, public server). Example: ``!edit`` in chat on a map whose spawns you want to edit
- use ``sm_new`` to create a new spawn. Example: ``!new ct a`` in chat will create a new CT spawn for bombsite A where you are standing.
- use ``sm_show`` to show the spawns for a site. Example: ``!show a`` in chat will show all spawns for bombsite A.
- use ``sm_deletespawn`` to delete the nearest spawn. Example: ``!deletespawn`` in chat.
- use ``sm_bomb`` to toggle whether to display all spawns or potential bomb-carrier spawns. Example: ``!bomb`` in chat
- use ``sm_nobomb`` to mark a spawn as unavailable to a bomb carrier. (by default, all spawns within the xy plane of a bombsite are available for a bomb carrier). Example: ``!nobomb`` in chat while standing on top of the spawn you want to edit.

## Contribution and Suggestions
First, check the [issue tracker](https://github.com/splewis/csgo-multi-1v1/issues?state=open) to ask questions or make a suggestion.
If you have a suggestion you can mark it as an enhancement.

Guidelines
- Create a fork on github, clone that, then create a branch to work on ``git checkout -b mybranchname``
- Follow the code-style already used as much as you can
- Submit a pull request when you're happy with the new feature/enhancement/bugfix
- Favor readability and correctness over all else
- For a moderately advanced feature, it may be simpler to write it as a plugin that uses the retakes natives from [retakes.inc](scripting/include/retakes.inc)
- **Keep it simple, stupid**
