# BitShift-Variations-unrolled
This is Rob Miles Bitshift Variations code unrolled so we can understand how it works. It's based on his original code, published here:

http://txti.es/bitshiftvariationsincminor

and which I have started to "unroll" or format for human reading here:

https://github.com/JamesNewton/BitShift-Variations-unrolled/blob/master/code.c

Unfortunately, the link to the original code shows a message indicating the site will be shut down as of July 1, 2023. As the site is still up as of today, September 18 2023, your mileage may vary. In case the code becomes unavailable, it has been reproduced at the bottom of this file.

This is amazingly cool code!

1. Compact (part of a competition to write a working program in the fewest possible characters)

2. Artistic (the output is actually rather nice... given time)

3. Descriptive (it embodies fundamental rules of a completely different area of study).

What does it do? It makes music. In that amazingly short program are a basic set of rules of good sounding music, including the waveform, notes, chords, and tempos. Looks like gobbly gook. Makes passable music. Amazing. Here is at least 16 minutes of it (the actual program will keep going forever, although it repeats at some, yet unknown, point). It starts slow, but gets going in under a minute.

https://soundcloud.com/robertskmiles/bitshift-variations-in-c-minor

See this video:

https://www.youtube.com/watch?v=MqZgoNRERY8

For a few notes on how it works (beyond the [source code](https://github.com/JamesNewton/BitShift-Variations-unrolled/blob/master/code.c)) see the local [wiki](https://github.com/JamesNewton/BitShift-Variations-unrolled/wiki)

"Let's all" fork this to continue to "unroll" it and document how it works!

If you haven't used github... well... A) you should, and B) this is a great place to start. Git can be very very scary and complex, but getting started is easy: If you see some change you could make to the "code" file listed above, then

- Sign in or sign up for github.
- Fork the project. (Hit the "Fork" button, upper right corner)
- Open the file "code" in your fork (click the file name "code" on the left)
- Edit the file to make your changes (pencil icon next to trash icon)
- When you are done editing, Commit your changes (scroll down, click Commit)
- Make a pull request. (green and white "New Pull Request" button.)
- Assuming your branch is now different from mine (because you committed a change) you should be able to "Create Pull Request"
- I get the pull request and approve it, which makes your changes the current "head" on this project and future forks.

This is using Github without installing Git on your local machine. It's quick, pretty easy, and... collaboration is fun and useful and worth learning to do. If you want to really get into it, start here:

https://help.github.com/

or run through the crash course version I wrote here:

http://techref.massmind.org/techref/app/git.htm

or take the free class from Audacity

https://www.udacity.com/course/ud775

###Original code
####Shutdown Message
As of September 18, 2023, the following message appears above the original code at the link above.
"ATTENTION!! Due to bad actors, txti will be shutting down permanently on July 1st, 2023. Please make arrangements to move your content elsewhere."

As a result, the original code is reproduced below. Its creator is, as written above, Rob Miles. The code is reproduced so it won't become lost, and because it's awesome! No copyright violation is intended.

####The Code

echo "g(i,x,t,o){return((3&x&(i*((3&i>>16?\"BY}6YB6%\":\"Qj}6jQ6%\")[t%8]+51)>>o))<<4);};main(i,n,s){for(i=0;;i++)putchar(g(i,1,n=i>>14,12)+g(i,s=i>>17,n^i>>13,10)+g(i,s/3,n+((i>>11)%3),10)+g(i,s/5,8+n-((i>>10)%3),9));}"|gcc -xc -&&./a.out|aplay

####Explanation
As written, the above code was intended to be run as a shell script, for example a .sh file that can be run in a command prompt. The actual program, the quoted string following "echo", is very well explained, but here's a brief explanation of how the script works.

#####The Script, Unrolled

Lets start by breaking the one-liner into three lines.

echo "g(i,x,t,o){return((3&x&(i*((3&i>>16?\"BY}6YB6%\":\"Qj}6jQ6%\")[t%8]+51)>>o))<<4);};main(i,n,s){for(i=0;;i++)putchar(g(i,1,n=i>>14,12)+g(i,s=i>>17,n^i>>13,10)+g(i,s/3,n+((i>>11)%3),10)+g(i,s/5,8+n-((i>>10)%3),9));}" |
	gcc -xc -&&./a.out |
	aplay

First, the "echo" command is used. It takes everything in the quotation marks, ("") and repeats it.
Ordinarily, the echo command would repeat it to the screen. Using the echo command is one way a script can communicate with its user. In this case though, it's followed with a | character.
The | character tells echo that it should use a pipe to send it to the next program. A pipe is a way of sending whatever a program produces to the next program. When the | character is on the command line, that is what that means. This can be used in linux/unix, Mac OS, Windows, MS Dos, and many more operating systems.

The second line tells the c compiler, gcc, to read from the previous command, aka the pipe, and compile and run the program.
The line ends with a | character. The parameters sent to gcc tell it to run the program it compiled, the program it got from "echo" above. This means the program, the music creator, will now run. It will produce the bytes for the song. The | at the end of that line tells the compiled program to send its output down the pipe to the "aplay" command.
The aplay command, which can be found on linux when alsa sound drivers are installed, takes whatever it reads from the pipe and sends it to the audio device. By default, aplay assumes it will receive 8 bit unsigned samples, and that there are 8000 samples per second.

####Aplay Alternatives

If you don't have alsa drivers installed, true for Windows and Mac OS, as well as in some Linux distributions, there is an alternative program, it's called SOX. SOX is short for Sound Exchange. A big part of its use is to convert and/or play sound files. Here are a couple ways you can install it.
If you use windows, you can download it and follow the installation instructions. if you have Chocolatey installed, this command will work:
"choco install sox"

If using Linux, you can use your package manager to install it. If running a Debian variant, this command will do it.
"apt-get install sox"

On MacOS,, like windows, you can download it from their web site and install it. If you have HomeBrew installed, you can install it with this command.
"brew install sox"

The sox web site is at [https://sourceforge.net/projects/sox/](https://sourceforge.net/projects/sox/)

Below, I'll show how to use it in this context, using the "play" command. If your installation of SOX doesn't include the "play" program, just copy the "sox" command, name the new file "play" with the same extension as sox, if any.

#####Playing

To play, we need only modify the command after the last | character.
Delete the "aplay" command, and use this instead.
"play -b 8 -c 1 -r 8000 -t raw -e unsigned-integer -"
Remember the - at the end, it tells SOX to read from the pipe. Putting it all together then, the new code would be:

echo "g(i,x,t,o){return((3&x&(i*((3&i>>16?\"BY}6YB6%\":\"Qj}6jQ6%\")[t%8]+51)>>o))<<4);};main(i,n,s){for(i=0;;i++)putchar(g(i,1,n=i>>14,12)+g(i,s=i>>17,n^i>>13,10)+g(i,s/3,n+((i>>11)%3),10)+g(i,s/5,8+n-((i>>10)%3),9));}"|gcc -xc -&&./a.out|play -b 8 -c 1 -r 8000 -t raw -e unsigned-integer -

#####The Parameters

The play command is given several parameters, here is an explanation of what they do.

-b 8 - tells sox this is 8bit data.
-c 1 - tells sox this is  a single channel sound, mono not stereo.
-r 8000 - tells sox the sound should be played at 8000 samples per second. 44100 is CD audio quality, this is quite a bit lower.
-t raw - indicates this is raw data, not a .wav file for example.
-e unsigned-integer - tells sox the data is unsigned, and that its integer data. Another example might be -e float, which would expect floating point values.
- - The - tells sox to play from the pipe, or if there isn't one, to play from the keyboard. It's pretty hard to type 8000 characters a second, so this command is usually used to read from another program via a pipe.

I hope this info proves to be helpful to you.
