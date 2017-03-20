# Building a MEAN App

![mean-logo](./images/mean-logo.jpeg)

---

## Learning Objectives

- Identify how different components of a MEAN app work together
- Build a simple MEAN app with data persistence, and dynamic views  
- Provide an example of a MEAN app
- Explain when to choose the MEAN stack

---

## Framing

So far we've studied Express, Mongo, Mongoose, and Angular in isolation, as well as have learned how to build a simple MEN app.

Today we'll complete the MEAN stack by adding Angular to `WhenPresident.`

The term MEAN was coined by a developer at Mongo in a [blog post](http://blog.mongodb.org/post/49262866911/the-mean-stack-mongodb-expressjs-angularjs-andMEAN) discussing his team's workflow. His insights are as follows:

> "By coding with Javascript throughout, we are able to realize performance gains in both the software itself and in the productivity of our developers...With MongoDB, we can store our documents in a JSON-­like format, write JSON queries on our ExpressJS and NodeJS based server, and seamlessly pass JSON documents to our AngularJS front-end."

Now self-promotion aside, his rationale is widely shared around the industry, as MEAN stack apps have risen in popularity since Node, Mongo, Express, and Angular were introduced in 2012.  

> Some popular MEAN apps in production include [Airpair](https://www.airpair.com/), [Open Graph](http://opengraph.io/), and [StartHQ](https://starthq.com/signup)

Ok, sure it's trendy, but why should we use the MEAN stack?

Let's review the use cases for each component:

<!-- Q: Why Express  -->
<details>
<summary>
<strong> Why use Express?</strong>
</summary>
<br>
Express is a minimal and flexible Node.js web application framework that provides a robust set of features for building web apps. Express works with a myriad of HTTP utility methods and middleware that allows developers to create robust APIs quickly and easily
 <br>
 <br>
</details>

<!-- Q: Why Mongo  -->
<details>
<summary>
<strong> Why use Mongo?</strong>
</summary>
<br>

MongoDB is an open-source document database that provides high performance, high availability, and automatic scaling
 <br>
 <br>
</details>

<!-- Q: Why Mongoose  -->
<details>
<summary>
<strong> Why use Mongoose? </strong>
</summary>
<br>

Like ActiveRecord for Rails, Mongoose is an ODM used to represent data from a Mongo database as models in a Javascript back-end. This makes performing CRUD actions to collections and documents in our DB easier.

 <br>
 <br>
</details>

<!-- Q: Why Angular  -->
<details>
<summary>
 <strong>Why use Angular?</strong>
</summary>
<br>

AngularJS is a robust front-end framework that makes it possible to easily and quickly build Single Page Applications. It has lots of functionality built in for rendering data, and swapping views in and out to give the impression of having multiple pages. It is fully extensible and works well with other libraries.

 <br>
 <br>
</details>

<br>

Each of the technologies have their own benefits, but combined, there is power in the ability to work with the same type of objects from the DB, to the Server, to the View, and it is easy for teams to collaborate since it's Javascript throughout the stack.

> "Debugging and database administration become a lot easier when the objects stored in your database are essentially identical to the objects your client Javascript sees. Even better, somebody working on the client side can easily understand the server side code and database queries; using the same syntax and objects the whole way through frees you from having to consider multiple sets of language best practices and reduces the barrier to entry for understanding your codebase."

---

## Where We’re Going

To get a sense of our built out application, let's look at the deployed [When President Solution](http://whenpresident.herokuapp.com)

Playing around with our deployed app, we can see that it is a SPA, and there are no page refreshes, so Angular is doing the heaving lifting with the view. Also pay attention to the url, what's missing?

---

## How We’ll Get There

 You have already created a MEN app with WhenPresident. We are now going to walkthrough adding Angular to the app  [whenpresident](https://github.com/ga-wdi-exercises/whenpresident).

[Code Walkthrough](angular-walkthrough-annotated.md)

---

## What’s Next

- [Deploying a MEAN App](https://github.com/ga-wdi-lessons/deploy-MEAN-app)

---

## Quiz Questions

- What advantages does the MEAN stack offer?
- When type of applications are best suited for the MEAN stack?
- What is HTML5 Mode and how does it affect our angular apps?
- What is the role of `body-parser` in the request-response cycle?

---

## Further Reading

- [MEAN Resources](https://github.com/ericdouglas/MEAN-Learning)
- [MEAN Stack Tutorial](https://thinkster.io/mean-stack-tutorial)

> [Back to Top](readme.md)
