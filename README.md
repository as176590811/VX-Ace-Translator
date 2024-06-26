# Description
Efficient translator for RPG Maker VX Ace games, fully written in Ruby, that can decompile/compile all text-related .rvdata2 files to a readable text files and vice-versa.

If you love the project, any support from you will help to keep the project alive, you can support me on Paypal from here: https://paypal.me/AhmedAhmedEG?country.x=EG&locale.x=en_US

# Features
- Automatic decryption for rgss3a files if no "Data" folder is found in the game's directory.
- Full support for modifying scripts, from adding, removing and even positionaly inserting them.
- Infinite depth serialization and deserialization of all parameter types in common events.
- User-friendly textual representation of all parameter types in common events.
- Fast decompling/compiling speed.
- Highly organized output format and file structure.
- Filtering to specifically target file(s) for decompiling/compiling.
- Full support for all event command types.
- Two modes for decompiling/compiling of event commands: indexless and indexing modes.
- Small file output size, consists of text files and Ruby scripts only.
- Error handling for out-of-bound pages, common events, and event commands, including indentation.
- Beautiful and informative terminal outputs.

# How to Use
Call the VXAceTranslator.exe file with the following arguments:-

```Decompiler Usage: VXAceTranslator.exe -d "GAME_DIR" -o "OUTPUT_DIR" [Optional]```

```Compiler Usage: VXAceTranslator.exe -c "GAME_DIR" -i "INPUT_DIR" [Optional] -o "OUTPUT_DIR" [Optional]```

Optional Arguments:
- -t TARGET_FILENAME: Specifies a target filename to decompile/compile specific files. Only files with the given target filename included in their base name will be processed.
- --force-decrypt: Forces the translator to decrypt the game and extract raw data files, even if the game is already decrypted.
- --switch-indexless: Enables indexing mode (Explained below).

> **_NOTE:_** It is crucial to consistently enclose paths within double quotes when entering them in a terminal, as not doing so can lead to misleading errors if the path contains any spaces.

# Examples
Example 1 - Decompiling/Compiling all supported rvdata2 files.:-

```Decompiling: VXAceTranslator.exe -d "path/to/game"```
  
```Compiling: VXAceTranslator.exe -c "path/to/game"```<br/><br/>

Example 2 - Decompiling/Compiling rvdata2 files that start with the word "Map" in their name.:-

```Decompiling: VXAceTranslator.exe -d "path/to/game" -t Map```
  
```Compiling: VXAceTranslator.exe -c "path/to/game" -t Map```<br/><br/>

Example 3 - Decompiling/Compiling Map001.rvdata2 file only.:-

```Decompiling: VXAceTranslator.exe -d "path/to/game" -t Map001```
  
```Compiling: VXAceTranslator.exe -c "path/to/game" -t Map001```

# How to Correctly Insert Scripts
Incase you want to insert new scripts without having to manually renumber all the scripts following it, there's a featured special syntax that makes it easy to achive this, normally a script will be named in this format:-

`Index - ScriptName.rb`

To insert a new script after a spacific script, you have to rename your new script to be like this:-

`index+1 - NewScriptName.rb`

This will insert the new scrip after that `Index` by 1, you can surly use any other numbers other than 1 to place it even further.

# Indexless vs Indexing Mode
Those are modes specify how to read and write event commands in CommonEvents.rvdata2, Maps.rvdata2 and Troops.rvdata2.

In indexless mode, event commands are compiled from the ground up based on what's written by the user, in the order the user written them in, any removed event commands will be discarded in compilation, this gives more freedom, but can destroy future compatibility in case the game got an update.

In indexing mode, event commands are written proceeded by it's index in the list of it's corresponding common event, original event commands in the game's files will be patched by the new values, which the user written in it's corresponding index, this applies for the event type and parameters too, removing any event command or changing it's order will have no effect in the game, gives less freedom, but assures future compatibility, it supports adding new event commands with simple syntax.

# How to Add Event Commands in Indexing Mode
The decompiler format for event comments in indexing mode is as follows:-

`Index-CommandEventName([Parameters])`

To manually add an event command, you have write them in the same way, but at the end of the line, you will add a plus sign, like this:-

`Index-CommandEventName([Parameters])+`

Surly the indentation level you will add behind the event command will be accounted for.
This will make the compiler insert that command in the index you have written, also you don't have to account for the future indexes of the event commands that follows the one you are adding, this will be automatically handled by the compiler.

# How to Build
1- Make sure you have Ruby v2.7.8, any version higher than that have a different format for marshaled files, and it's not compatible with the engine.

2- Make sure RubyGems is not installed at all, as it causes crashes with executables generated by Ocra library, a version of Ocra ripped from the official gem is included in the project.

3- Simply run Build.rb and done.

> **_NOTE:_** As the newest version of RubyGems causes crashes with executables generated by Ocra library, and the source code in the official Ocra GitHub is outdated, and the updated working code is available only in the gem version of Ocra, I installed Ocra gem, copied Ocra folder from RubyGems directory, reinstalled Ruby, and used the copied Ocra library manually, and it worked perfectly.
