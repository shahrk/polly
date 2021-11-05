<div align="center">

<h1> Hello! Welcome to Poll Me! </h1>

<div align="center">

[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com) 
</div>

![GitHub top language](https://img.shields.io/github/languages/top/Hetthakkar/polly)
![GitHub contributors](https://img.shields.io/github/contributors/Hetthakkar/polly)
![GitHub language count](https://img.shields.io/github/languages/count/Hetthakkar/polly)
![GitHub](https://img.shields.io/github/license/Hetthakkar/polly)
![GitHub last commit](https://img.shields.io/github/last-commit/Hetthakkar/polly)
![Lines of code](https://img.shields.io/tokei/lines/github/Hetthakkar/polly)
[![build](https://github.com/hetthakkar/polly/actions/workflows/build.yml/badge.svg?branch=main)](https://github.com/hetthakkar/polly/actions/workflows/build.yml)
[![DOI](https://zenodo.org/badge/403373361.svg)](https://zenodo.org/badge/latestdoi/403373361)



</div>

<h1> 📹 Project Video </h1>

https://user-images.githubusercontent.com/42487202/135560302-1599ac5a-050d-48e1-b486-bb60f83340ec.mp4

<h1> 💎 What is Poll Me about? </h1>

Poll Me is an app open for all and developed as part of the CSC 510 Software Engineering Project 1. Want to get the opinion of many people on a certain matter, but haven't found a device that supports a large number of users yet? Then Poll Me is the right place for you. This app enables the creation of robust polls that support the use of a large number of users. Each host can create their own virtual room where they can publish their questions and share them with a large number of people. With pre-built survey templates, different survey types can be created and the results can be viewed by both host and player after answering the question. 

<h1> 🚅 Demo </h1>

<img src="https://github.com/hetthakkar/polly/blob/main/images/Enter.png" width="400"/>

<img src="https://github.com/hetthakkar/polly/blob/main/images/Personal%20room.png" width="400"/>

<img src="https://github.com/hetthakkar/polly/blob/main/images/Create%20question.png" width="400"/>

<img src="https://github.com/hetthakkar/polly/blob/main/images/Answer%20question.png" width="400"/>


<h1> 📐 Architecture </h1>

<img src="https://github.com/hetthakkar/polly/blob/lorenz_branch/images/Architecture.png" width="600"/>

<h1>Deployment details</h1>

<h2>Backend</h2>

The backend API is deployed on AWS Lambda using the [serverless framework](https://www.serverless.com/). Automated deploys are setup via a Github action that detects pushes to the main branch in the backend directory present in the project root. The action performs the following steps
- Install dependencies using `npm install`
- Generate prisma client(more about Prisma ORM in `./backend/README.md`)
- Push pending migrations to the database
- Deploy the service on AWS Lambda

The above action requires the following environment variables to be set

- `DATABASE_URL` (URL of your postgres database)
- `SERVERLESS_ACCESS_KEY`(Access key for the serverless framework generated from the [serverless dashboard](https://app.serverless.com))
- `JWT_SECRET`(Key used to sign auth tokens using JWT)
- `ALLOWED_ORIGIN`(Origins that are allowed via CORS)

When a service is deployed to AWS via the serverless framework, the following things happen

- Code is zipped and pushed to an S3 bucket
- API gateway service is created(as we use `http` events for our lambda functions)
- An aws lambda function is created/updated for each function defined in the `serverless.yml` file

<h2> Frontend </h2>

Frontend of the application is deployed on [Netlify](https://netlify.com). Netlfiy detects changes to the front end and creates a production optimized build by running the command

    npm run build

The static site assets are then served via Netlify's CDNs. 

Note: There are many other providers that provide static site deployments like Vercel, AWS Amplify, etc that can be swapped for Netlify in this project

<h1> 📊 UML Diagram </h1>

<img src="https://github.com/hetthakkar/polly/blob/lorenz_branch/images/UML%20Diagram.png" width="600"/>

<h1> 🚀 Local development setup </h1>

<h2> Backend </h2>

- Switch to backend directory
 
      cd backend
- Install dependencies
 
      npm i
- Create and populate `.env` file from the `env.example` template
- Generate prisma client
 
      npx prisma generate
- Start local serverless API 
 
      npx serverless offline      
            
Performing database changes(Refer [prisma docs](https://www.prisma.io/docs/))

- Make your schema changes in the `prisma/schema.prisma`
- To create a migration, use the command

      npx prisma migrate dev --name <migration_name>

<h2> Frontend </h2>

- Switch to frontend directory
 
      cd frontend
- Install dependencies
 
      npm install
- Create and populate `.env` file from the `env.example` template
- Start local serverless API 
 
      npm run start

<h1> ✅ Things that have been done in Phase 1 </h1>

* Designing the Wireframe
* Basic architecture design and implementation
* Backend API implemented using serverless framework
* Front end mobile UI implemented using React
* Database design and schema implementation using Prisma

Live preview available at https://gracious-swirles-4a8c61.netlify.app

<h1> Future scope </h1>

A list of future tasks are described in the issues section of this repository

<h2> A note on scalability </h2>

All the architecture decisions in this project have been motivated with scalability in mind. Hence, we chose `serverless` for our backend and a Jamstack compatible framework(`React`) for our front end. Even though these are highly scalable and robust, there are certain parts of the application that could cause bottlenecks at scale

*Database connections*: , Each serverless function instance that runs requires it's own database connection. This can cause issues at scale as database connections are often quite limited. Following are certain remedies
  - Each serverless function would push their intent into a queue when counting votes. A seperate consumer lambda could then aggregate these votes and count them together
  - Another solution could be to use database connection pools to manage and preserve connections



<h1> 📬 Team Members </h1>

Het Thakkar

Asha Khatri 

Lorenz Scheller

Neelkanth Tripathi 

Divyank Gupta 
