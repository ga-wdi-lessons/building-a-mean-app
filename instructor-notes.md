# Building a MEAN App

Angular Walkthrough Code Snippets

## Setup

```bash
$ git clone git@github.com:ga-wdi-exercises/whenpresident.git
cd whenpresident
git checkout angular-starter
git checkout -b angular-inclass
npm install

# in another tab
mongod

node db/seeds.js
mv sample.env.json env.json
nodemon
```


## Adds Welcome Page

```js
// public/js/app.js
  .config([
    "$stateProvider",
    Router
  ]);

  function Router($stateProvider){
    $stateProvider
    .state("welcome", {
      url: "/",
      templateUrl: "/assets/html/candidates-welcome.html"
    });
  }
```

## Adds Rudimentary Index Page

In `public/html/candidates-welcome.html`
```html
<h2><a data-ui-sref="index">Which candidate will you pick?</a></h2>
```

```js
// public/js/app.js
.state("index", {
  url: "/candidates",
  template: "<h2>This is the candidates index page.</h2>"
});
```

## Makes API Routes for Candidates

In `index.js`: modify our app's routes
```js
app.get("/api/candidates", function(req, res){
  Candidate.find({}).then(function(candidates){
    res.json(candidates);
  });
});

app.get("/api/candidates/:name", function(req, res){
  Candidate.findOne({name: req.params.name}).then(function(candidate){
    candidate.isCurrentUser = (candidate._id == req.session.candidate_id);
    res.json(candidate);
  });
});

app.delete("/api/candidates/:name", function(req, res){
  Candidate.findOneAndRemove({name: req.params.name}).then(function(){
    res.json({success: true});
  });
});

app.put("/api/candidates/:name", function(req, res){
  Candidate.findOneAndUpdate({name: req.params.name}, req.body.candidate, {new: true}).then(function(candidate){
    res.json(candidate);
  });
});

app.listen(app.get("port"), function(){
  console.log("It's aliiive!");
});
```

## Adds Candidate Factory

```js
// public/js/app.js

.factory.("Candidate", [
  "$resource",
  Candidate
])

.controller("candIndexCtrl", [
  "Candidate",
  candIndexCtrl
])

// in router function
.state("index", {
  url: "/candidates",
  templateUrl: "assets/html/candidates-index.html",
  controller: "candIndexCtrl",
  controllerAs: "indexVM"
})

function Candidate($resource){
  var Candidate = $resource("/api/candidates/:name", {}, {
    update: {method: "PUT"}
  });
  Candidate.all = Candidate.query();
  return Candidate;
}

function candIndexCtrl(Candidate){
  var vm = this;
  vm.candidates = Candidate.all;
}
})();
```

In `public/html/candidates-index.html`
```html
<h2>{{indexVM.candidates.length}} candidates</h2>
<h3 data-ng-repeat="candidate in indexVM.candidates">
  <a href="/candidates/{{candidate.name}}">{{candidate.name}} for President in {{candidate.year}}</a>
</h3>
```

## Adds HTML5 Mode

```js
// index.js
app.get("/*", function (req, res){
  res.render("candidates")
})
```

```js
// public/js/app.js
.config([
  "$stateProvider",
  "$locationProvider",
  Router
])

function Router ($stateProvider, $locationProvider) {
  $locationProvider.html5Mode(true)
}
```

```html
<head>
  <title>When President</title>
  <link rel="stylesheet" href="/assets/css/styles.css" />
  <base href="/"></base>
</head>
```

## Adds Redirect to Root Route

```js
// public/js/app.js
.config([
  "$stateProvider",
  "$locationProvider",
  "$urlRouterProvider",
  Router
])
s
function Router ($stateProvider, $locationProvider, $urlRouterProvider) {

  // after state definitions
  $urlRouterProvider.otherwise("/")
}
```

## Adds Show Route

```js
// index.js

app.get("/api/candidates", function (req, res) {
  Candidate.find({}).lean().exec().then(function(candidates){
    candidates.forEach(function(candidate){
      candidate.isCurrentUser = (candidate._id = req.session.candidate._id)
    })
  })
})
```
In `public/html/candidates-show.html`
```html
<div data-ng-if="!showVM.candidate">
  <h2>That candidate couldn't be found!</h2>
</div>
<div data-ng-if="showVM.candidate">

  <h2>{{showVM.candidate.name}} for President in {{showVM.candidate.year}}!</h2>
  <div data-ng-if="showVM.candidate.isCurrentUser">
    <input type="number" placeholder="Year" data-ng-model="showVM.candidate.year" />
    <button>Edit Platform</button>
    <button>Concede</button>
  </div>

  <div data-ng-repeat="position in showVM.candidate.positions">
    <p>{{position}}</p>
    <button data-ng-if="showVM.candidate.isCurrentUser">Change your mind</button>
  </div>

  <div data-ng-if="showVM.candidate.isCurrentUser">
    <textarea></textarea>
    <button>Add a position</button>
  </div>

</div>
```

```js
// public/js/app.js

.controller("candShowCtrl", [
  "Candidate",
  "$stateParams",
  candShowCtrl
]);

.state("show", {
  url: "/candidates/:name",
  templateUrl: "/assets/html/candidates-show.html",
  controller: "candShowCtrl",
  controllerAs: "showVM"
});


function Candidate($resource){
  var Candidate = $resource("/api/candidates/:name", {}, {
    update: {method: "PUT"}
  });
  Candidate.all = Candidate.query();
  Candidate.find = function(property, value, callback){
    Candidate.all.$promise.then(function(){
      Candidate.all.forEach(function(candidate){
        if(candidate[property] == value) callback(candidate);
      });
    });
  }
  return Candidate;
}
```

## Adds Update

In `index.js`: configure `body-parser`
```js
app.use(parser.json({extended: true}));
```

In `public/html/candidates-show.html`: replace the `edit` button with
```html
<button data-ng-click="showVM.update()">Edit Platform</button>
```

In `public/js/app.js`: add update function to `candShowCtrl`
```js
vm.update = function(){
  Candidate.update({name: vm.candidate.name}, {candidate: vm.candidate}, function (){
    console.log("Done updating");
  })
}
```

## Adds Candidate Delete

In `public/html/candidates-show.html`: replace the "concede" button with
```html
<button data-ng-click="showVM.delete()">Concede</button>
```

In `public/js/app.js`: add `$window` to `candShowCtrl`
```js
.controller("candShowCtrl", [
  "Candidate",
  "$stateParams",
  "$window",
  candShowCtrl
]);


function candShowCtrl(Candidate, $stateParams, $window){
  var vm = this;
  Candidate.find("name", $stateParams.name, function(candidate){
    vm.candidate = candidate;
  });
  vm.update = function(){
    Candidate.update({name: vm.candidate.name}, {candidate: vm.candidate}, function(){
      console.log("Done!");
    });
  }
  vm.delete = function(){
    Candidate.remove({name: vm.candidate.name}, function(){
      $window.location.replace("/");
    });
  }
}
```
