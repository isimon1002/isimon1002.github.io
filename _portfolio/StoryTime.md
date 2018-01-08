---
layout: post
title: Story Time
thumbnail-path: "img/Story Time no user homepage.png"
short-description: The best place on the internet to read and share stories!

---

{:.center}
![]({{ site.baseurl }}/img/Story Time no user homepage.png)

## Summary

There are many places for people to share stories they author online, but most of them are genre specific.  Story Time allows people to read and share stories from a variety of genres in one place.  

## Explanation

I have a friend who is frequently sharing stories he writes on Facebook.  His stories fall within a variety of genres.  The problem with him using Facebook as his platform is that it limits his readership to his Facebook friends.  By using Story Time authors like my friend can share all their stories in one place with anyone anywhere, not just Facebook friends.


## Problem

I am highlighting two problems I had creating Story Time, one technical and one design.

I wrote Story Time in Ruby on Rails and used the devise gem to create users, allow users to sign in and out, and it created the emails that users receive related to signing up for Story Time.  When devise created a user, it created the user without a name using the user's email address as its name.  This caused a problem, because I wanted users to sign up with their name as well as their email address.  Even if the user used a fake name, I wanted to be able to call the users something other than their email address.  The difficulty is that messing with devise is risky and can lead to breaking your website.  I wanted to change devise's sign up page so that it would include and save my users’ names when they sign up without breaking anything.  

A second problem I had was that I after I successfully got Story Time running properly I knew the functionality worked perfectly, but the aesthetics had a lot of room for improvement.  Since Story Time is an important website to me I did not just want it to work, I wanted it to look good as it worked.  My problem is that my skills in making aesthetic choices for websites are limited as most of my experience is focused on functionality and not aesthetics.

## Solution

I solved my problem with signing in by adding a name to the user model and added the name category to the sign-up form.  This part was easy, because it did not interact directly with devise.  Next, I created a registration controller which over ruled parts of devise's registration controller, while leaving most of what devise does alone. This minimal change prevented me from breaking devise.  The registration controller I created added name to the required sign up parameters, and saved the name that the user input, so that my users have a name.

{% highlight ruby %}
class RegistrationsController < Devise::RegistrationsController

   def show
     @user = User.find(params[:id])
   end

  private

  def sign_up_params
    params.require(:user).permit(:name, :email, :password, :password_confirmation)
  end

  def account_update_params
    params.require(:user).permit(:name, :email, :password, :password_confirmation, :current_password)
  end
end
{% endhighlight %}

My solution for my web design problems are currently in progress.  I met a talented web designer named Amy at a meetup.  We started talking and she kindly agreed to collaborate with me on Story Time to improve its design.  We are currently collaborating, and Story Time's design is constantly improving.  

## Results

I was successful in allowing users to use their name when they sign up.  This allowed me not only to include a “you are signed in as user's name”, but also allowed me to create a profile page for each user that includes the stories they authored as well as their name.  

{:.center}
![]({{ site.baseurl }}/img/Stort Time user profile.png)

## Conclusion

I wrote Story Time because my author friend inspired, and Bloc taught me the skills so that when I have an idea for a website I can build it myself and turn my idea into reality.  I am excited to see if Story Time will go viral, but currently I am in the process of trying to get content from authors.  For example, two of the three highlighted story spots on the homepage are empty and I am currently waiting on friends for content.  Once I fill up those spots I plan on advertising Story Time’s existence.  Currently it can be viewed at [Story Time](https://storytime1.herokuapp.com/).
