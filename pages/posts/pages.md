---
title: Senior Project
date: 2021/3/3
description: Learn about the hardships and new discoveries I made when developing with my senior project team.
tag: Senior Project
author: Dean Cutalo
---

## Project Idea
My teammates and I, consisting of 6 members total, decided to call our project gaspal. The goal for the project was to allow users to see how many gallons of gas a trip would take. Users would create a new trip giving start and end points. The app would then give them the amount of gallons of gas the trip would take and be able to compare that with the amount of gas they have currently.

## Project Setup

After my teammates and I discussed the tech stack we would use it was time to setup the project. We all agreed on using the MERN stack, I volunteered to set up the project for development as this was my first time doing so and I thought it would be a good learning experience. I started off by creating a git repository, then it was time to setup the dependencies for the project using homebrew. Homebrew is available to macOS and linux, for the entirety of the project I developed on mac. After I created the project and all of its dependencies it was time to create a comprehensive readme so my team was aware of the development process. The readme contained information pertaining to project setup, feature development, deploying, production and general git references. At first I did not properly setup the merge and code review process on github, each teammate was able to directly push to main without any other teammates approval. After realizing this I changed the process making each member create a feature branch and having them do pull requests. After the pull request was made one other member needed to review the code and give the thumbs up before merging with main.

## Design Document GasPal

High level Description:
- GasPal is a gas-tracking service.
- The website will give information about available car mileage based on
information provided by the user.
- GasPal will provide financial advice on how to save money on gas and how your
driving style affects the gas mileage of your car.
- Our app will use google maps to monitor users fuel gauge and update it within
the application.
- Users will be greeted with a login with the choice of creating an account or
logging in if one exists.
- After logging in users will provide year, make, model, total number of gallons and
current number of gallons.
- GasPal will provide notifications and user authentication based on user email.
- Users will be greeted with a fuel gauge and a variety of actions to choose from one
being the trip function. The trip function will allow users to choose a car and a destination. Users will be provided with gps for their selected route created by google maps.

(I did not include the website design since they are just crude drawings.)

## Tab Selection Options

Gas Gauge Page (default initial tab)
- Estimated Mileage
- Manual Gas input (text field)

User Profile
- Update email
- Change username
- Change password
- Update car information
- Log out
- Delete profile

Gas Efficiency Reports
- Input gas acquired

Trip
- Start trip
- End trip
- Create trip category

## DB Design

User
- user_id (PK) int
- OAuth_Store [email, id, etc. - still unclear]
- email varchar(25)
- username varchar(15)

Car
- car_id (PK) int
- make varchar(15)
- model varchar(15)
- year int
- trim varchar(25)
- package varchar(20)
- tank_capac [sourced from fueleconomy.gov] float(4,1)
- mpg [sourced from fueleconomy.gov] float(5,2)

Trip
- trip_id (PK) int
- car_id (FK) int
- user_id (FK) int
- start_adr varchar(90)
- end_adr varchar(90)
- distance [float representing miles between start_adr and end_adr] float(6,2)

User_Owned_Car
- user_id (pK) int
- car_id (pK) int
- current_fuel_amt float(4,1)

## RESTful API

/api/user/user_id/car/car_id
- GET returns each registered users account credentials and car information

/api/user/user_id/car
- POST add users with car information

/api/user/user_id
- PUT Update any changes to the users account

/api/user/user_id
- DELETE a users account
- Terminating any user data and session tokens

```json
# POST
{ user:
username: “...”
email: “...”
password: “...” 
re-enter_password: “...”
}
```

```json
# POST
{ car:
year: 2002
make: “...”
model: “...”
trim: “...”
fuel economy→ Total_gallons: 0.0 Cur_gallons: 0.0
}
```

```json
# PUT
{
user: "..."
car: [car1, car2, ...]
trip:[trip1, trip2, ...] 
}
```

```json
# POST
{ trip:
user: “...”
car: “...”
start_address: “...”
end_address: "..."
trip_status: bool
}
```

```json
# GET
{ gauge:
car: [car1]
fuel_added: 0.0 
}
```

## API
- Google Maps
- fueleconomy.gov

## User authentication/Security
- Node.js, Express library, REST client
- All passwords will be hashed
- Express will be used as the server framework
- Express will be used to handle HTTP requests such as POST and GET
- Use REST client to create HTTP requests
- AuthO to manage user authentication

Tech Stack

Platform

- Website on windows and macos

Development Tools

- Version control: using github
- Each team member has the choice of their own text editor
- IntelliJ with Android Studio or VSCode
- Trello Board for issue/bug tracking

Backend

- Node.js for executing code on server side. Express.js framework for building the web application. MySql database to store users information.

Frontend

- React.js for UI components

## Other Promising Solutions that were considered

- Firebase provides much more centralized and elegant solutions to integrate different aspects of the application together for a collaborative development environment
- Firebase, while providing an unfamiliar NoSQL database solution can be integrated with many other Languages to interact with and configure APIs and DB functions
- Using Flutter is a straightforward technology to streamline both iOS and Android development over the likes of React.js or React Native