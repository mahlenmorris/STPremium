# Twixt, a CV signal controller module for VCV Rack

Twixt is a signal generator for VCV Rack.

Twixt is useful for exploring the sonic spaces between desired sonic points (the Squares). It also has unique randomization capabilities (with undo and redo) using the companion module [Mixt](#mixt) that make it delightful for sonic exploration. 

# Twixt
Twixt is a 2D graphical signal generator consisting of up to sixteen visible Squares,
each with 12 output values, and a visible Point chosen by mouse or CV.
Where the Point is in relation to the Squares (and their values) determines the 12 CV outputs.

Twixt's "making values between known sets of values" UI is inspired by Metasurface part of [AudioMulch](http://www.audiomulch.com/), a desktop music studio.

![Twixt Overview](images/TwixtHeadline.png)

# Quick Start
If you just want a quick taste of what Twixt does:
* Take an existing patch of yours.
* Add a Twixt module.
* Randomize it with the menu.
* Attach some of the outputs to various CV control points in your patch (if they have attenuverters, make sure they aren't at zero).
* Start dragging the mouse around the surface.
* Try different values for the TWIXT knob.

### Videos
Short videos: [teaser](https://youtu.be/XVvhzCE7Hsk?si=nbeVQ3aMhPy6dM-O), [slightly more informative](https://youtu.be/WoRrLPeSNlc?si=_K4vIA7JKqTKTFfQ), [short](https://www.youtube.com/shorts/FhxLgaAo-Xw). Note that none of these feature the current design.

### Uses
* **Access the sounds between other sounds.** When you have two or more distinct sonic qualities you want to explore for the same section of a patch (e.g., making the lead melody "clean" vs. "drenched in chorus and reverb" vs. "overdriven"):
* * Make each of those a Square.
* * Attach the outputs to the inputs of the modules that control those qualities.
* * Move the Point on top of each of the squares.
* * * Type in the name of Square.
* * * Adjust the output values that create that quality.
* * Pick a TWIXT value (e.g., Bilinear Squared), and drag the point around with the mouse to hear the sounds between the ones you created.

* **Graphically control the mix.**
* **Explore changing many properties of a patch at once.**

## Controls

### The Square Surface
The large black are in the center of Twixt is where the Squares and the Point reside.

#### Squares
Each Square has a number from 1 - 16. They can also have names, edited with the NAME edit field on the right side.

The Squares are created, resized, moved, and deleted with keystrokes. These are all centered
around the WASD keys familiar to anyone who has played games on a computer.
![Twixt Keyboard editing hints](images/TwixtKeyboard.png)
**You can show this help within Twixt by clicking the EDIT HELP button.**

These edits affect
whichever Square is currently **selected**; the currently selected Square is shown in slightly thicker lines, and its corresponding number is shown in a small white window to the left of the Surface (just above the NAME).

* Make new Squares:
* * **F** - create a brand new Square centered on where the mouse cursor is currently hovering over the surface. That new Square will now be the selected Square. All of its values will be zero.
* * **R** - copies the selected Square and places the copy centered on where the mouse cursor is currently hovering over the surface. If the original Square had a NAME, (e.g., "Spacey") then the new Square will have a similar name (e.g., "Copy of Spacey").
* Changing or moving the selected Square:
* * **W/A/S/D** - move the selected Square around the space.
* * **Q** - shrink the selected Square. Some settings of TWIXT take into account the relative sizes of the Squares when computing the values of the outputs.
* * **E** - enlarge the selected Square.
* Changing which Square is selected:
* * Right-clicking the mouse pointer on the Surface will make the nearest Square be the selected square.
* * **C/Z** or **TAB/SHIFT-TAB** - cycles through the Squares, selecting each in turn. **C** and **TAB** move to the next higher numbered Square, **Z** and **SHIFT-TAB** move to lower numbers, and both gestures wrap around from the last Square to the first.
* Remove Squares:
* * **X** - deletes the selected Square.

##### Square Names
Each Square can have a user-created name, which is shown underneath the Square's number. This can, for example, make it easier to see at a glance which Square corresponds to which sound quality. When a Square is selected, the current name for it is shown to the left of the Square Surface in an editable text window (NAME). Editing text there immediately updates the text seen on the display.

A couple of notes:
* While editing names, use **TAB** and **SHIFT-TAB** to rotate through the Squares.
* If the name of a Square is getting wider than you like, you can separate the name into multiple lines by typing a newline/Enter in the name.

#### EDIT HELP
Clicking this button will replace the colorful graphical display of the Surface and show the keyboard help.

### The Point
The Point is a small circle in the Surface that controls the signals sent by each of the twelve CV outputs along the right edge. The position of Point is a pair of X and Y voltages, where X = -5, Y = -5 is at the lower left corner and X = 5, Y = 5 is
at the upper right corner.

There are menu options on Twixt to change either or both of the X and Y axis from the [-5, 5] range to [0, 10].

![X and Y controls](images/TwixtXY.png)

The Point's position can be set (and moved) in a number of ways:
* Clicking or dragging on the surface will move the Point to that position.
* On the left side of Twixt, there are a number of controls to move Point: 
* * Inputs at the top for setting X and Y. If these are not set, then the last position set by clicking on the surface will be used.
* * Below that, inputs with attenuverters are added to the values from the inputs (or last clicked position). Note that, somewhat unusually, the attenuverters range from -200% to 200%.
* * And below that are outputs of the current position of Point. Note that you can use these to chain together multiple Twixt modules with the same movement; just connect the X & Y outputs of the first Twixt to the X & Y inputs of the second.
* Note that X and Y are independent of each other, meaning that you can, for example, use the inputs above to control the X position of Point, but control the Y solely by your mouse clicks on the Surface.

#### Movement Files
To make Point movements easier to create, Twixt includes some .WAV files that can be played with many VCV Rack sample players (including my own [Memory System](https://github.com/mahlenmorris/VCVRack/blob/main/Memory.md)). They are written to the folder **plugins-[your OS]\StochasticTelegraphTwixt\twixt-waves** underneath your Rack2 user folder. Play one in Memory and use the left and right outputs as signals to X and Y.

![Playing a .WAV file to move Point](images/TwixtMover.png)

They currently include movement in a circle, a square, and a triangle. Playing these files slower, faster, reversed, amplified, and combining/mixing multiple playback heads or files can create interesting movements.

### TWIXT
There are currently five different methods Twixt can use to determine what values the Outputs have when not directly atop a Square. This knob determines which is to be used.
They are:
* **Bilinear Squared**
* **Bilinear Cubic**
* **Venetian Secret**
* **Tactical Map**
* **Nearest Square**
These methods are in order from most gradual changes in value to least. In Nearest Square, the Outputs are just set to the values of the closest Square. This can be handy if you want to quickly change from one square's setting to another without having to be terribly careful in your mouse clicking.

### Outputs
On the 

### Menu Options
#### Randomize
The Randomize menu option found on every module will, in Twixt, also replace any existing Squares with a random set of new ones. The Squares will also have randomly generated names and MATH1 formulas.
#### Show Keyboard Commands
As noted above, when set (the default), this will show the larger version of the editing keyboard commands. Unsetting it will replace it with a small icon.
#### Only Compute MATH1 for a Square when inside it
Defaults to true. By default, the value of MATH1 is zero for a particular Square when Point is not in the Square. This is to reduce the CPU load. If, however, the value of MATH1 is important for a Square even when Point is not in it, then unset this menu option.
#### Point position X ranges from 0-10 instead of -5 - 5
When set, the X input will be expected from 0-10, and the X output will fall into that range as well.
#### Point position Y ranges from 0-10 instead of -5 - 5
When set, the Y input will be expected from 0-10, and the Y output will fall into that range as well.
#### MATH Cheat Sheet
Just shows a brief reminder of all the functions and variable names Twixt will recognize.

### Bypass Behavior
If this module is bypassed, then all output values will be 0.0V. However, you can continue to
edit the Surface, adding and changing Squares as you wish.

![Line Break image](images/Separator.png)

# Mixt
[TODO] Complete this.


# Acknowledgements

Thanks foremost to @paradiddle16 on the VCV Rack Community board for mentioning
AudioMulch's Metasurface. Twixt is my attempt to bring that interaction to Rack. 

Many thanks to [Marc Weidenbaum](https://disquiet.com/) for his
encouragement and enthusiasm for my module-making efforts.

And my deepest gratitude to Diane LeVan, for letting me ignore her and/or
the world for periods of time just to craft these things. I apologize for
waking up with new ideas at 5AM, and for having a retirement hobby that
is nearly impossible to even *start* describing to any of our friends.
