This folder contains all files required to laser-cut and engrave the plexi plates for the housing.

For the initial built, both 3 and 6 mm plexi material has been used.  

When using another thickness, the length of the srews and bolts should be adapted.

The .cdr-files have been created with CorelDraw, and have been optimized for [Trotec laser and engraving machines](https://www.troteclaser.com/en/). Three different RGB-colors have been used :

color  | RGB-code    | function             | comments
-------|-------------|----------------------|---------
black  | (0,0,0)     | engraving            | 1 pass, basic text and outline
green  | (0,255,0)   | deep engraving       | 5 passes, LED windows
yellow | (255,255,0) | additional engraving | 1 pass, text on LED windows
red    | (255,0,0)   | internal cut-outs    |
blue   | (0,0,255)   | outline cut          |

It is important to perform the jobs in the above order for optimal visual effect. The three step engraving black/green/yellow only applies on the front slice of the housing. Internal cut-outs are always done before the outline cut, for mechanical stability of the plexi plate in the laser cutting machine.

The compressed file [```digital-font.zip```](digital-font.zip) contains part of the .ttf font-files which have been used for the engraving. They might not be installed on your system. It concerns a free (for personal use) font which was downloaded from the internet somewhere in the 20th century, for which unfortunately the referring website does not exist anymore (http://digitalfont.hypermart.net). The second font, which is used for the optional training front plate, should be part of your operating system. If not, it is available in [```OCR-font.zip```](OCR-font.zip).
