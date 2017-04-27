# :clock10: µ-controller based Ternary clock with colorful read-out

## What

At school, kids learn to count from 1 to 10 (probably because of the number of fingers on your hands ;-). As such, in daily life, the decimal system is by far the most popular, and most intuitive to use. Computer scientists tend to prefer [binary](https://en.wikipedia.org/wiki/Binary_number) (0-1) or [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) (x0-xF) systems. All of them are just a way of representing quantity (or whatever info you want) in a non-ambiguous way.

In a [ternary or base-3 systems](https://en.wikipedia.org/wiki/Ternary_numeral_system), only 0,1 and 2 are used. Being way less common, reading figures like 12201211 might make your brain-processor to get hot. The µ-controller driven clock in this repository is based on the ternary numeral system.

A web-version is already available in a [related repository](https://github.com/nostradomus/Base3-clock-webversion). In order to see a fully functional demo, click on [this link to our server](http://nostradomus.ddns.net/clock.html).

## Why

Some might find the idea a little crazy, others will say its fun. I think it is an excellent tool to train the brain... and I am probably having a twisted mind :laughing:

Anyhow, after having played around with javascript and css for the [web-version](https://github.com/nostradomus/Base3-clock-webversion), a new challenge popped up. I felt the need for a massive stand-alone living-room version.

## How

Well, lets not reveal everything right away :stuck_out_tongue_winking_eye:

`...more on the way, be patient...`

## Progress status

 - [x] have a [crazy idea](#why)
 - [ ] write the [functional specifications](#how)
 - [ ] build a proof-of-concept prototype
 - [ ] design and build the final [electronics](#electronics)
 - [ ] write [code for the µ-controller](#µ-controller-code) respecting best-practices
 - [ ] design and build a [state-of-the-art housing](#mechanical-construction)
 - [ ] write an end-user manual

## Technical details

### How to read this clock

Each line or column (depending on how you mount the clock) represents a part of the time :

line | description | values
-----|-------------|-------
1 | hours | 00-23
2 | minutes | 00-59
3 | seconds | 00-59

Each element of the line represents one base-3 digit, with a different color for each possible value :
 - 0 : `light off`
 - 1 : `green`
 - 2 : `red`

In a horizontal configuration, the numbers should be read from right to left.

The rightmost element is the least significant trit (yes trit, not bit).

The leftmost element is the most significant trit.

### The Maths, a bit of theory...

The same way binary or decimal numeral systems are based on powers of their respective radices 2 and 10, the **ternary** system is based on powers of `3`.

trit    | least significant |       |        |         |          | ... | most significant
--------|-------------------|-------|--------|---------|----------|-----|-----------------
power   | 0                 | 1     | 2      | 3       | 4        | ... |
decimal | 1                 | 3     | 9      | 27      | 81       | ... |
range   | 0/1/2             | 0/3/6 | 0/9/18 | 0/27/54 | 0/81/162 | ... |

So to convert a ternary number to the decimal system, you have to start with the rightmost digit, multiply it with 3^0, multiply the next digit with 3^1, 3^2, and so on...

So for example (11021)ter = 1x3^0 + 2x3^1 + 0x3^2 + 1x3^3 + 1x3^4 =  (111)dec

The ternary numbers for the clock will have maximum 4 digits (max 3 for the hours).
 - `hours` : (000)ter - (222)ter => (0)dec - (26)dec
 - `mins/secs` : (0000)ter - (2222)ter => (0)dec - (80)dec

### Electronics

`...on the way, be patient...`

### µ-controller code

`...on the way, be patient...`

### Mechanical construction

`...on the way, be patient...`

## Contributors

If you are having any good suggestions, just drop me a line [:email:](http://nostradomus.ddns.net/contactform.html).
If feasible, I'll be happy to implement proposed improvements.
And if you are having lots of time, I'll be happy to share the work with you ;-).

When you create your own version, don't forget to send us some nice pictures of your construction. We'll be happy to publish them in the :confetti_ball:Hall of Fame:confetti_ball:.

## :globe_with_meridians: License

There is no specific license attached to this project.

If you like it, have fun with it (at your own risk of course :-D), and especially, be creative.

Oh, and when using anything from this repository, it is highly appreciated if you mention its origin.
