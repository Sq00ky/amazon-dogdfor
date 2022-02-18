  ### WELCOME/INTRO
  hello everyone!!!
  this is my formal writeup on #amazon #dogdor, aka the vulnerability that shocked the internet that caused a #dataleak on all of amazon's dogs. This repository will contain a full dump of all of amazon's cute dog pictures for your viewing pleasure!!
  
  ### D.O.G.D.O.R
  "Dropping 
  
  Organically 
  
  Grown 
  
  Dogs 
  
  From 
  
  Open 
  
  Repository" 
  
        \- Varg
        
  ### FINDING THE DOGS
  to find this vulnerability, i visited a invalid page on amazon
  <picture 1>
  as you can see, we see dog! if we do a website hack of viewing the sourcecode (by right clicking inspect element, going to sources, clicking the amazon image cdn we can see the url of one dog pic
  only one?!?!?! that's not enough!! we want all the dogs!
  <picture 2>
  
  ### ANALYZING THE DOGS URL
  because we're greedy, we want all the dogs, so we must look at the url:
  
  https://images-na.ssl-images-amazon.com/images/G/01/error/12._TTD_.jpg
  
  <img src="https://images-na.ssl-images-amazon.com/images/G/01/error/12._TTD_.jpg">
 
 as we see, the URL has a number... 12... What if we change this to 13..?
 
  <img src="https://images-na.ssl-images-amazon.com/images/G/01/error/13._TTD_.jpg">
  
  WE GET A NEW DOG! hello FRANK.
  
  ok good. we can now build our #poc
  
  ### BUILDING OUR POC
  now to do this, we're going to build a one-liner bash loop that gets us all the dogs. I already did the hard part, I'm not going to explain the code. You look at it. Read the code. DO IT
  ```
  for I in `seq 1 200`;do curl "https://images-na.ssl-images-amazon.com/images/G/01/error/$I._TTD_.jpg" -O ./$I.jpg;done
  ```
  be careful while running this... it will put over TWO HUNDRED dog pictures in your current folder...
  
  but now, the question EVERYONE wants to know... how many dogs does amazon have?
  what are their names?
  all very good questions... first we will find ALL of the unique dogs that AMAZON has taken pictures of.
  
  ### UNIQUE DOGS
  
  to find all the unique dogs, we will take the sha256 sum (this is the secure hashing algorithmn, it makes no mistakes!! as it uses complicated math!!!). so to do this we will use ANOTHER LOOP to list all of the files, take the hash value of the images, sort them, and count all of the same hashes. it can be done with this command:  
  ```
  for LINE in `ls`; do sha256sum $LINE;done | sort | cut -d ' ' -f 1 | uniq -c
  ```
  if you want to know what it does, read the code or wait for my FULL ANALYSIS....
  
  counting all of the lines, it looks like we only have 83 dogs!! WAIT 83 DOGS?! but we downloaded over 200!! whats the deal with this AMAZON?! why would you reuse DOGS!?!?!
  i dont know... but what i do know is that we have a serious information disclosure vulnerability. We have over 83 PHOTOS OF DOGS AND THEIR NAMES!! using this info we can perform a reverse lookup attack to find all the passwords of the dogs.
  as im sure you all know this is a very critical information disclosure vulnerability and requires at least a P2 on hackerone and bug crowd... For this research, i ask amazon to FIX THIS VULNERABILITY. Dogs should be stored in a secure way!! They must be protected at all costs.
  As a dog owner, i am personally offended at how careless amazon can be with their DOGS!
