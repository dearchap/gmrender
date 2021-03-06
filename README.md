I needed a small headless UPnP media renderer for Linux (for small footprint-use
in a Raspberry Pi or CuBox), but there does not seem to be much small stuff
around.

Found: GMediaRender http://gmrender.nongnu.org/
but it was incomplete, several basic features missing and the project seems to
have been abandoned some time ago.

So this is a fork of those sources to resurrect this renderer and add the
missing features. (Original sources at
http://cvs.savannah.gnu.org/viewvc/gmrender/?root=gmrender )

I consider this fork GMediaRender 0.0.7 (license to trill).

Added so far
  * Support to get duration and position of current stream. This allows
    controllers to show a progress bar.
  * Support basic commands (Only `Play` and `Stop` were working before)
     - `Pause`  : Pause current stream.
     - `Seek`   : Seek to a particular position.
  * When current track is finished, transition to state `STOPPED`
    so that the controller sends us the next song (Actively eventing).
  * Support gapless (via SetNextAVTransportURI to play gapless). Looks like
    the next version of BubbleUPnP will send the right action to support it.
  * Volume/Mute control.

TBD
  * go into TRANSITIONING while seeking.

Tested the following control points: BubbleUPnP, 2Player, DK Player, eezUPnP;
Please report what other control-points worked for you - and which didn't.

Needed
------

There are reports, that the sound output is flaky in recent versions of
Raspbian Wheezy on Raspberry Pi, probably due to pulseaudio, missing gbus or
gbus-session or something -- I don't know since I don't have a Raspberry Pi
(yet).
So if someone gets it to work properly, please send me an init-script for other
people to try.
And of course, debian packages for Raspberry Pi would be probably the best.

You can reach me via <h.zeller@acm.org>.
