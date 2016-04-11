# Putting the A in MEAN

> [Back to Main](readme.md)

## Adding Angular to Presidents

In this exercise, our goal is to refactor a full stack express app with server side rendered views, into a Single Page App by adding Angular and using our back-end to render `json`.

### Setup

We are going to start from a specific commit in `WhenPresident`'s history, so go ahead and run the below commands to checkout to the starter code for this exercise:

If you want to start fresh, clone down the repo:
```bash
$ git clone git@github.com:ga-wdi-exercises/whenpresident.git
$ cd whenpresident
```
After you clone, or after you're working from your local copy:

```bash
$ git checkout c1537cf
$ git checkout -b angular-starter
```

Great, now that we have our MEN app locally, let's take a few minutes to look around at our app's state and get familiar with the files and directories.

<details>
<summary>
**Q**. If we just cloned down an express app, what else do we need to run to complete our setup?
</summary>
<br>
```
We need to install our dependencies, and configure our database locally
 ```

</details>

---

To install our app's dependencies, run:

```bash
$ npm install
```

In another tab, let's run our mongo server
```bash
$ mongod
```

> **Note**: be sure to create and connect to your database if you haven't already

Now lets start our server and make sure everything works

```bash
$ nodemon
```

If there are no errors in the terminal, we can now navigate in our browser to: http://localhost:3001 to interact with our app.

---

#### STOP

---

<!-- NHO: TODO: evaluate the turn in talk or dive into walkthrough of starter  -->
### Turn and Talk (5 mins)

Without writing any code, take 2 minutes to [look through](https://github.com/ga-wdi-exercises/whenpresident/tree/c1537cff04d43de448dc4280711a9e5d92c6de7e) the code and try to determine:

- What parts of app will stay the same
- What parts will need to be removed/modified
- What are some of the files we are going to need for our app

---

## **ng-presidents**

---

Let's take a look at the last commit, ["Added Angular Dependencies"](https://github.com/ga-wdi-exercises/whenpresident/commit/c1537cff04d43de448dc4280711a9e5d92c6de7e) to get a sense of our starting point.

We already have a starter file for Angular, `public/js/app.js`, with our initial module defined:

```js
"use strict";

(function(){

  angular
  .module("candidates", [
    "ui.router",
    "ngResource"
  ]);

})();
```

As well as are currently loading in Angular and its sub packages in `views/candidates.hbs`

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.3/angular.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular.js/1.5.3/angular-resource.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/angular-ui-router/0.2.18/angular-ui-router.min.js"></script>
<script src="/assets/js/app.js"></script>

<div data-ng-app="candidates">
  <main data-ui-view></main>
</div>
```

> **Note**: If you want to work with this app offline, you can use `bower` to load front end asset libraries. See [this commit](https://github.com/ga-wdi-exercises/whenpresident/commit/656343c9db904aca407d9e7aa5caf7945277ea53) for more app configuration.

> Make sure to install `bower` through `npm` and then use `bower` like `npm` to load packages. **Pro-tip**: remember to use `bower install --save` when installing packages and to add `bower_components` to `.gitignore`

Review Questions:

<!-- Q: ng-app  -->
<details>
<summary>
**Q**. What is `data-ng-app` and what is it doing?</summary>
<br>
```
data-ng-app is a directive that initializes our angular-app
 ```
<br>
<br>
</details>

<!-- Q: ui-view  -->
<details>
<summary>
**Q**. What role does `data-ui-view` play in our application?
</summary>
<br>
```
data-ui-view is the placeholder for where all of our angular rendered html templates will go
 ```
 <br>
 <br>
</details>

<!-- Q: root route  -->
<details>
<summary>
**Q**. Which route is currently loading our Angular app?
</summary>
<br>
```
Our root route, "/"
 ```
<br>
<br>
</details>

---

### [Adds Welcome Page](https://github.com/ga-wdi-exercises/whenpresident/commit/d56558786fecd844747fcba1f19f501f71ce73d5)

In our first step, we need to configure our app's router, and define a state for our app's `welcome-page`

![Welcome-Page-Diff](./images/added-welcome-page.png)


<details>
<summary>
**Q**. What existing file can we modify to serve as our welcome template?
</summary>
<br>
```
views/app-welcome.hbs --> public/html/candidates-welcome.html
```
<br>
<br>
</details>

---

### (You-Do) [Add Rudimentary Index Route](https://github.com/ga-wdi-exercises/whenpresident/commit/bfc9247278d8007cf8f1704dc93a3517eaa6d8f0)


<!-- Maybe do entire index route  -->
<!-- https://github.com/ga-wdi-exercises/whenpresident/commit/9f36a80f55e8fe613d39bbda85849e975f32d5a9#diff-f5260081ec80c28a01bd5809279dbfa4R30  -->

---

## Break (10 mins)

---

### [Made API Routes for Candidates](https://github.com/ga-wdi-exercises/whenpresident/commit/963c30d6bae15c10d3e0ed327af29e29c374f888)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

---

### [Adds Candidate Factory and Connect Index Controller to DB](https://github.com/ga-wdi-exercises/whenpresident/commit/9f36a80f55e8fe613d39bbda85849e975f32d5a9)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

---

### [Adds HTML5 Mode](https://github.com/ga-wdi-exercises/whenpresident/commit/915bcc840a4b8e8956ade78c6833f130cb460c78)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

---

### [Adds Redirect to Root Route](https://github.com/ga-wdi-exercises/whenpresident/commit/a8111764bbb0641bd2f26b33932f85256a731c63)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

---

### [Adds Show Route](https://github.com/ga-wdi-exercises/whenpresident/commit/48cf115b7847c8d1601aeff2a23cc5cd0ad7fb5a)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

---

### [Adds Candidate Update](https://github.com/ga-wdi-exercises/whenpresident/commit/c9961f23086850fcd45beb85cd375f7c714d8f35)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

---

### [Adds Candidate Delete](https://github.com/ga-wdi-exercises/whenpresident/commit/331e2649984ef7879796fb766b9322c0a700e8e9)

<!-- TODO: add commit diff  -->

<!-- TODO: add questions  -->

<!-- TODO: review wrap-up  -->
Great, now we have completed full CRUD for `candidates` in our MEAN app.

*If we have time*, we have a few more steps to build out our applications desired features:

---

## **(Bonus)** CRD for Positions
<br>
**[Can Add a New Position](https://github.com/ga-wdi-exercises/whenpresident/commit/d3374a15b00e4a71ad7104c2b2f12178a01895d0)**

**[Can Delete Positions](https://github.com/ga-wdi-exercises/whenpresident/commit/c989c50eab587766456eae349acf3e71a6e6ed49)**

---

## **(Double Bonus)** Add User Endorsements
<br>
**[Adds Endorsement Schema](https://github.com/ga-wdi-exercises/whenpresident/commit/607b73e592d7b7523cd966950bc4def4d752a009)**

**[Adds Endorsements](https://github.com/ga-wdi-exercises/whenpresident/commit/69044912daca740e4379b818813ff84fc0807dee)**

**[Can Endorse a Candidate Only Once](https://github.com/ga-wdi-exercises/whenpresident/commit/6885aed6efa59aefe1820003d9be8ea34898c10d)**

---
> [Back to Main](readme.md)
