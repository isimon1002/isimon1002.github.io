---
layout: post
title: BlocChat
thumbnail-path: "img/Blocchat.png"
short-description: BlocChat is a slack like real time message sharing application.

---

{:.center}
![]({{ site.baseurl }}/img/Blocchat.png)

## Summary
BlocChat is a message sharing application that allows users to create usernames and chat rooms.  Users can then send each other messages within chat rooms that can be viewed by anyone within the room live.

## Explanation

BlocChat was the second project I worked on to increase my skills as a frontend web developer through Bloc with the help of my mentor, Mark.  Specifically, BlocChat leveraged my previous skills in HTML, CSS, JavaScript, JQuery, and AngularJS as well as required me to develop new skills to use Firebase with a focus on Firebase's ability to work as a live database.

## Problem

The most difficult part of the project was getting BlocChat to send data to Firebase.  Specifically, when the user creates a chat room, or sends a message, both the chat rooms and messages are stored in Firebase to allow for them to be viewed live.  It was also difficult to get the relationship between the chat rooms and the messages correct to make the messages show up in the room where they are sent.    

## Solution

The solution was to turn both the messages and the rooms into separate objects that would be added to Firebase via Firebase's $add function.  The room object just contains its user created name, but the message object contains the username of its sender, the message itself, the room id for the room from which it was sent, and the time it was sent.  Each room had a Firebase created room id that distinguished it from all other rooms and a function was created to filter all the messages that are contained associated with a given room, so that only those messages show up in the room.   The code below filtered the messages by chat room.  
{% highlight javascript %}
Message.getByRoomId = function (roomId) {
    return $firebaseArray(ref.orderByChild('roomID').equalTo(roomId));
}
{% endhighlight %}

## Results

I succeeded in getting BlocChat to display messages that are associated with a room live by displaying the information that is stored in Firebase.  You can see an example of one such conversation.  

{:.center}
![]({{ site.baseurl }}/img/BlocChat Room.png)

## Conclusion

BlocChat, being completed as a bloc project, was very beneficial. It not only provided me an opportunity to increase my skills as a web developer, it also allowed me to learn Firebase and gain experience incorporating a live database within my website.  Many websites retrieve data stored in a live database for their users to use whether it be a social networking website like Facebook, or websites such as many governmental and university run websites that contain live data.  Due to the work requirements for Bloc it is impossible to have time to make BlocChat as awesome as possible since there is additional course work that needs to be completed. It would be fun in the future to return to BlocChat and make BlocChat more aesthetically pleasing.  Additionally, I would like to add increased functionality to BlocChat such as adding private chat rooms.  
