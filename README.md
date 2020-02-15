# MorningSTAR
![image](https://user-images.githubusercontent.com/54637957/74596502-c18d0000-5015-11ea-823b-4eb61b00cc4e.png)
> PC repair tracking for HBCI

# Waaaat the hell

So basically 🤞🤞, this is going to replace morningSTAR at some point, I didn't want to start with a dirty code base, so I figured I'd start from scratch.

# 🚧Build Instructions🚧

`nuxt generate`

Due to buisness requirements, I couldn't make this run as an app with dynamic routing, so, each SO is just opened as reference
from a list.

# Usage

## Homescreen
![image](https://user-images.githubusercontent.com/54637957/74596428-b38aaf80-5014-11ea-97eb-7239b609bd25.png)

Here we have the homescreen, the buttons along the bottom lead to all the major functionality of the app, 
but there is also a hidden menu in the upper right that persists across screens

## New Repair

![image](https://user-images.githubusercontent.com/54637957/74596444-e765d500-5014-11ea-9fcf-6c72711b793f.png)

This page is for when a customer drops off a PC, it does not do a DB query to find the information, so it will have to
be looked up in iVue if the customer cannot provide account numbers and the like.

once you click "Create New Repair", the repair is put into the queue.

## Repair Queue

![image](https://user-images.githubusercontent.com/54637957/74596474-3ca1e680-5015-11ea-8ea3-3743aba50f97.png)

This page contains all the active repairs for PC's that the company has physically being worked on.

The "More Details" button will show you more information about why it was checked in and more customer information


## Checkout

![image](https://user-images.githubusercontent.com/54637957/74596487-7f63be80-5015-11ea-8bb8-b6f03ca85f2c.png)


once a repair as been completed, the repair goes into the "Checkout" Queue, meaning it is now ready for the customer to
pick up and pay for, from here, it would be sent to the archives, so it can be referenced at a later date.
