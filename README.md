## Project 3 - Walkies 🐾

Walkies is a dog borrowing site, inspired by [borrow my doggy](https://www.borrowmydoggy.com/). 
It was made by [Ava](https://github.com/avayazdan), [Claudia](https://github.com/claudia-pacheco) and [Laura](https://github.com/laura-arch) as part of our Software Engineering Flex course at General Assembly.

Deployed [here.](https://walkiessei22.netlify.app/)

<img width="1433" alt="Screenshot 2022-06-10 at 15 40 28" src="https://user-images.githubusercontent.com/94257616/173097425-913a1240-7955-44d2-8e39-b4429494a9f0.png">

The project aim was to build a Full Stack MERN app that consumes its own RESTful API. We used React, HTML and CSS for Frontend and MongoDB, Node.js and Express for Backend. 


### Table of contents 
 
1. Tech Stack
2. Planning 
3. Build
4. Styling
5. Challenges and Wins
6. Key Learnings
7. Future improvements

## Tech stack

The project utilises React, HTML and CSS, Node.js, MongoDB, NPM, Mongoose and MongoDB Atlas cloud. Tested on Insomnia and Postman.


## Planning 

We used Excalidraw to plan and wireframe our website through a Borrower and Owner point of view. We also drafted some Pseudo code to help us approach the initial set up of the app.
Additionally to that we created a board on Trello to organise and keep track of our timeline. 
<img src="https://user-images.githubusercontent.com/75817925/161280307-a79a28e1-e83e-4cd6-bba9-64ae7e568f6b.png" >
<img src="https://user-images.githubusercontent.com/75817925/161281508-a9f4ac23-2d69-4140-9ad3-8ea52729a37d.png">

## Build

Group project | Timeframe: 2 weeks

The project utilises React, HTML and CSS. As well as MongoDB, NPM and Mongoose. We used Insomnia and Postman to test our API's data and the data was stored on the MongoDB Atlas cloud. 

We decided to build the backend together so we could solidify our knowledge with MongoDB. We used the Live Share option on Visual Studio to code along.
Once we had our Backend completed, we delegated tasks to eachother so we could work on individual Git branches on different components.

The project was split into 2 different Git repositories. Please refer to the backend code [here](https://github.com/claudia-pacheco/walkies-backend).

### Backend 

We built a CRUD API to let users (owners) create a profile for their dogs and Borrowers to message Owners about a specific dog to walk. Throughtout the project we didn't seed data, we opted to test it through Postman/Insomnia.

<img width="426" alt="Screenshot 2022-06-13 at 13 54 51" src="https://user-images.githubusercontent.com/94257616/173358447-9e6ca2b4-0899-4e08-8255-b35a9a50ce68.png">

For instance, if you wanted to create a `Dog`, you would have to be a `owner` - meaning if your role was `borrower` you'd be unauthorized to do so. Should the check be successful, your dog would be created under your user profile.

We stayed on track with our wireframe and created a User and Dog Schema.
<img width="489" alt="Screenshot 2022-06-10 at 16 58 07" src="https://user-images.githubusercontent.com/94257616/173105607-02324bcb-aa41-4c4c-8c8d-5d3664d29618.png">

The use of Mongoose made it easier and neat to link Schemas. For example, we have linked our User schema to the Dog one by referencing the object ID ``type: mongoose.Schema.ObjectId`` to the model ``User``. This was when a dog is created, it will be linked to the owner. This works great in terms of authorisation as it is simple to connect them.

 


  #### Frontend 

<img width="406" alt="Screenshot 2022-06-10 at 15 32 34" src="https://user-images.githubusercontent.com/94257616/173088443-aae7077a-0803-491d-a282-9f8df9330f41.png">

I started by creating a form where the input data is handled by the ```onChange``` event and populates the corresponding labelled data in the API.

<img width="407" alt="Screenshot 2022-06-10 at 15 34 38" src="https://user-images.githubusercontent.com/94257616/173088889-7e8664ab-95a9-4858-b187-8c72e0b31b5d.png">

This was data was then handled by the ``onSubmit`` function incorporated in the form.

<img width="569" alt="Screenshot 2022-06-10 at 15 36 41" src="https://user-images.githubusercontent.com/94257616/173089340-ff4c9391-2eb1-4267-8bc9-de1825b51f72.png">

The function uses ``axios`` to create a POST request to the API so the new user is added. The user is then created in the API and once they login, a access token is generated.


If a user clicks on `View Dogs` they will be presented with a list of dogs that have been fetched from the API. Should they wish to know more about a specific one, they can click on the `More About Me` button. This will open a new page displaying just the information from that dog.


<img width="1425" alt="Screenshot 2022-06-10 at 15 41 35" src="https://user-images.githubusercontent.com/94257616/173090552-e080b8f3-dd6d-4d42-817d-1d3496cd7cea.png">

This was achieved by linking the id of each dog to a new page. 

<img width="458" alt="Screenshot 2022-06-10 at 15 44 07" src="https://user-images.githubusercontent.com/94257616/173091027-a28b9f8f-3561-4e11-a425-63645b8b557a.png">

As you can see in this screenshot, ``x`` stands for each individual dog that is being mapped onto the page, therefore if we want to grab the ID we use ``x._id``. Our API endpoint for fetching each dog is ``dogs/dogId`` so by using ``useParams`` I was able to share the ID of the dog that's been clicked on from the ``dog`` page to the ``dog/dogId``.

<img width="483" alt="Screenshot 2022-06-10 at 15 44 38" src="https://user-images.githubusercontent.com/94257616/173091102-beaf3835-9825-4d3c-b5d9-072be2fb38f0.png">

I had to deconstruct the `dogId` object so I could easily access the value and use it on the fetching GET request endpoint. Additionally, I had to also include the Authorization headers with the access token (stored in LocalStorage after a user logs in) so they would be authenticated and authorised to see the dogs page.

<img width="1422" alt="Screenshot 2022-06-10 at 16 01 10" src="https://user-images.githubusercontent.com/94257616/173094129-82a9bf2c-5eaa-4b0f-b23e-54150098fee3.png">

## Styling

We decided to go for bright colours and use pictures of our family/friends for the Community Stories section. This way our project feels more personalised and intimate. Initially, we were thinking to use a styling library however, we soon realised they were more coplicated than we anticipated! Therefore, we decided to go with vanilla CSS to save us some time. Hopefully in the next projects/future we will be able to work with one.


## Challenges and Wins

### Wins

One of our greatest wins was working successfully as a team and organising our work through Trello boards. This helped us to stay on track with every task that needed to be completed. We kindly accepeted constructive criticism and shared ideas with each other in order to reach the best results possible.

A personal win was definitely succesfully feed data into our API from the Register form. This was a new concept for me as previously we had an external API so it was really cool to have our own and it working successfully. 
Another win was playing around with ``useParams`` and ``LocalStorage``. For the most part, it was successful and we were able to retrieve the correct information without having to place different fetch requests.

### Challenges 

At the beggining we had lots of bugs trying to feed the data into the MongoDB Atlas cloud so we could all work on different devices with the same data. It tooks us a few moments to realise how to properly connect it, but once we figured it out we used the cloud throughout the whole project!

We had a few challanges - such as connecting to MongoDB, deploying our backend without errors and finally (arguably the largest one) uploading our dog data via the frontend to the database successfully. Luckily we had the help of our tutors but we always tried to work on the problem for a couple of hours before asking for help. 

I had quite a lot of trouble to initially grab a specific ID from a different component. I kept getting ``undefined`` on the console so it was very pleasant when ``useParams`` worked.
I wish I had spent some time on styling as I feel like I haven't contributed as much as I would like to.

### Future Improvements

Features to add:

- Adding a Dogs favourites page 
- Implementing a successful chat/inbox messaging system between users

Bugs to fix:

- Currently the `Messages` page doesn't display the comments made individually on each dog. It returns ``undefined`` for the dogId which is quite frustrating taking into account the code is quite similar to the method of passing down the ID from the ``dog to dog/dogId`` pages.
