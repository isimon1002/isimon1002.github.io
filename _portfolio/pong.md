---
layout: post
title: Pong
thumbnail-path: "img/Pong.PNG"
short-description: Table tennis sports game featuring two-dimensional graphics.
---
{:.center}
![]({{ site.baseurl }}/img/Pong.PNG)

## Summary

There are many versions of pong online today.  This version has a home page that allows the user to choose between a one and two player game.  If the user chooses to play against the computer there are three levels to choose from, easy, medium and hard.  Pong was also the first website I created that I felt was ready for public consumption and therefore can be played online [here](https://d3gkh9werr34rn.cloudfront.net/).  

{:.center}
![]({{ site.baseurl }}/img/pong home.png)     
## Explanation

Pong was my first bloc specialization project.  I chose it, because I had not yet created any online games and I thought creating pong would be a good opportunity for me to learn how to create games.  One thing that is important when you create one player games is artificial intelligence.  Frequently in one player games, such as pong, the user plays against a computer.  For the computer to be difficult for the user to beat, it needs an artificial intelligence.  Programming pong was my first experience creating an artificial intelligence and I enjoyed the experience. Since Pong was ready for public consumption it was also my first opportunity to use Amazon Web services to deploy a website.     

## Problem

I ran into two problems creating my pong game.  The first one was related to the canvas.  I could draw it, but when I moved the paddle the location where the paddle used to be did not reset.  The second problem I had was creating an artificial intelligence.  How do I get the computers paddle to move intelligently towards the ball, but not be impossible to beat?    

## Solution

To solve the problem with the canvas I changed the render function that I used to display it.  Originally it was white rectangle with a black boarder.  I changed it to a black rectangle.  
{% highlight javascript %}
var render = function() {
  table.fillStyle = "black"
  table.fillRect(0, 0, width, height);
  // Other things I also rendered //
}
{% endhighlight %}

I created a ball object that contained the location of the ball as it moved, so I knew where the ball was, but I still needed to figure out how to use that mathematically to make sure the computer's paddle moved with the ball.  I also had a move function that I used for the player to move the player paddle, but by clicking the player manually inputs information into the function to move their paddle intelligently.  I needed the computer to input that information based on the location of the ball.  To do this I created a new function that.  The function finds the difference between where the paddle is and the ball is along the y axis and inputs that difference into the move function.  It also uses the paddle width to make sure it hits the ball slightly off center to make the ball move at an angle.  I then added limits to the diff value to make it possible to beat the computer.  Without limits to the diff value the computer would immediately move the paddle to the location of the ball on the y axis making it impossible to score.  

{% highlight javascript %}
Computer.prototype.update = function(ball){
  var y_ball = ball.y;
  var diff = -((this.paddle.y + (this.paddle.width / 2)) - y_ball);
  if(diff > 3){
    diff = 3;
  }
  else if(diff < -3){
    diff = -3;
  }
  computer.paddle.move(diff)
}
{% endhighlight %}

## Results

I was successfully able to create a pong game with artificial intelligence.  Instead of me posting a gif of the game in action please play it and see for [yourself](http://aws-website-pong-czg7o.s3-website-us-east-1.amazonaws.com/).  


## Conclusion

Pong, being completed as a bloc project, was very beneficial. Completing pong provided me with the opportunity to learn about artificial intelligence as well as how to deploy a website on amazon web services which many businesses use to deploy their websites.  This allowed me to not only increase my programming skills, but also my deployment skills that hopefully I can leverage professionally.  It also provided me the opportunity to put in extra work on a project to make it the way I wanted it.  For example, the project was completed with me just creating one level and that was it.  I decided to do extra work to gain practice creating a home page, creating a multi-level game, creating a two-player game.  Creating the home page, multiple levels, and the two-player level was extra practice of my HTNL, CSS, and JavaScript skills.      
