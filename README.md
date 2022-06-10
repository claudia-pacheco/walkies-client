## Project 3 - Walkies 

This project was lovingly made by [Ava](https://github.com/avayazdan), [Claudia](https://github.com/claudia-pacheco) and [Laura](https://github.com/laura-arch) as part of our Software Engineering Flex course at General Assembly.

Deployed [here.](https://walkiessei22.netlify.app/)

![kdds](https://user-images.githubusercontent.com/75817925/161390251-1b84f54d-4aca-49df-8641-3e7da6242542.png)


## Project Requirements

This project was built for project three of General Assembly's Full-Stack Software Engineering course. The project aim was to build our a MERN stack website/application with own API, utilise our growing knowledge of React as well as connecting backend to frontend for the first time. The project specs allowed us to take inspiration from complex websites/apps that use data such as AirBnb or Facebook, and essentially rebuild it in our own way if we desire.

### Table of contents 

1. Project aims & inspiration 
2. Planning 
3. Build
4. Styling
5. Challenges and Wins
6. Key Learnings
7. Future improvements

## Tech stack

The project utilises React, HTML and CSS. As well as MongoDB, NPM and Mongoose. We used Insomnia and Postman to test our API's data and we stored our data on the MongoDB Atlas cloud.

## Project aim 

Walkies is a dog borrowing site, inspired by [borrow my doggy](https://www.borrowmydoggy.com/).

The functionality of Walkies includes:

- Register a user
- Login a user
- View dogs once you are logged in
- Create a dog
- Message the dog's owner to arrange `walkies`!


## Planning 


![Untitled-2022-03-31-0020](https://user-images.githubusercontent.com/75817925/161280307-a79a28e1-e83e-4cd6-bba9-64ae7e568f6b.png)

Our planning consisted of mostly discussing ideas and their potential caveats or benefits. Once we agreed on an idea, we researched other websites and their functionality and chose what we would like to implement in our own project. As shown above, we used Excalidraw to wireframe our project. Naturally, as we progressed deeper into our project and realised potential flaws or caveats, elements of our wirefrime were changed or edited to suit the new functionalities or elements.
A big part of our planning as well as process was using Trello for organisation and predicting our timeline. This helped tremendously with time management and awareness of what needs to be done next during our the process of building our project. 

![Untitled](https://user-images.githubusercontent.com/75817925/161281508-a9f4ac23-2d69-4140-9ad3-8ea52729a37d.png)

## Build

Group project | Timeframe: 2 weeks

The project utilises React, HTML and CSS. As well as MongoDB, NPM and Mongoose. We used Insomnia and Postman to test our API's data and we stored our data on the MongoDB Atlas cloud at the end of week one. We started by building our backend/API together as a team, we utilised VScode LiveShare and we pushed to the same main branch during this week. During week two, we switched up our workflow, and started using our own Git branches, the reason for this was because on the frontend we split up individual tasks/components, whereas the backend was built together. 

### Backend 

Our [backend](https://github.com/claudia-pacheco/walkies-backend) and client were split up in two seperate files and were two seperate Git repositories. We built a CRUD API to let users create dogs/users and to store our User and Dog data. During our process, we didn't use dummy data - rather we opted to upload testing data via apps like Insomnia or Postman. Our backend consists of User schema, Dog schema, middleware for authorization and error handling, a router, and of course, controllers - which held the functions and logic for our API to work. For example: 

```
// create / list your dog

async function create(req, res, next) {
  console.log(req)
  if (!["owner"].includes(req.currentUser.role)) {
    return res.status(400).json({
      //     message: "You need to be an owner to create a dog! 🐕",
    })
  }
  const newDog = req.body
  newDog.createdBy = req.currentUser._id
  try {
    const createdDog = await Dog.create(newDog)
    console.log(createdDog)
    res.status(201).json(createdDog)
  } catch (err) {
    next(err)
  }
}
```

The utilisation of Mongoose made it more simple for us to write the logic for our API and what we require it to do. The built in CRUD related methods, for example: 

```
router.route("/dogs")
  .get(auth, dogsController.index)
  .post(auth, dogsController.create)

router.route("/dogs/:dogId")
  .get(auth, dogsController.show)
  .put(auth, dogsController.update)
  .delete(auth, dogsController.remove)

router.route("/messages/:dogId")
  .get(auth, commentscontroller.show)
  .post(auth, commentscontroller.create)
  ```
  #### Frontend 
  
  As this is a React app, we followed the methodology and popular conventions of React apps - such as creating **src** folders and **components**. We first began by creating all of our needed components as well as our **App** and **Index** **.js**. We also used **axios** for fetching our API data. 
 
   ```
   axios({
          method: 'get',
          url: 'https://walkies-backend.herokuapp.com/dogs',
          headers: {
            Authorization: `Bearer ${localStorage.getItem("token")}`,
          }
        })
        .then(response => {
          // Console logging the data
          console.log(`doggo data: `);
          console.log(response.data)
  ```
Once we were able to successfully fetch data from the API, we delegated tasks so we could work on different things in individual branches. I was assigned the ```Register, Messages and Dog (Individual)``` pages.

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

Our styling was inspired by colourful and animated websites surrounding our chosen topic. We wanted to make it look modern and easy-to-read. One interesting aspect of our project was that we opted out of using stock photos to using photos of family/friends and ourselves in the Community Stories section in our home page, which subsequently gives our project a more personalised feel. Originally, we had planned to use a styling library, however underestimated how complicated they can actually get! So ultimately we opted for vanilla CSS as to save us some time. For future projects we would aim to implement a styling library for learning and experience purposes. 


## Challenges and Wins

### Wins

One of our wins was working efficiently as a team, organising effectively and utilising the tools available to us effectively. Another win was accepting kind critisim from each other on small things that we may have different opinions on, we listened to eachother with respect and no one overuled one another, it could even be argued that we mastered the skill of working efficiently as a team in a short amount of time! Speaking of time - that was another win of ours. We moved with quick pacing fromt the very get go and that could also be down to our efficient organisation methods and skills. 

A personal win was definitely succesfully feed data into our API from the Register form. This was a new concept for me as previously we had an external API so it was really cool to have our own and it working successfully. 
Another win was playing around with ``useParams`` and ``LocalStorage``. For the most part, it was successful and we were able to retrieve the correct information without having to place different fetch requests.

### Challenges 

We had a few challanges - such as connecting to MongoDB, deploying our backend without errors and finally (arguably the largest one) uploading our dog data via the frontend to the database successfully. Luckily we had the help of our tutors but we always tried to work on the problem for a couple of hours before asking for help. 

I had quite a lot of trouble to initially grab a specific ID from a different component. I kept getting ``undefined`` on the console so it was very pleasant when ``useParams`` worked.
I wish I had spent some time on styling as I feel like I haven't contributed as much as I would like to.

### Future Improvements

Features to add:

- Favorites page would be a great addition to our project (adding a dog or a borrower to your favorites, storing them for later)
- Implementing a chat messenger where users can interact with eachother in real time, or to get an inbox functionality between owners and borrowers

Bugs to fix:

- Currently the `Messages` page doesn't display the comments made individually on each dog. It returns ``undefined`` for the dogId which is quite frustrating taking into account the code is quite similar to the method of passing down the ID from the ``dog to dog/dogId`` pages.


  

