---
layout: post
title:      "Proof of Concept "
date:       2021-05-04 02:48:05 +0000
permalink:  proof_of_concept
---


I have been afraid to say that I am learning to code to my loved ones because I did not have proof that I was truly capable to code. Being in the self paced program, the difficulty in balancing work, family, and home can make some deadlines seem impossible. However, I am finally done with my proof of concept. My first project...

> *The Youtube Channel CLI information search*

The name is very to the point and not very catchy but I believe it conveys the information that is needed. The journey to create my first project took about a month of weekend work. Though I may have put off more than I could chew, I somehow managed to swallow it down. 

I was not a huge fan of the scrapper labs in Module 6, so I decided to try an API instead. From my new programmer perspective APIs looked much simpler. In reality both have their own positive and negative aspects. One thing that was important to me when designing my CLI application was that I wanted the user to be able to search their own inputs instead of giving the user a list of possible things to search. It was that idea that led me to find the [Youtube API](https://developers.google.com/youtube/v3/quickstart/ruby http://). 

The good thing about the [Youtube API](https://developers.google.com/youtube/v3/quickstart/ruby ) is that there were plenty of resources and guides to get started. Though that does not mean that it was simple. The first half of my project was just understanding how to get the information from the API to connect to my program. I made various accounts, learned what a client secret is (that apparently you should never push to git), learned about tokens. I even at one point learned about refresh tokens, even though I did not implement it. Though it was a trying process I am glad that I used the API, I think that it was a good introduction. 

One I got the API working I  decided to write some “Pseudocode”. I thought it would be a good idea to map out what I wanted the app to do then build from there. Some examples of what I did below. 

` def into
        puts "Welcome to the Youtube Channel CLI information search! Please select from the following options!"
            enter_channel_name
            exit
        end
        exit
    end

    def enter_channel_name(name)
        puts "Please enter the name of a channel that you would like to learn more about."
            if channel_name = true
                channel_options
                #should I make a method about checking if the input is true separate of this then call the method?
            else
                puts "I'm sorry. I could not find that channel. Please enter a channel or type exit to leave the application"
                    if !exit 
                        enter_channel_name
                    else 
                        exit
                    end
            end
    end

    def channel_options
        puts "Here is what you can learn about #{enter_channel_name}"
        while @input !exit
            channel_id
            channel_views
            channel_videos
            #will I need more? Should I figure out how to do top 5 videos instead or something?
        end
        exit
    end

    def channel_id
        puts "This channel's ID is #{item.fetch("id")}.  Please type return to return to the options screen, or type exit to leave the application"
        #will need to find out how to link cross files
            if @input = return
                return
            elsif @input  = exit
                exit
            else 
                "That is not a proper input please try again"
                (#will I need to put something else here to start it over?)
            end 
    end`

After I wrote out what I believed to be the basic idea I then tried to convert it to working methods. I started out with three different option menus and by the time my project was done *I ended up with 9!* It was a very fun journey to get to the final code. I want to retell some of my hardest and favorite epiphanies. 


## Hardest Epiphanies 

Besides the initial struggles with the API, I also had a learning curve when it came to nested arrays. I knew I had to iterate over each and needed to store my information in a way that 1. I could iterate over it and 2. In a way where previous information could be stored without rerunning the API. I think the hardest part of this struggle was the journey I chose to take. I initially thought I needed an array, then I was briefly obsessed with hashes, then after many articles read. I realised that one of my initial nested arrays worked, I just was missing one comma. Being new to coding, the balance between wondering if something is not working because of my capabilities or because it may not exist is hard to balance. Eventually I stored everything properly like the following:
> `@@all_channels_and_items << ["#{self.name}", ["#{(self.video_count)}", "#{(self.date_created)}", "#{(self.description)}", "#{(self.video_count)}", "#{(self.subscriber_count)}"]]`

My last struggle was the classes and modules. When I initially wrote my code, I had one class and I was using global variables to compensate. I got my application to completely work using this so I assumed it was fine. Then I reread the rubric... I was missing examples of class variables and instances of self. I had to rework my completely working application to add some of these things. Going from an application that works with no issues to not running at all because of difficulties linking the modules to the classes can be a little bit of a downer. But, after some time sitting down, breathing, and researching, I was able to rework the program in a way where everything was properly connected. I would put my linking struggle possibly tied with my earlier API struggles.  It is hard to compare the two as one was a starting pain and the other was an ending. I did make a [meme](https://imgur.com/eAd6l2E) to work through my pain. 


## Favorite Epiphanies 

My `where_to_ next` method makes it so after every option choice the user has the question raised to either go the the main menu, search a new channel, or close the application.

> `def where_to_next
>         puts "Please type '1' to return to the option menu,'2' to input a new channel search, or '3' to close."
>         user_input = gets.strip
>         while user_input != '1' && user_input != '2' && user_input != '3'
>             puts "That was not a valid entry."
>             puts "Please type '1' to return to the option menu,'2' to input a new channel search, or '3' to close."
>             user_input = gets.strip
>         end
>         if user_input == '1'
>             channel_options
>         elsif user_input == '2'
>             enter_channel_name
>         elsif user_input == '3'
>             close
>         end
>     end`

Originally I had this code in every method. This made my code longer and was repetitive. This epiphany really helped clean up my code. 


Another epiphany was using the `begin  rescue retry`. This was not something that has been covered in my Flatiron lessons thus far. I found it when I was researching how to make it so my application did not kick the user out when a person searched something that was not in the API. For example, if a person searched “Sykkunoooooo” instead of “Sykkuno” the application would close due to an error. I was able to use the following code.

> 
> `begin
>             @user_input = gets.strip
>             @channel = Project::Channel.new(@user_input)
>         rescue StandardError => e
>             #print(e)
>             puts "I'm sorry. I could not find that channel."
>             puts "Please enter the name of a channel that you would like to learn more about."
>             #puts "#{@user_input}, #{@channel}"
>             retry`
> 

This code makes it so if an error occurs, a message will prompt that an error occurred, and ask them to put in a new input. The retry will rerun the application from where begin is. This cycles until they complete a proper search. 




This project was filled with some amazing highs and some sad lows. I feel like I have finally achieved my proof of concept. I was able to make something. If someone had shown me this last year I would have told them that this was gibberish. I have learned so much this year. I am excited to see what the future modules and projects bring. 

