# A Native AngularJS multiselect directive


#### index.html
```html
<!DOCTYPE html>
<html ng-app="plunker">
  <head>
    <script src="app.js"></script>
    <script src="multiselect.js"></script>
  </head>
  <body ng-controller="MainCtrl">

    <multiselect multiple="true" ng-model="selectedCar" options="car.id as car.name for car in cars" template-url="/multiselect.tmpl.html" />
    <div class="well well-small">
        {{selectedCar}}
    </div>

  </body>
</html>
```


#### multiselect.tmpl.html
```html
<div class="btn-group">
  <button type="button" class="btn btn-default dropdown-toggle" ng-click="toggleSelect()" ng-disabled="disabled" ng-class="{'error': !valid()}">
    {{header}} <span class="caret"></span>
  </button>
  <ul class="dropdown-menu">
    <li>
      <input class="form-control input-sm" type="text" ng-model="searchText.label" autofocus="autofocus" placeholder="Filter" />
    </li>
    <li ng-show="multiple" role="presentation" class="">
      <button class="btn btn-link btn-xs" ng-click="checkAll()" type="button"><i class="icon-check"></i> Check all</button>
      <button class="btn btn-link btn-xs" ng-click="uncheckAll()" type="button"><i class="icon-check-empty"></i> Uncheck all</button>
    </li>
    <li ng-repeat="i in items | filter:searchText">
      <a ng-click="select(i); focus()">
        <i ng-class="{'icon-check': i.checked, 'icon-check-empty': !i.checked}"></i> {{i.label}}</a>
    </li>
  </ul>
</div>
```


#### app.js
```js
var app = angular.module('plunker', ['ui.multiselect']);

app.controller('MainCtrl', function($scope) {
  $scope.cars = [{id:1, name: 'Audi'}, {id:2, name: 'BMW'}, {id:3, name: 'Honda'}];
  $scope.selectedCar = [];
});
```


#### After selecting 'Audi' and 'Honda', the model will look like:
```
  $scope.selectedCar = [1, 3];
```


#### Change options to `car.name for car in cars` for a data model like:
```
  $scope.selectedCar = [{id:1, name: 'Audi'}, {id:3, name: 'Honda'}];
```

#### Changing options to `car.id for car in cars` will change the options labels in the UI:
`'Audi', 'BMW', 'Honda'` -> `'1', '2', '3'`


## Example
http://plnkr.co/edit/LPGYIf?p=preview

## License

MIT
