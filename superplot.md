MIKE PORTUESI
128 SOUTH CHRISTIINE
MOUNT CLEMENS, MI 48043
(313) 469-8176
DATE OF SUBMISSION 03/01/83

Computer Type: Atari 400/800
Memory Requirement: 24K
Requires BASIC ROM, Joystick

# Superplot

Recently I purchased a copy of COMPUTE! 's Second Book of Atari.
Buried among the many treasures in the book was
an article called "Plotting Made Easy".  The program that
accompanied the article allowed you to draw on the screen
and have the computer write a series of PLOT-DRAWTO statements
for use in another program. The program worked
as advertised, but it was not without need of improvements.
The cursor was simply a plotted pixel and erased everything
it went over. In addition, the program did not allow you to
create a picture with more than one color. I incorporated
these and other improvements into Superplot.

## Requirements for Superplot

The program as it is now requires at least 24K of
memory and a joystick to use. Most of the memory used is
devoted to the display. 4K of memory is reserved at the
very top of memory for player-missile graphics. About 3K of
this is not used, because the memory for the graphics 7
display would interfere with the player-missile memory.
Finding an alternate place to put the player-missile area
(try directly below the display) would free those bytes,
and with some cutting you may get it to run in 16K. One
thing you might want to do to save memory is to have the
program self-delete all the initialization code after it is
finished running. This includes not only everything before
line 280, but also the SETPM and INITML routines.  However,
keep in mind that the program requires more memory as it
runs.  The program adds statements to itself to save your
picture, so the more complex a picture is, the more memory
it will require to save.

## How to use Superplot

When you first type Superplot in, it is a very good idea
to make a few backup copies.  Not only is this program
self-modifying, but the computer could also lock up if you
fail to type in the machine language data correctly. When
you RUN the program, there will be a short pause as it
initializes. Following this, you will be asked a series of
questions dealing with color and luminance for the cursor, `
background, and each of the color registers. Enter the
standard Atari color and luminance values for each of these
prompts (the same values used in the SETCOLOR statement).
Once the questions are over, the program sets up its
display and you're in business.

### The Indicator Line

You should notice a set of indicators on the bottom of
the display. The first two indicators (from left to right)
are 'X=' and 'Y='. These tell the current location of the
cursor. The coordinates you see there are the same as the
X,Y values of the PLOT statement, and they point to the
center blank spot of the cursor. The next indicator, 'C=',
tells you what color you're drawing in.  Note that this
inidicator is the same value as the Atari COLOR statement,
and _not_ a color register number.  The differences between
the two are shown in the chart below. The next indicator,
'LAST=', tells you the last thing you did on the display,
whether it was plotting a point or drawing a line. If you
just plotted a point on the display, the indicator will
read 'P'. If you just drew a line it will read 'D'. The
last indicator is 'M'. This informs you of the amount of
free memory your system has left (in bytes).  This serves as
a warning in case you're running out of memory.  There are
also four color bars under the text window.  These will be
discussed after we meet the cursor.

### The Cursor

On the display in the upper left hand corner is a small
cross. This is the cursor.  If you don't see it, or you only
see part of it, use the joystick to move it into view. To
plot a point, move the cursor to the desired spot and press
the fire button.  To draw a line, move the cursor to the
endpoint of your intended line and press the fire button
again. The computer will draw a line to connect these two.
To plot a single point, simply press the fire button twice.
This actually PLOTs and DRAWTOs a line to the same spot,
but when the program writes the BASIC subroutine it will
show up as only one PLOT statement.  If you want to connect
lines, make the endpoint of the first the beginning of the
second by pushing the fire button again after you draw the
first line.  For example, if you want to draw a square,
follow these steps:

1. Move the cursor to the first corner of the square and
press the fire button.
2. Move the cursor to the second corner and press the fire button twice. This draws the first side of the square
and plots the beginning of the second.
3. Move the cursor to the third corner and press the
fire button twice.
4. Continue this process until the square is completed.

When the program writes the BASIC subroutine, the
instructions for the square will come out as one PLOT
statement and a series of DRAWTOs.

### The Color Bars

The color bars are used to change the color you wish to
draw with. To change the drawing color, simply move the
cursor over the appropriate bar and push the fire button.
The next line you draw will be in the color selected. Note
that the blank space in the middle of the cursor must be
over the color bar to make the change.  The color register
numbers, 'C=' numbers, COLOR values, and the color bars are
related as follows:

|Color     | "C="      | COLOR     | Color Bar  |
|Register  | Indicator | Statement | on display |
|Number    | Number    | Argument  | ( L - R )  |
|----------|-----------|-----------|------------|
| 4        | 0         | 0         | FIRST      |
| 0        | 1         | 1         | SECOND     |
| 1        | 2         | 2         | THIRD      |
| 2        | 3         | 3         | LAST       |

The program will take these changes into account when
the BASIC subroutine is written, and will add COLOR
statements at the appropriate places.

### The Console Keys

Each of the yellow console keys performs a different
function. These are as follows:

#### OPTION

When you press this key the program will ask
for an output device. Enter 'C:' to save your BASIC
subroutine to cassette, 'D:filename.ext' to save your
routine to disk, or 'P:' to list your routine out to the
printer. This program saves the routine in LIST format. To
enter it back in, use the ENTER command. If you saved it on
disk, use 'ENTER "D:filename.ext"' to retrieve it from
disk, and if you saved it to cassette use 'ENTER "C:"'.
After the program saves your routine, it will ask if you
want to clear it out in memory. Answering 'Y' to this
prompt will result in the computer deleting all the lines
it has added to the program. It will then return you back
to graphics mode 7 with a clean display, ready for a new
picture. If you do not wish to save your subroutine, but
simply want to get rid of it, push the RETURN key in
response to the 'Enter output device?' prompt. It will then
ask if you want to clear out the lines.

#### SELECT

This key is used to change the colors in each
color register. The computer will ask for the color register
number, (see the chart above to pick the right one), the
Atari color value, and the luminance of that color.  It will
then change the color in that register.

#### START

Pressing this key will cause the computer to
add statements to the program. All the lines you have drawn
will automatically be converted to PLOT-DRAWTO
statements and stored with line numbers beginning at 20000
and continuing upwards by increments of ten. If you do not
press this key, the program will automatically update
itself after every 20 lines you draw on the screen. Note
that this option will not work if you have just plotted a
point on the display.  You must have just completed drawing
a line for this option to work.

### The Space Bar

If you make a mistake drawing a line, hit the space bar.
The program will delete the last line you drew on the
display. Each time you hit the space bar, the computer will
erase the previous line drawn. You can erase as many lines
as you wish this way. There are a few restrictions on its
use, however. The first is that you cannot delete a line
whose coordinates have already been made part of the
program. If you want to do this, just edit the finished
subroutine. The second limitation is that the program uses
the background color to erase the offending line from the
display. In doing this, it may inadvertently erase parts of
other lines as well. This will not affect operation of the
program in any way, and when the program modifies itself it
will restore the erased parts as it redraws the display.
Like the START key, this option will not work if you have
just plotted a point. If you plotted a point in the wrong
spot, finish the line before using the space bar. The last
thing to note about this option is the way it handles the
current drawing color. As an example, suppose you changed
the drawing color from one to two, and you drew a line. If
you erased the line, the program would not only delete the
line, it would also reset your drawing color back to 1.
Keep this in mind as you use this option.

## How Superplot Works

Superplot uses a few nifty tricks to accomplish its
various tasks. The program itself is actually a collection
of subroutines driven by a main loop running from lines 280
to 410. This loop reads the joystick, moves the cursor,
updates the indicator line, and checks the console switches
and space bar. The program uses James E. Korenthal's
Assembler Joystick Driver (_COMPUTE!_ No. 14, pg. 126) to
read the joystick and assign delta x and y values. The
cursor is Player 0. It is moved vertically using string
manipulations. This technique involves fooling BASIC into
thinking that the memory space allocated for a string is
smack in the middle of player/missile memory. By
manipulating the string, you move the player vertically
much faster than BASIC can move it any other way short of
machine language.  If you would like a more detailed
explanation, see the "Outpost: Atari" column in the April
1981 _Creative Computing_, page 194.

The text window is one of the trickiest parts of the
program. In order to keep it from changing all sorts of
unsightly colors, two display list interrupts are used,
each with a separate routine all its own. The first routine
before the text window stores the standard Atari default
blue into the CTIA or GTIA (whatever your machine has)
hardware color registers. Then it sets up the 6502 for the
second interrupt routine directly after the text window by
storing its address into the display list interrupt vector
at locations 512 and 513 decimal. The second routine
restores the colors by reading them from the operating
system shadow registers. This keeps the text window blue
while the color of the bars remains unchanged.  After doing
this, it sets the machine up for the first routine again.
The program shuts off the interrupts when either modifying
the program or saving lines.  The color bars are actually
one line of graphics mode 3. The program POKEs the data for
the bars in at the appropriate spot in display memory.

Most of the subroutines within the program are pretty
straightforward. Each one states what it does in the
remarks before the routine itself.  However, a few bear
closer examination. Some of the more interesting ones are:

#### CHNGCOL (Lines 1000 to 1060)

This routine does all
of the color changes using the color bars at the bottom of
the display. It is also one of the simplest parts of the
program.  All it does is take the X coordinate of the cursor,
divide it by 40, and take the result for the COLOR value.
Simple, isn't it?


#### MODPROG (Lines 6000 to 6160)

This routine is the
one that adds statements to the program. The very first
thing it does is shut off the interrupts and P/M graphics.
Then it goes to graphics 0, prints the new program lines on
the screen, and adds them to the program rising the forced
read mode.  Then it restores the graphics display and
continues.  When the program adds statements to itself,
BASICs' internal pointers to the string and array area are
changed. The program recalculates the offset to the P/M
memory and resets the pointers in the variable table. Then
it reinitializes the arrays holding X,Y coordinates and
exits. For more information on how the forced read mode is
used to update the program, see "Using the Atari Forced
Read Mode" by Frank C. Jones in _COMPUTE's Second Book of Atari_, pg. 26.

#### SETDIS (Lines 8000 to 8120)

This routine has been
pretty much explained earlier.  First, it sets up the
indicators in the text window. Then it modifies the last
few bytes of the display list to allow for the display list
interrupts and the color bar line. Next, it figures the
appropriate spot in memory and POKEs in the data for the
color bars. Then it turns on the interrupts and exits.

#### SETPM (Lines 9000 to 9170)
This routine initializes
Player/Missile graphics. Lines 9020 and 9030 figure the
addresses of the Variable Name Table and Array Table
pointers respectively.  Line 9040 informs ANTIC of the
location of P/M memory, and 9050 through 9090 relocate the
string MEM$ right on top of the memory for player 0. Line
9095 clears out MEM$, and 9110 though 9140 read in the
data for the cursor.

## Improvements to the Program

Like its predecessor, Superplot still has room for
improvements. No program is so good that it can't be
improved, and mine is no exception. Tailoring the program
to do what you want is fairly easy, owing to the way the
program is designed. Modifying the program involves
changing a subroutine.  If you really don't like something
about a section of the program, you might even want to
replace the offending subroutine. New features can be added
in the same fashion.

