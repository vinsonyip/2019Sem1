# COMP3230 - AngularJS code examples

---------------------------

<details>

<summary><b>Code example : Basic structure of AngularJS program</b></summary>

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl">
            First name : <input type="text" ng-model="fn"><br> <!-- "ng-model" will bind the value of input element to variable:"fn" -->
            Last name : <input type="text" ng-model="ln"><br>
            {{fn+" "+ln}} <!-- This is a "Expression" -->
        </div>
        <script>
            var app = angular.module('myApp',[]);
            app.controller('myCtrl',function($scope){ 
                // Even though you don't want to put anything on input bar, you still need to define the controller, or the expression doesn't work
                $scope.fn = 'Vinson';
                $scope.ln = 'Yip';
            })
        </script>
    </body>
</html>
```

</details>