---
layout: post
title: "Ep.3: Kurt Vonnegut's Slaughterhouse-five and Erlang"
subtitle: "Comparing Kurt Vonnegut's novel Slaughterhouse-five with the
programming language Erlang"
date: 2011-02-16
comments: true
categories: Programming Literature Podcast
permalink: /podcast/slaughterhouse-five-and-erlang
file-url: "https://s3.amazonaws.com/readncode/shows/Read_n_Code_-_3_Kurt_Vonneguts_Slaughterhouse_Five_and_Erlang.mp3"
guid: "http://readncode.com/media/shows/Read_n_Code__3_Kurt_Vonneguts_Slaughterhouse_Five_and_Erlang.mp3"
itunes-keywords: Erlang, Programming, Code, Literature, Kurt Vonnegut, Slaughterhouse-five, Modernism, books, development, read 
duration: "19:15"
summary: "In this podcast I discuss Kurt Vonnegut's novel Slaughterhouse-five. I then talk a little about Erlang, the programming language. As always, I end with an attempt to reconcile and compare
these seemingly dissimilar concepts."
---

<iframe width="100%" height="166" scrolling="no" frameborder="no" src="http://w.soundcloud.com/player/?url=http%3A%2F%2Fapi.soundcloud.com%2Ftracks%2F46487551&show_artwork=true"></iframe>

In this podcast I discuss Kurt Vonnegut's novel Slaughterhouse-five. I then talk a little about Erlang, the programming language. As always, I end with an attempt to reconcile and compare these seemingly dissimilar concepts.

Raw show notes:
--------------

We're in iTunes! Using Ken Fallon's RSS podcast from HPR, I managed to create the RSS feed required for a podcast to be in iTunes.

<strong>Kurt Vonnegut</strong>
born after WWI, died in 2007. Served in WW2
wrote Slaughterhouse-five the year Neil Armstrong landed on the moon.
postmodernism (started after WW2), and I guess continues today, since Thomas Pynchon is still alive.

In short, postmodernist literature takes everything with a large grain of salt, and the stories are often a commentary on the story itself. (like a recursive function) (e.g.: "That was I. That was me. That was the author of this book.")

<strong>Slaughterhouse-five</strong>
     -About an emaciated, fatalistic, and ill-trained soldier named Billy Pilgrim in WW2, who is once compared to a broken kite.
     -The narrative is nonlinear, but it follows some of Billy's experiences in Germany, and then getting caught and shipped to Dresden for community work, where they stay in an old meat-packing house called "Schlachtof-funf"
     -When Dresden is bombed, most are killed, but the American soldiers survived and experienced the total destruction of the city
     -Billy then returns to the US, where he becomes and optometrist, and marries an undesirable obese woman, whose father has a lot of money, and they have children.
     -He suffers head injuries in a plane crash (of which he is the only survivor) and starts thinking he has made a connection with the alien people of Tralfamadore, with whom he has traveled in time and has seen all that will happen in the future.
     -He starts giving radio talks and speeches about the nature of time and flying saucers, and he dies shot at one of these events in Chicago.


<strong>Quotes:</strong>

All this happened, more or less. The war parts, anyway, are pretty much true. One guy I knew really was shot in Dresden for taking a teapot that wasn't his.

As an Earthling, I had to believe whatever clocks said -- and calendars.

All this responsibility at such an early age made her a bitchy flibbertigibbet.

The gun made a ripping sound like the opening of the zipper on the fly of God Almighty

"There's more to life than what you read in books," said Weary.

Like so many Americans, she was trying to construct a life that made sense from things she found in gift shops.

One scout hung his head, let spit fall from his lips. The other did the same. They studied the intinitesimal effects of spit on snow and history.

Now they were dying in the snow, feeling nothing, turning the snow to the color of raspberry sorbet.

Rosewater told a psychiatrist: "I think you guys are going to have to come up with a lot of wonderful new lies, or people just aren't going to want to go on living."

So they were trying to re-invent themselves and their universe. Science fiction was a big help.

"That's the attractive thing about war," said Rosewater. "Absolutely everybody gets a little something."

"I'm afraid I don't read as much as I ought to." said Maggie.
"We're all afraid of something," Trout replied. "I'm afraid of cancer and rats and Doverman pinschers"

And then Russians came on motorcycles, and they arrested everybody but the horses.

So it goes. (appears 106 times in the novel)

There used to be a dog named Spot, but he died. So it goes.
The champagne was dead. So it goes.
The water was dead. So it goes. Air was trying to get out of that dead water. Bubbles were clinging to the walls of the glass, too weak to climb out.


<strong>Erlang:</strong>
based on a one day training session with Kevin Smith @kevsmith
designed by Ericsson in 1986 to support big fault-tolerant applications, released open source in 1998. Stands for Ericsson Language.

<strong>multicore</strong>
          -main feature: great support for concurrency (doing multiple things at the same time)
               -Though I'm not an expert, languages such as Java and Python struggle to efficiently use machines that have tens or hundreds of cores.
               -Erlang has these lightweight processes with minimal overhead, allowing the rapid creation of hundreds of thousands of these processes. These processes have no shared state. They know nothing about each other. They communicate through asynchronous message passing.
                    each process has a mailbox, which it checks to see if it has the message it wants, and then deletes it after it's consumed. Very much how we would ideally check our own email inboxes.
          -to start one of these you just call spawn(Fun), which returns a pid (process ID)

<strong>functional</strong>
          -Immutable variables
               -assignment only
          -functions are first class citizens, that can be used like any other data, like an integer.
          -this basically replaces the need for objects in OO languages

<strong>proven</strong>
          -CouchDB, Membase, Riak, RabbitMQ

<strong>Similarities:</strong>

All this happened, more or less.
spawn(Module, Function, Args) -> pid

Pack a lot of meaning in a few lines: He said that everything there was to know about life was in The Brothers Karamazov, by Feodor Dostoevsky. "But that isn't enough anymore."

<code>A = [1,2,3,4,5].
[1,2,3,4,5]
[X || X <- A, X rem 2 == 0].
[2, 4]</code>

immutable variables - Billy Pilgrim - we find out more about him (and in the process ourselves). This consistency allows us to depend on the narrator more, as we depend on an erlang program more that state will not change in the middle.

functional - jumping in history, future, and dreams, which can all live on their own and can be used independent of one another.

"He is in a constant stage fright, he says, because he never knows what part of his life he's going to have to act in next."
that's like Inboxes and message passing in Erlang.

So it goes. The ending of an Erlang line could be , ; or .



