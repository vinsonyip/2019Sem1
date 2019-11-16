# COMP3230 - AngularJS code examples

---------------------------

<details>

<summary>Code example : Basic structure of AngularJS program</summary>

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
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

<details>

<summary>Using "ng-bind" instead of "{{}}" to define a "Expression"</summary>

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
            First name : <input type="text" ng-model="fn"><br> <!-- "ng-model" will bind the value of input element to variable:"fn" -->
            Last name : <input type="text" ng-model="ln"><br>
            Fullname : <span ng-bind="fn"></span> <span ng-bind="ln"></span> <!-- Another way to define a "Expression" -->
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

<details>
<summary>Using "ng-repeat" to traverse a list</summary>

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
            <p ng-repeat="x in namelist"> {{x}} </p> <!-- A list:"namelist" should be defined in script-->
        </div>
        <script>
            var app = angular.module('myApp',[]);
            app.controller('myCtrl',function($scope){
                // Even though you don't want to put anything on input bar, you still need to define the controller, or the expression doesn't work
                $scope.namelist = [ // Definition of namelist
                    "John",
                    "David",
                    "Abby",
                    "Robbie"
                ];
            })
        </script>
    </body>
</html>
```

</details>

<details>
<summary> Event handler: ng-blur, ng-click, ng-change </summary>

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
            <h1 ng-mouseover="count = count + 1"> Mouse over here</h1> <!-- A variable:"count" should be defined in script-->
            <br>
            {{count}}
        </div>

        <script>
            var app = angular.module('myApp',[]);
            app.controller('myCtrl',function($scope){
                // Even though you don't want to put anything on input bar, you still need to define the controller, or the expression doesn't work
                $scope.count = 0;
            })
        </script>
    </body>
</html>
```

</details>

<details>
<summary> Directives for binding application data to the attributes of HTML DOM elements: ng-show, ng-hide, ng-src, etc. </summary>

```html
<body ng-app=""> <!-- ng-app should be defined as "", or the code don't works -->
Show HTML: <input type="checkbox" ng-model="checkedOrNot">
    <div ng-show="checkedOrNot"><p>Welcome to school.</p></div>
    <div ng-init="myPic = 'pic.jpg'">
        <img ng-src="{{myPic}}">
    </div>
</body>
```

</details>

<details>
<summary> ng-class for dynamically binding one or more CSS classes to an HTML element </summary>

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
        <style>
            .blue{
                background-color:"blue"
            }
            .red{
                color: "red"
            }
        </style>
    </head>
    <body>
        <div ng-app=""> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
            <select type="checkbox" ng-model="changeclass">
                <option value="blue">Blue</option>
                <option value="red"> Red</option>
            </select>
            <br>
            <h1 ng-class="changeclass"> Changing the class and show it here </h1> <!-- "ng-class" change the class by binded variable -->
        </div>
    </body>
</html>
```

</details>

<details>
<summary> An AngularJS "service" example </summary>

## This is sample of a "service"

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
            The hexidecimal of 255 is : {{hex}}
        </div>
        <script>
            var app = angular.module('myApp',[]);
            app.service('hexafy',function(){
                this.myFunc=function(x){
                    return x.toString(16);
                }
            });
            app.controller('myCtrl',function($scope,hexafy){
                $scope.hex = hexafy.myFunc(255);
            })
        </script>
    </body>
</html>
```

## This example shows that how to dynamically use "service" when view changes

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
        The hex you want to transform: <input type="text" ng-model="inputHex"><br>
            The hexidecimal of 255 is : {{hex()}}
        </div>
        <script>
            var app = angular.module('myApp',[]);
            app.service('hexafy',function(){
                this.myFunc=function(x){
                    return x.toString(16);
                }
            });
            app.controller('myCtrl',function($scope,hexafy){
                $scope.hex = function(){
                    var hexval = parseInt($scope.inputHex);
                    return hexafy.myFunc(hexval);
                }
            })
        </script>
    </body>
</html>
```

</details>

<details>
<summary> $http service (client side html) </summary>

## Method 1 : Write http request with $http directive

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
        <p>Welcome message: {{welcomemsg}}</p>
        </div>
        <script>
            var app = angular.module('myApp',[]);
            app.controller('myCtrl',function($scope,$http){
                $http({
                    method : "GET",
                    url : "welcome.html"
                }).then(function(res){
                    $scope.welcomemsg = res.data;
                },function(res){
                    $scope.welcomemsg = res.statusText;
                })
            })
        </script>
    </body>
</html>
```

### Note

response is an object with these properties:

- .config: the configuration object used to generate the request
- .data: a string or an object representing the response body
- .headers: a function used to get header value
- .status: status code of the response
- .statusText: status phrase of the response
=============================

## Method 2 : Shortcut method

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
    </head>
    <body>
        <div ng-app="myApp" ng-controller="myCtrl"> <!--"ng-app" define an AngularJS application, "ng-controller" define a controller to handle variable  -->
        <p>Welcome message: {{welcomemsg}}</p>
        </div>
        <script>
            var app = angular.module('myApp',[]);
            app.controller('myCtrl',function($scope,$http){
                $http.get("welcome.html")
                .then(function(res){
                    $scope.welcomemsg = res.data;
                },function(res){
                    $scope.welcomemsg = res.statusText;
                })
            })
        </script>
    </body>
</html>
```

### List of shortcut methods

- .delete()
- .get()  
- .head()  
- .jsonp()  
- .patch()  
- .post()  
- .put()

</details>

<details>

<summary> Routing using "ngRoute" (Ajax in angularJS) </summary>

## Description: The ngRoute module routes an application to different pages without reloading the entire page, to implement a single page application

```html
<html>
    <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
        <script	src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular-route.js"></script>
    </head>
    <body>
        <div ng-app="myApp">
            <a href="#/!"> Main</a>|<a href="#!apple">Apple</a>|<a href="#!pear">Pear</a><br>
            <div ng-view></div> <!--html pages show here -->
        </div>
        <script>
            var app = angular.module('myApp',["ngRoute"]); // ngRoute is a dependent module to "myApp" module
            app.config(function($routerProvider){
                $routeProvider
                .when("/",{
                    tempUrl : "main.html"
                })
                .when("/apple",{
                    tempUrl : "apple.html"
                })
                .when("/pear",{
                    tempUrl : "pear.html"
                })
            })
        </script>
    </body>
</html>
```

</details>