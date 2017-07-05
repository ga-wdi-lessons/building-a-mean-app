# Putting the A in MEAN

> [Back to Main](readme.md)

## Adding Angular to Presidents

In this exercise, our goal is to refactor a full stack express app with server side rendered views, into a Single Page App by adding Angular and using our back-end to render `JSON`.

Solution code for this walkthrough can be found on the `angular-solution` branch of the [WhenPresident repo](https://github.com/ga-wdi-exercises/whenpresident/tree/angular-solution)

---

### Setup

We are going to start from the solution code for the Express-Mongoose class, so go ahead and run the below commands to checkout to the starter code for this exercise...

```bash
$ git clone https://github.com/ga-wdi-exercises/whenpresident
$ cd whenpresident
$ git checkout angular-starter
```

Great, now that we have our MEN app locally, let's take a few minutes to look around at our app's state and get familiar with the files and directories.

<details>
  <summary>
    If we just cloned down an Node app, what else do we need to run to complete our setup?
  </summary>
  <br>

  We need to install our dependencies. If the app uses a particular database, we'll also have to ensure that database is configured and running smoothly on our local machines.

</details>

---

To install our app's dependencies, run...

```bash
$ npm install
```

In another tab, let's run our mongo server...

```bash
$ mongod
```

Then create our database and seed it locally...

```bash
$ node db/seed.js
```

Now lets start our server and make sure everything works...

```bash
$ nodemon
```

If there are no errors in the terminal, we can now navigate in our browser to: `http://localhost:3001/candidates` to interact with our app.

---

#### STOP

---


## **< data-ng-presidents />**

---

Let's take a look at the last commit, ["Added Angular Dependencies"](https://github.com/ga-wdi-exercises/whenpresident/commit/2a97dfb7cc4258d489f318aa09707c0aef97e0ae) to get a sense of our starting point.

We already have a starter file for Angular, `public/js/app.js`, in that file we have our initial module...

```js
angular
  .module("whenPresident", [
    "ui.router",
    "ngResource"
  ])
```

We also loaded in Angular and its sub packages in `views/candidates.hbs`...

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.3/angular.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.3/angular-resource.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-router/0.2.18/angular-ui-router.min.js"></script>
<script src="/assets/js/app.js"></script>

<div data-ng-app="whenPresident">
  <main data-ui-view></main>
</div>
```

### Review Questions

<!-- Q: ng-app  -->
<details>
  <summary>
    What is <code>data-ng-app</code> and what is it doing?
  </summary>
  <br>
  <code>data-ng-app</code> is a directive that initializes our AngularJS app.
  <br>
  <br>
</details>

<!-- Q: ui-view  -->
<details>
  <summary>
    What role does <code>data-ui-view</code> play in our application?
  </summary>
  <br>
  <code>data-ui-view</code> is the placeholder for where all of our state-bound view-templates (defined in our <code>Router</code> function) will go.
  <br>
  <br>
</details>

<!-- Q: root route  -->
<details>
  <summary>
    Which route is currently loading our Angular app?
  </summary>
  <br>
  Our root route, <code>/</code>.
  <br>
  <br>
</details>

---

### [Adds Welcome Page](https://github.com/ga-wdi-exercises/whenpresident/commit/039ef225db7ca933a72e3e587fd616e9242dd837)

In our first step, we need to configure our app's router, and define a state for our app's `welcome-page`.

**Questions:**
<!-- Q: What other component do we need to define   -->
<details>
  <summary>
    What method do we need to start defining states on our Angular module?
  </summary>
  <br>

  <code>.config</code>

  <br>
  <br>
</details>

<details>
  <summary>
     What dependency is necessary to use the method referenced above?
  </summary>
  <br>

  <code>ui.router</code>, which will bring in the <code>$stateProvider</code> service for use in our <code>Router</code> function.

  <br>
  <br>
</details>

<details>
  <summary>
    What is the importance of the first argument for <code>.state</code>?
  </summary>
  <br>

  The first argument is a string containing the name for our state, in this case <code>"welcome"</code>.

  <br>
  <br>
</details>

<details>
  <summary>
    What line in our server's configuration specifies where to look for our app's static assets?
  </summary>
  <code>app.use("/assets", express.static("public"));</code>
</details>

![Welcome-Page-Diff](./images/adds-welcome-page.png)

---

### [Adds Index Route](https://github.com/ga-wdi-exercises/whenpresident/commit/fa68cc105b67527c4986a721b51358dc16d82e2c)

**Steps**:

    1. Define a new state for "index"
    2. Modify an existing file to be the template rendered at that state
    3. Add a link to your "index" state in your welcome page

<!-- Index Route Commit Diff  -->

![Adds Index Route Commit Diff](images/adds-index-route.png)

### [Makes API Routes for Candidates](https://github.com/ga-wdi-exercises/whenpresident/commit/a4207981999f0c9d3544aa5173b0c7ce7d6d4f7a)

Alright, let's review a little bit about what we want to accomplish when building out the Angular side of our application.  

So far, we still are using express to serve at least one server-side rendered view, that loads and initializes our Angular app. From there, Angular takes over the view-templating and routing throughout our SPA. Also, eventually we want our front-end to be able to sync with our back-end in order to persist data throughout our app.

> How can we do this?

<!-- BE comparison to Rails  -->
<details>
  <summary>
    How did we do this in Rails?
  </summary>
  <br>
  By building out our own API, then making AJAX requests from the front-end to our API endpoints in order to keep the data in sync.
  <br>
  <br>
</details>

<br>
We need to do exactly this kind of thing with our MEAN app: we need to setup our back-end to have routes that serve JSON.

**Questions**:

<!-- Q: api namespace  -->
<details>
  <summary>
    Why might it be a good idea to namespace our back-end routes under <code>api</code>?
  </summary>
  <br>
  To eschew confusion between routes meant to serve html and routes that respond with JSON objects.
  <br>
  <br>
</details>

<!-- Q: Delete response  -->
<details>
  <summary>
    What is the significance of the response for our <code>delete</code> request?
  </summary>
  <br>
  To provide a clue to the client that the request went through, and the delete was processed.
  <br>
  <br>
</details>

<!-- Q: Update response  -->
<details>
  <summary>
    What is returned from our <code>put</code> request?
  </summary>
  <br>
  A JSON object with our updated candidate's info!
  <br>
  <br>
</details>

<br>

---

### [Adds Candidate Factory and Connect Index Controller to DB](https://github.com/ga-wdi-exercises/whenpresident/commit/c8f4b58a7bf4cf419e3272a737b812bb767649c7)

Great now that we have our back-end all setup to support requests from the front-end that will return JSON, let's add our Angular component that will allow us to fetch all that data.

<!-- Q: Angular Factory  -->
<details>
  <summary>
    What method do we use on our Angular module  setup in order to get data from our API?
  </summary>
  <br>
  A factory for candidates.
</details>

<br>

Follow the steps below to add an index view for candidates...

    1. Create and define a new "Candidate" factory
    2. Pass your factory as an argument to the index controller and use it to fetch all candidates

<!-- Candidate Factory and Index Controller Commit Diff  -->
<!-- Factory and Controller -->
---

### [Adds Show Route](https://github.com/ga-wdi-exercises/whenpresident/commit/bd3ecd8d54398bd614c1fe1261e71d4eb1cbb57e)

Now that our app is behaving more like a SPA, let's add support for the Show Route by defining another state.

**Steps**:

    1. Create a new state definition for `show`.
    2. Delete `views/show.hbs` and create a template to be rendered when we are at our `show` state.
    3. Define a new controller for `show`, make the appropriate query and display the correct data in the view.

In `public/js/ng-views/show.html`: We need to add a `show` view to display information about a candidate.

In `public/js/app.js`: We need to define a new state, controller, template, and support the query for show.

Finally, we can delete our `views/candidates-show.hbs` file since Angular will be handling our show view from here on out.

---

### [Adds Create Functionality](https://github.com/ga-wdi-exercises/whenpresident/commit/e787c60a8d349a09d94447e42deedf0fa64f4196)

Let's continue building out CRUD functionality, by adding the ability to create a new Candidate...

#### Steps

    1. Update a the `index` view to include a form for creating a new candidate.
    2. Update the index controller to add a definition for our `create` method.
       1. It should persist the new candidate to the database.
       2. Take the user to the new candidate's show page after it is saved.
    3. Update the create route in `index.js` to pass in `req.body` not `req.body.candidate`.
    4. Change our app's body-parser configuration to use JSON.

#### Remaining Tasks

In `public/js/ng-views/index.html` we need to add some UI.

In `public/js/app.js` we need to update the index controller to add a definition for our `create` method.

Next, we'll need to update the route in `index.js`.

---

### [Adds Candidate Update](https://github.com/ga-wdi-exercises/whenpresident/commit/0b2b1546215e7e3cd6af2f6a14c30404f78845f2)

Moving onto the U in CRUD, let's build out our app's update functionality.

<!-- NHO: demo the importance of body parser via postman  -->

**Questions**:

<!-- Q: body-parser  -->
<details>
  <summary>
    What role does <code>body-parser</code> play in our application?
  </summary>
  <br>
  <code>body-parser</code> is necessary middleware that allows us to access the body of post requests from ajax requests and html form submissions. In our app, we use to parse the request's body as JSON.
  <br>
  <br>
</details>

<!-- Q: two-way data-binding  -->
<details>
  <summary>
    What is two-way data-binding in Angular?
  </summary>
  <br>
  Two-way data-binding in Angular apps is the automatic synchronization of data between the model and view components via view-models.
  <br>
  <br>
</details>

<br>


---

### [Adds Candidate Destroy](https://github.com/ga-wdi-exercises/whenpresident/commit/1f63608bb0d5f0712febf4b965c40c1568debff4)

As we put some of the finishing touches on our app, let's add the functionality so a candidate can "concede".

**Steps**:

  1. Modify the "concede" button in `show.html` to run an `update` method on click.
  2. Define an `update` method in your `showCtrl` in `app.js`.
  3. Pass in `$state` to your show controller than use it to redirect the user to the index root after deletion.

Great, now we have completed full CRUD for `candidates` in our MEAN app!

---

## **(Bonus)** Clean Routes


### [Adds HTML5 Mode](https://github.com/ga-wdi-exercises/whenpresident/commit/8cf8fb0ce9ebdb1516940fc62d31cd3aae8dd433)

Next up, we need to configure our app to be a true HTML5 SPA. Part of this process involves cleaning up our url and getting rid of those pesky `#` signs.

**Questions**:

<!-- Q. Root Route  -->
<details>
  <summary>
    What does changing the root route definition to <code>'/*'</code> do and why is it important for our app?
  </summary>
  <br>

  We add the wildcard (*) to our route so that all combinations of routes hit via the url manually will trigger our Angular SPA and allow us to use UI Router's <code>html5Mode</code> to take over routing.

  <br>
  <br>
</details>

<!-- Q. Base Href  -->
<details>
  <summary>
    What is the purpose of adding <code>base href</code>?
  </summary>
  <br>

  Adding the `base href` tag tells our app the base location from which links on a page should be made

  <br>
  <br>
</details>

In `index.js`: change our app's root route...

![Change Root Url ](./images/html5-server.png)

In `public/js/app.js`, we'll enable HTML5 mode. We'll also add our app's base ref in `views/layout-main.hbs`...

![Change Root Url ](./images/html5-angular.png)

> For further reading: checkout [this link](https://github.com/ga-wdi-lessons/angular-routing#locationprovider) to the `$locationProvider` section in the `uiRouter` class

---

### [Adds Redirect to Root Route](https://github.com/ga-wdi-exercises/whenpresident/commit/f1d4585aa70a0ee76ec7b4f960123f3aac0fd476)

Continuing with the work with our app's routes, we need a way to redirect any request not defined in our app's states to a default state.

**Questions**:

<!-- Q. $urlRouterProvider.otherwise -->
<details>
  <summary>
    What is the importance of the argument to <code>$urlRouterProvider.otherwise</code>?
  </summary>
  <br>

  The url to redirect to if any request does not match our app's defined states.

  <br>
  <br>
</details>

<!-- Q. $urlRouterProvider.otherwise -->
<details>
  <summary>
    If you had to guess, when is <code>$urlRouterProvider</code> activated?
  </summary>
  <br>

  <code>$urlRouterProvider</code> makes its check any time a state transition is made.

  <br>
  <br>
</details>

<br>

![adds-redirect-to-root-route](./images/redirect-root.png)

---

> [Back to Main](readme.md)
