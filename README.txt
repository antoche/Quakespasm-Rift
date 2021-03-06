  QuakeSpasm

  ____________________________________________________________

  Table of Contents


  1. About
  2. Downloads
  3. Hints
     3.1 Music Playback

  4. Compiling
     4.1 Linux/Unix
     4.2 Windows
     4.3 Mac OS X

  5. Known Bugs
  6. Changes
     6.1 Changes in 0.85.9
     6.2 Changes in 0.85.8
     6.3 Changes in 0.85.7
     6.4 Changes in 0.85.6
     6.5 Changes in 0.85.5
     6.6 Changes in 0.85.4
     6.7 Changes in 0.85.3
     6.8 Changes in 0.85.2
     6.9 Changes in 0.85.1

  7. Todo
  8. Copyright
  9. Links


  ______________________________________________________________________


  Page last edited Apr. 12, 2013


  1.  About

  QuakeSpasm is a Quake 1 engine based on the SDL port of FitzQuake.  It
  includes 64bit CPU support, a new sound driver, several networking
  fixes and a few graphical niceities.

  <http://quakespasm.sourceforge.net>


  2.  Downloads

  o  <http://quakespasm.sourceforge.net/download.htm>


  3.  Hints

  Visit the FitzQuake Homepage <http://www.celephais.net/fitzquake> for
  a full run-down of the engine's commands and variables.


  o  To disable some changes, use "quakespasm -fitz"

  o  For different sound drivers use "SDL_AUDIODRIVER=DRIVER
     ./quakespasm" , where DRIVER may be alsa, dsp, pulse, esd ...

  o  Shift+Escape draws the Console.

  o  From the console, use UP to browse the command line history and TAB
     to autocomplete command and map names.

  o  There is currently no CD Music volume support. cd_sdl.c needs
     replacing with cd_linux.c, cd_bsd.c etc..

  o  In windows, alternative CD drives are accessible by "quakespasm
     -cddev F" (for example)

  o  Quakespasm allows loading new games (mods) on the fly with "game
     GAMENAME"


  3.1.  Music Playback

  Since version 0.85.4, Quakespasm can play back external MP3, OGG and
  Wave music files.

  o  Tracks should be named like "track02.ogg", "track03.ogg" ... (there
     is no track01) and placed into "Quake/id1/music".

  o  Unix users may need some extra libraries installed: "libmad" or
     "libmpg123" for MP3, and "libogg" and "libvorbis" for OGG.

  o  To prevent tracks from being downsampled, use the "-sndspeed"
     option to set a sufficiently high sample rate.

  o  Use the "-noextmusic" option to disable this feature.

  o  See  <README.music> for more details.


  4.  Compiling

  To check-out the latest version of QuakeSpasm, use :
  svn co svn://svn.code.sf.net/p/quakespasm/code/trunk/quakespasm

  4.1.  Linux/Unix

  After extracting the source tarball, browse the Makefile and edit the
  music streaming options, then

  ______________________________________________________________________
  make
  cp quakespasm /usr/local/games/quake (for example)
  ______________________________________________________________________

  Compile time options include

  o  make DEBUG=1 for debugging

  o  make SDL_CONFIG=/PATH/TO/SDL-CONFIG for unusual SDL installations

  Streaming music playback requires "libmad" or "libmpg123" for MP3, and
  "libogg" and "libvorbis" for OGG files.

  HOME directory support can be enabled via Misc/homedir_0.patch

  The project can also be built with Codeblocks (project files
  included).

  4.2.  Windows

  The QuakeSpasm developers cross-compile windows binaries using MinGW
  <http://www.mingw.org> and Mingw-w64 <http://mingw-w64.sf.net>.

  The project can also be built using Visual Studio 2005 (or newer).

  4.3.  Mac OS X

  A Quakespasm App (including program launcher and update framework) can
  be made using the Xcode template found in the MacOSX directory.

  Alternatively, have a look at Makefile.darwin for more instructions on
  building from a console.


  5.  Known Bugs

  Some versions of Xorg and SDL have brightness issues. If you have Xorg
  >= 7.5 and broken brightness, these patched libSDL binaries may help.

  o  Gamma patched libSDL (i686-linux)
     <http://sourceforge.net/projects/quakespasm/files/Support%20Files/libSDL_gamma_patched.tgz/download>

  o  Gamma patched libSDL (x86_64-linux)
     <http://sourceforge.net/projects/quakespasm/files/Support%20Files/libSDL_gamma_patched-
     AMD64.tgz/download>


  6.  Changes

  6.1.  Changes in 0.85.9

  o  Fixes for several undefined behaviors in C code (gcc-4.8 support.)

  o  Implemented Hor+ style field of view (FOV) scaling, useful for
     widescreen resolutions. Configured by new cvar fov_adapt: set it
     to 1 and your fov will be scaled automatically according to the
     resolution. Enabled by default.

  o  Adjusted string buffers for PR_ValueString and friends to fix
     crashes with excessively long global strings seen in some rude
     mods.

  o  Toned down warning messages from PF_VarString() a bit.

  o  Fixed Fitzquake's map existence check in changelevel (used to leak
     file handles which would end up in a Sys_Error() due to consuming
     all free handles if many maps reside not in pak files.)

  o  Fixes/cleanups in chat mode handling. Client no longer gets stuck
     in chat mode upon disconnect.

  o  Mouse grab/key_dest fixes and key cleanups.

  o  The "speedkey" now acts as "slowkey" when "always run" is on.

  o  Support for demo recording after connection to server. (thanks to
     Baker for a patch)

  o  Corner case fixes in COM_Parse() for quoted strings and support for
     C-style /*..*/ comments.

  o  Changed lightmaps to GL_RGBA instead of GL_RGB.

  o  Better parse for opengl extensions list (from quakeforge.)

  o  Vsync saving/loading fixes.

  o  Fixed pointfile loading.

  o  Multiple cleanups in gl_vidsdl.c.

  o  Opus music decoding support (as an optional patch only.)

  o  Several other minor fixes/cleanups.


  6.2.  Changes in 0.85.8

  o  Made Quake shareware 1.00 and 1.01 versions to be recognized
     properly.

  o  Fixed control-character handling in unicode mode. Keyboard input
     tweaks.

  o  Made the keypad keys to send separate key events in game mode.

  o  Text pasting support from OS clipboard to console. (windows and
     macosx.)

  o  Support for the Apple (Command) key on macosx.

  o  Fixed increased (more than 32) dynamic lights.

  o  Music playback: Made sure that the file's channels count is
     supported.

  o  Support for Solaris.

  o  Switched to using libmad instead of libmpg123 for MP3 playback on
     Mac OS X.

  o  Better support for building the Mac OS X version using a makefile,
     support for cross-compiling on Linux.

  o  Fixed a minor intermissions glitch.

  o  Increased string buffer size from 256 to 384 for PF_VarString to
     work around broken mods such as UQC.

  o  Restored original behavior for Quake registered version detection.

  o  Minor demo recording/playback tweaks.

  o  Minor tweaks to the scale menu option.

  o  unbindall before loading stored bindings (configurable by new cvar
     cfg_unbindall, enabled by default.)

  o  New icon.

  o  Miscellaneous source code cleanups.


  6.3.  Changes in 0.85.7

  o  Added support for cross-level demo playback

  o  gl_texturemode is reimplemented as a cvar with a callback and the
     setting is automatically saved to the config

  o  Fixed execution of external files without a newline at the end

  o  Reduced memory usage during reloading of textures

  o  Fixed compilation on GNU/kFreeBSD (Debian bug #657793)

  o  Fixed backspace key on Mac OS X

  o  Disable mouse acceleration in Mac OS X

  o  Worked around recursive calling of the anisotropic filter callback

  o  Console word wrap and long input line fixes

  o  Verified correct compilation by clang (using v3.0)

  o  Several other small changes mostly invisible to the end-user


  6.4.  Changes in 0.85.6

  o  More work for string buffer safety

  o  Reverted v0.85.5 change of not allowing deathmatch and coop cvars
     to be set at the same time (was reported for possibility of causing
     compatibility issues with mods)

  o  Several cleanups/changes in the cvar layer

  o  Minor SDL video fixes.


  6.5.  Changes in 0.85.5

  o  SDL input driver updated adding native keymap and dead key support
     to the console

  o  Fixed a crash in net play in maps with extended limits

  o  Verified successful compilation using gcc-4.6.x

  o  Added workaround against GL texture flicker (z fighting),
     controlled by new cvar 'gl_zfix'

  o  Read video variables early so that a vid_restart isn't necessary
     after init

  o  mlook and lookspring fixes

  o  Added support for loading external entity files, controlled by new
     cvar 'external_ents'

  o  Made mp3 playback to allocate system memory instead of zone

  o  Some updates to the progs interpreter code

  o  Fixed r_nolerp_list parsing code of fitzquake

  o  Made sure that deathmatch and coop are not set at the same time

  o  Several code updates from uHexen2 project, several code cleanups.


  6.6.  Changes in 0.85.4

  o  Implement music (OGG, MP3, WAV) playback

  o  A better fix for the infamous SV_TouchLinks problem, no more hard
     lockups with maps such as "whiteroom"

  o  Add support for mouse buttons 4 and 5

  o  Fix the "unalias" console command

  o  Restore the "screen size" menu item

  o  Fixed an erroneous protocol check in the server code

  o  Raised the default zone memory size to 384 kb

  o  Raised the default max_edicts from 1024 to 2048

  o  Revised lit file loading, the lit file must be from the same game
     directory as the map itself or from a searchpath with a higher
     priority

  o  Fixed rest of the compiler warnings

  o  Other minor sound and cdaudio updates


  6.7.  Changes in 0.85.3

  o  Fix the "-dedicated" option (thanks Oz) and add platform specific
     networking code (default) rather than SDL_net

  o  Much needed OSX framework stuff from Kristian

  o  Add a persistent history feature (thanks Baker)

  o  Add a slider for scr_sbaralpha, which now defaults to 0.95
     (slightly transparent, allowing for a nicer status bar)

  o  Allow player messages longer than 32 characters

  o  Sockaddr fix for FreeBSD/OSX/etc networking

  o  Connect status bar size to the scale slider

  o  Include an ISNAN (is not-a-number) fix to catch the occassional
     quake C bug giving traceline problems

  o  Enumerate options menus

  o  Add a "prev weapon" menu item (from Sander)

  o  Small fix to Sound Block/Unblock on win32

  o  Lots of code fixes (some from uhexen2)

  o  Sys_Error calls Host_Shutdown

  o  Added MS Visual Studio support

  o  Add a "-cd" option to let the CD Player work in dedicated mode, and
     some other CD tweaks.


  6.8.  Changes in 0.85.2

  o  Replace the old "Screen size" slider with a "Scale" slider

  o  Don't constantly open and close condebug log

  o  Heap of C clean-ups

  o  Fix mapname sorting

  o  Alias the "mods" command to "games"

  o  Block/Unblock sound upon focus loss/gain

  o  NAT fix (networking protocol fix)

  o  SDLNet_ResolveHost bug-fix allowing connection to ports other than
     26000

  o  Bumped array size of sv_main.c::localmodels from 5 to 6 fixing an
     old fitzquake-0.85 bug which used to cause segfaults depending on
     the compiler.

  o  Accept commandline options like "+connect ip:port"

  o  Add OSX Makefile (tested?)


  6.9.  Changes in 0.85.1

  o  64 bit CPU support

  o  Restructured SDL sound driver

  o  Custom conback

  o  Tweaked the command line completion and added a map/changelevel
     autocompletion function

  o  Alt+Enter toggles fullscreen

  o  Disable Draw_BeginDisc which causes core dumps when called
     excessively

  o  Show helpful info on start-up

  o  Include real map name (sv.name) and skill in the status bar

  o  Remove confirm quit dialog

  o  Don't spam the console with PackFile seek requests

  o  Default to window mode

  o  Withdraw console when playing demos

  o  Don't play demos on program init

  o  Default Heapsize is 64meg

  o  Changes to default console alpha, speed

  o  Changes to cvar persistence gl_flashblend (default 0), r_shadow,
     r_wateralpha, r_dynamic, r_novis


  7.  Todo

  o  Add uHexen2's first person camera (and menu item)

  o  Native CD audio support (if desired). cd_sdl.c doesn't have proper
     volume controls

  o  Test usb keyboards.

  o  Complete the unix user directories support


  8.  Copyright

  o  Quake and Quakespasm are released under the GNU GENERAL PUBLIC
     LICENSE Version 2 <http://www.gnu.org/licenses/gpl-2.0.html>

  o  Quakespasm console background image by AAS, released under the
     CREATIVE COMMONS PUBLIC LICENSE
     <http://creativecommons.org/licenses/by/3.0/legalcode>


  9.  Links

  o  QuakeSpasm Homepage <http://quakespasm.sourceforge.net>

  o  QuakeSpasm Project page
     <http://sourceforge.net/projects/quakespasm>

  o  FitzQuake Homepage <http://www.celephais.net/fitzquake>

  o  Sleepwalkr's Original SDL Port
     <http://www.kristianduske.com/fitzquake>

  o  Baker's 0.85 Source Code
     <http://quakeone.com/proquake/src_other/fitzquake_sdl_20090510_src_beta_1.zip>

  o  Func Quakespasm forum
     <http://www.celephais.net/board/view_thread.php?id=60452>

  o  Func SDL Fitzquake forum
     <http://www.celephais.net/board/view_thread.php?id=60172>

  o  Ozkan's email <mailto:gmail - dot - com - username - sezeroz>

  o  Stevenaaus email <mailto:yahoo - dot - com - username - stevenaaus>

  o  Kristian's email <mailto:gmail - dot - com - username - inveigle>


