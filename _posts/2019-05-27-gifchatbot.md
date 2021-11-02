---
title:  GIF Chatbot
featured: https://i.imgur.com/3j5uUNI.jpg
layout: post
---

For my CS class final project we made this fancy "desktop assistant" sort of thing which uses animated GIFs to interact with the user.
Quick overviews can be found at [my page](https://ctychen.github.io/GIF-Chatbot) and at [my friend and teammate's page](https://fancy.lerdorf.com/gif-chatbot/).


The released versions for the project can be downloaded [from GitHub](https://bit.ly/2I2Y45T) or [from Dropbox](https://bit.ly/2HZH8NC).


### Description:

Our project is a conversational tool, a chatbot of sorts, that responds to a user’s text input and perceived mood with GIFs. Our goal was to make “Alexa ... with memes”. Admit it, we all enjoy sending fancy GIFs to friends in chats, and this tool will help you find the best ones with ease.
This program keeps you perfectly balanced, as all things should be. Feeling down? If it detects that in your response, it sends you some fun images to cheer you up. Getting too excited and recklessly happy? This bot will bring you down to Earth with some depressing memes.
Trying to find a funny reaction image? Need something to spice up a presentation?We got you covered -  just enter one or two key words describing what you’re looking for! Tired of opening YouTube to watch videos? This tool can do a YouTube search for you! Using the Tenor API, this program can find a GIF related to anything you want, and use them to chat with you. Users can use commands to adjust the image results for a better experience. This program is for anyone who likes seeing fun images and is really just something cool to play with.

### Instructions:

Type some garbage into the chat window and admire the GIF responses.
Sentiment analysis is automatically enabled for user inputs that are longer than 2 words.
Type certain keywords to activate features:
Type ‘/’ to enter command mode.

### Available commands:
/get url : copies URL of displayed GIF to clipboard


/refresh : reloads GIF display window


/trash : deletes cached files


/hide shelby : does not display a photo of Mr Shelby in default


/set filter: adjust the content filter (G, PG, PG-13, or no filter)


/resolution : adjust GIF display resolution


/toggle scaling : adjust scaling


/result limit : set the number of GIF results to get


/play (song/video name): play the specified video on YouTube.


/help : see list of available commands

## Features:
### Must Haves:
Web Fetcher/Scraper to pull memes from websites based on category


5/24: Using Tenor API to get GIFs based on user query


Some system which will consistently filter


Display gif/image on screen (5/24: Using Processing PApplet for GIF Display)


Analyzes text input from user and replies with relevant photo/meme/gif (5/24: Uses your search query, or does sentiment analysis on longer inputs)


Does something useful: opens programs, plays music, etc are sample ideas
 (5/24: Playing music using YouTube search)


School appropriate demo mode (doesn’t pull memes off all of Reddit)
 (5/24: Set-filter lets user adjust the results’ content filter, which is set to PG by default)

### Want-To-Haves:
Speech to text with mic instead of typing (for the pi)
 (5/27: Working and implemented! Speech-to-text mode still takes a bit long to get a search result though.)


Sentiment analysis (5/24: Working and implemented!)


Rate memes (help the bot improve future results through user input) (5/24: Not yet...)


Different modes (G, PG, PG-13, no filter) (5/24: Working and implemented!)


## Fancy Results!


Here is the finished product, hardware version:

![finished](https://github.com/the-null-terminator/GIF-Chatbot/blob/gh-pages/img/portfolio/finished.PNG?raw=true)


Hardware version progress pics:


Started with this...

![design](https://github.com/the-null-terminator/GIF-Chatbot/blob/gh-pages/img/portfolio/design.PNG?raw=true)

<!-- ![](https://i.imgur.com/ahGKXkg.jpg) -->
<img src="https://i.imgur.com/ahGKXkg.jpg" width="500"/>

<!-- ![](https://fancy.lerdorf.com/wp-content/uploads/2019/06/61478075_2398156113574534_6942451769377030144_n-1024x768.jpg) -->

<img src="https://fancy.lerdorf.com/wp-content/uploads/2019/06/61478075_2398156113574534_6942451769377030144_n-1024x768.jpg" width="500"/>

<img src="https://i.imgur.com/3j5uUNI.jpg" width="500"/>

<!-- ![](https://i.imgur.com/3j5uUNI.jpg) -->

<img src="https://i.imgur.com/4FmM2aq.jpg" width="500"/>

<img src="https://fancy.lerdorf.com/wp-content/uploads/2019/06/61649198_1369844023163798_2344093330821873664_n-1024x768.jpg" width="500"/>

<img src="https://fancy.lerdorf.com/wp-content/uploads/2019/06/61381785_436487023805332_7927540108268404736_n.jpg" width="500"/>

<img src="https://i.imgur.com/1YyXSW4.jpg" width="500"/>

<img src="https://i.imgur.com/HVwiOCq.jpg" width="500"/>

<img src="https://i.imgur.com/7pnYH0N.jpg" width="500"/>

<img src="https://i.imgur.com/fn8sVAn.jpg" width="500"/>





Software version:


<!-- ![finished](https://github.com/the-null-terminator/GIF-Chatbot/blob/gh-pages/img/portfolio/ui1.PNG?raw=true) -->
<img src="https://github.com/the-null-terminator/GIF-Chatbot/blob/gh-pages/img/portfolio/ui1.PNG?raw=true" width="500"/>

With this version, the user can interact via text input or by using the /record command and then talking. Either way, if the user's input
is 2 words or less in length, a relevant GIF will be displayed as seen in the screenshot above. For longer responses, we apply sentiment
analysis, and a relevant GIF will be found based on the result of the analysis (although sometimes we do get ... interesting results
as can be seen below...)

<!-- ![sentiment](https://github.com/the-null-terminator/GIF-Chatbot/blob/gh-pages/img/portfolio/ui2.PNG?raw=true) -->
<img src="https://github.com/the-null-terminator/GIF-Chatbot/blob/gh-pages/img/portfolio/ui2.PNG?raw=true" width="500"/>

We used the Tenor API to get GIFs; getting that working wasn't too hard as a JSON file with links to GIFs
would be returned for each search query and from there it was just parsing. In order to make looking for images more efficient,
GIFs and JSON files are cached and for each search query the program checks if there are already files for it locally.

## Challenges

Something that took us a long time to figure out was how to play music. Our original goal was, there would be a command that
let the user add songs to a queue and either play specific songs from it or play all. Ideally, the music
would play in the background without opening additional windows. To do this we first looked at using
Spotify or SoundCloud APIs but ran into trouble with both. We also tried seeing how Discord music bots did it, and tested out
the Lavaplayer library. We weren't able to figure out how to get that working, so next attempt: I made a YouTube audio extracting
tool and used that to get the audio from the Youtube video that was the top result for the user's input. This code can be found on the
[video-testing branch of the repo for this project.](https://github.com/ctychen/GIF-Chatbot/tree/video-testing/). In the end
we just did a simple Youtube search, then opening the browser and playing the top video result. It works for now but
if we want to make this even fancier I swear there's a better way of playing music that's more like what we originally thought of.

Speech-to-text was also a pain to set up. We used CMU's Sphinx tools for this and just figuring out how to use it and implement it
into the project took a while. After that, we had to test, and fixing all sorts of issues took even more time. A lot of the
hypotheses (guesses for what it thinks you said) were wildly inaccurate before more fixes were added. As of right now, the speech-to
-text can usually get what you're saying, but processing takes an extremely long time (around a minute or two on my laptop, and
at least double that on the Raspberry Pi). This is an issue that we're still trying to figure out.
