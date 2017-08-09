---
layout: post
title: BlocJams
thumbnail-path: "img/bloc_jams_bg.jpg"
short-description: BlocJams is a Spotify like music player that allows you to listen to awesome music.

---

{:.center}
![]({{ site.baseurl }}/img/bloc_jams_bg.jpg)

## Summary
There are many music players on the market that come with all types of functions at the expense of cost.  BlocJams is a simple music player that lacks some of the functionality of market leaders like Spotify, but makes up for it by being free to use and allowing the user unlimited access to its preloaded music.     
## Explanation

BlocJams was the first project I did to increase my skills as a frontend web developer through Bloc with the help of my mentor, Aaron.  Specifically, BlocJams required me to increase my HTML and CSS skills.  It also taught me how to use a programming language, in this case JavaScript, with a library and a framework since I used the JQuery library and the AngularJS framework.  

## Problem

Problems that I solved during the creation of BlocJams involved how to make both the player bar and the seek bar interactive so that the user can start and pause songs, switch to the next song, and return to a previous song in the player bar and move throughout a song and change the volume in seek bars.  

## Solution

The player bar was made interactive by functions that were called when the user clicked on buttons in the player bar.  For example, when a user clicked on the play button a function is called that causes the music to start to play and when the user clicks on the pause button a function is called that pauses the music.  When the user clicks on the previous button a function is called that switches to the previous song and when the next button is called a function switches to the next song.  An example of one of these functions is the next function in the SongPlayer service.  
{% highlight javascript %}
SongPlayer.next = function() {
   var currentSongIndex = getSongIndex(SongPlayer.currentSong);
   currentSongIndex++;
   if (currentSongIndex >= currentAlbum.songs.length) {
       currentBuzzObject.stop();
       SongPlayer.currentSong.playing = null;
       }
   else {
       var song = currentAlbum.songs[currentSongIndex];
       setSong(song);
       playSong(song);
     }
 };
{% endhighlight %}

To maintain the MVC framework the PlayerBar controller has access to all the functions within the SongPlayer service and the functions are called from the PlayerBar controller and not the SongPlayer service when they are clicked.  

Both the volume and music seek bars were made interactive by creating custom functions for the seek bar that did things like calculate the percentage of the total seek bar based on where the user clicks to tell BlocJams to play at that percentage of the total song, or that percentage of the total volume.   The function that calculated the percentage of the seek bars is shown below.

{% highlight javascript %}
var calculatePercent = function(seekBar, event) {
   var offsetX = event.pageX - seekBar.offset().left;
   var seekBarWidth = seekBar.width();
   var offsetXPercent = offsetX / seekBarWidth;
   offsetXPercent = Math.max(0, offsetXPercent);
   offsetXPercent = Math.min(1, offsetXPercent);
   return offsetXPercent;
};
{% endhighlight %}

## Results

I was successfully able to create an interactive player bar and seek bars that allow users to change the volume of the song and location within a song as well as play, pause, skip to the next song, and return to a previous song.  You can watch the next button inaction below.   

{:.center}
![]({{ site.baseurl }}/img/giphy.gif)

## Conclusion

BlocJams, being completed as a bloc project, was very beneficial. It not only provided me an opportunity to increase my skills as a web developer and to learn AngularJS, but it also allowed me to learn about the MVC framework. For example, you do not call service functions in the HTML, so you must create controller functions that have access to service functions to maintain the separation between the model and the controller. Due to the work requirements for Bloc it is impossible to have time to make BlocJams as awesome as possible since there is additional course work that needs to be completed. It would be fun in the future to return to BlocJams and add additional functionalities to it such as allowing users to create playlists and upload their own music.   
