# LẬP TRÌNH  FRONT-END

# VueJS

### I. NỘI DUNG TÌM HIỂU

#### 1. VueJS là gì?
**Vue.js** (View) là 1 thư viện Javascript UI mới (again) đang khá là hot trong thời gian gần đây.
 Vue.js là một framework linh động (nguyên bản tiếng Anh: progressive – tiệm tiến) dùng để xây dựng giao diện người dùng (user interfaces). Vue cũng đáp ứng được dễ dàng nhu cầu xây dựng những ứng dụng một trang (SPA - Single-Page Applications) với độ phức tạp cao hơn nhiều.

  - **Cách sử dụng:** Để sử dụng Vue thì rất là đơn giản. Chỉ cần thêm đoạn script HMTL này vào là bạn đã có thể sử dụng Vue trong trang web

  ```javascript
  <script src="https://unpkg.com/vue@next/dist/vue.js"></script>
  ```
Sau đây là 1 ví dụ tạo 1 instance Vue. Trong đó trường el là trường sẽ được mounted.

Dữ liệu để mount tới el đã được định danh ở phía trên sẽ được định nghĩa ở trong trường data, và dữ liệu này sẽ được truy cập qua các template.

Để rõ hơn thì mình có 1 đoạn code HTML như sau:
```html
<div id="app">
  <p>{{ message }}</p>
</div>
```
1 điều cần lưu ý ở đây là thẻ div với id mà chúng ta đã trỏ tới ở phía trên. Và 2 dấu ngoặc nhọn **{{ message }}** được sử dụng để hiển thị dữ liệu được truyền tới.

 ```javascript
  new Vue({
  el: '#app',
  data: {
    message: 'Welcome to Vue.JS!',
  }
})
  ```
 - **Điều kiện**
Vue cung cấp cho chúng ta 1 tính năng khá là hữu dụng như là khả năng binding data tới view theo điều kiện. 

   - Example:

```javascript
new Vue({
  el: '#app',
  data: {
    message: 'Welcome to Vue.JS!',
    // điều kiện
    newMember: true
  }
})
 ```
 ```html
<div id="app">
  <!-- Display chỉ khi newMember = true -->
  <h2 v-if="newMember">{{ message }}</h2>
  <!-- Display chỉ khi newMember = false -->
  <h2 v-else="newMember">Pick a Mentor</h2>
</div>
 ```
**v-if** và **v-else** được dùng cho việc display data theo điều kiện. Và về cách sử dụng thì như là if-else trong các ngôn ngữ lập trình.

- **Vòng Lặp**

Ngoài việc là thực hiện binding theo điều kiện thì Vue cũng có duyệt data theo mảng.
 ```html
<div id="app">
    <ol>
        <li v-for="mentor in mentors">{{mentor.fullname}}</li>
     </ol>
</div>
 ```
Câu lệnh điều hướng **v-for** ở trên tạo 1 biến **mentor** và sử dụng biến này để duyệt hết các phần tử trong array **mentor**.

```javascript
new Vue({
el: '#app',
data: {
  // Array of mentors
  mentors: [
    {id: "1", fullname: "Arup Rakshit"},
    {id: "2", fullname: "Mo Moadeli"},
    {id: "3", fullname: "Khaja Minhajuddin"},
    {id: "4", fullname: "bendozy"},
    {id: "5", fullname: "Massimo Frascati"},
    {id: "6", fullname: "Christian Nwamba"}
  ]
}
})
```
- **Two-Way Binding** trong Vue được sử dụng qua câu lệnh **v-model**. Điều này sẽ thể hiện rõ hơn qua ví dụ.

    - Example:

     ```html
    <div id="app">
        Add mentor:
        <input type="text" v-model="mentor">
         <p>Two-Way Binding Here: {{mentor}}</p>
    </div>
    ```
    ```javascript
    <script>
        new Vue({
            el: '#app',
            data: {
                mentor: ''
            }
        });
    </script>
    ```

- **Xử lí sự kiện** Trong các ứng dụng web thì việc xử lí các sự kiện rất là quan trọng. Gỉa sử như chúng ta cần collect mentor content và status.

  ```html
    <div id="app">
        <p>
            <input type="text" v-model="mentor">
        </p>
        <p>
            <button v-on:click="addMentor">Add Mentor</button>
            <ol>
                <li v-for="mentor1 in mentors">{{mentor1}}</li>
            </ol>
    </div>
    ```
     ```javascript
    <script>
        new Vue({
            el: '#app',
            data: {
                mentor: "",
                mentors: [
                ]
            },

            methods: {
                addMentor: function () {
                    if (this.mentor != "") {
                        this.mentors.push({ 
                            content: this.mentor,
                            status: false
                        })
                        this.mentor = ""
                    }
                }
            }
        })
    </script>
    ```
- **Compenents** là 1 trong những tính năng mạnh mẽ của Vue. Tính năng giúp chúng ta đóng gói các HTML element để tiện cho tái sử dụng trong codebase.
    - Example

```javascript
    // mentor-user component
Vue.component('mentor-user', {
    // acceptable props
    props: ['mentor'],
    // renderable templates
    template: '<li>{{mentor.fullname}}</li>'
});
```

#### 2. 






#### 3. Các tính năng cơ bản
  
- `$scope`  là đối tượng có nhiệm vụ giao tiếp giữa controller và view của ứng dụng.

Cách dùng
```javascript
<div ng-app="myApp" ng-controller="myCtrl">

<input ng-model="name">

<h1>My name is {{name}}</h1>

</div>

<script>
var app = angular.module('myApp', []);

app.controller('myCtrl', function($scope) {
    $scope.name = "John Doe";
});
</script>
```
- `Controller`  xử lí dữ liệu cho đối tượng **$scope**, từ đây bên views sẽ sử dụng các dữ liệu trong scope để hiển thị ra tương ứng.

Cách dùng
```javascript
<div ng-app="myApp" ng-controller="myCtrl">

First Name: <input type="text" ng-model="firstName"><br>
Last Name: <input type="text" ng-model="lastName"><br>
<br>
Full Name: {{firstName + " " + lastName}}

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstName = "John";
    $scope.lastName = "Doe";
});
</script>
```
- `Data-binding`  tự động đồng bộ dữ liệu giữa model và view

Cách dùng
```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstname = "John";
    $scope.lastname = "Doe";
});
```
- `Data-binding`  tự động đồng bộ dữ liệu giữa model và view

Cách dùng
```javascript
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.firstname = "John";
    $scope.lastname = "Doe";
});
```
- `ng-click`  sự kiện xảy ra khi click chuột

Cách dùng
```javascript
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body ng-app="">

<p>Click the button:</p>

<button ng-click="count = count + 1" ng-init="count=0">OK</button>

<p>The button has been clicked {{count}} times.</p>

</body>
</html>
```

- `ng-chage`  thay đổi theo sự kiện mà người dùng chọn.

Cách dùng
```javascript
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body ng-app="myApp">
<div ng-controller="myCtrl">
  <p>Write something in the input field:</p>
  <input type="text" ng-change="myFunc()" ng-model="myValue" />
  <p>The input field has changed {{count}} times.</p>
</div>

<script>
  angular.module('myApp', [])
    .controller('myCtrl', ['$scope', function($scope) {
      $scope.count = 0;
      $scope.myFunc = function() {
        $scope.count++;
      };
    }]);
</script>
</body>
</html>
```

- `ng-style`  css cho thẻ được chọn mà không cần phải viết vào location write CSS

Cách dùng
```javascript
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>

<body ng-app="myApp" ng-controller="myCtrl">

<h1 ng-style="myObj">Welcome</h1>

<script>
var app = angular.module("myApp", []);
app.controller("myCtrl", function($scope) {
  $scope.myObj = {
    "color" : "white",
    "background-color" : "coral",
    "font-size" : "60px",
    "padding" : "50px"
  }
});
</script>

</body>
</html>
```

- `Filter`  Lọc các tập con từ tập item trong các mảng và trả về các mảng mới.

Cách dùng
```javascript
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body>

<div ng-app="myApp" ng-controller="namesCtrl">

<ul>
  <li ng-repeat="x in names | filter : 'i'">
    {{ x }}
  </li>
</ul>

</div>

<script>
angular.module('myApp', []).controller('namesCtrl', function($scope) {
    $scope.names = [
        'Jani',
        'Carl',
        'Margareth',
        'Hege',
        'Joe',
        'Gustav',
        'Birgit',
        'Mary',
        'Kai'
    ];
});
</script>

<p>This example displays only the names containing the letter "i".</p>

</body>
</html>
```
- `Directive`  dùng để tạo các thẻ HTML riêng phục vụ những mục đích riêng. AngularJS có những directive có sẵn như **ngBind**, **ngModel**…

Cách dùng
```javascript
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body>

<div ng-app="" ng-init="quantity=1;price=5">

<h2>Cost Calculator</h2>

Quantity: <input type="number" ng-model="quantity">
Price: <input type="number" ng-model="price">

<p><b>Total in dollar:</b> {{quantity * price}}</p>

</div>

</body>
</html>
```
- `Routing`  chuyển đổi giữa các action trong controller, qua lại giữa các view.

Cách dùng
```javascript
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular-route.js"></script>

<body ng-app="myApp">

<p><a href="#/!">Main</a></p>

<a href="#!red">Red</a>
<a href="#!green">Green</a>
<a href="#!blue">Blue</a>

<div ng-view></div>

<script>
var app = angular.module("myApp", ["ngRoute"]);
app.config(function($routeProvider) {
    $routeProvider
    .when("/", {
        templateUrl : "main.htm"
    })
    .when("/red", {
        templateUrl : "red.htm"
    })
    .when("/green", {
        templateUrl : "green.htm"
    })
    .when("/blue", {
        templateUrl : "blue.htm"
    });
});
</script>
    <p>Click on the "red.htm", "green.htm", "blue.htm"</p>
</body>
</html>
```
- `MVC` : mô hình thiết kế để phân chia các ứng dụng thành nhiều phần khác nhau (gọi là Model, View và Controller) mỗi phần có một nhiệm vụ nhất định. AngularJS không triển khai MVC theo cách truyền thống, mà gắn liền hơn với Model-View-ViewModel.

#### 4.Các components chính
 - **ng-app** : định nghĩa và liên kết một ứng dụng AngularJS tới HTML.
 - **ng-model** : gắn kết giá trị của dữ liệu ứng dụng AngularJS đến các điều khiển đầu vào HTML.
 - **ng-bind** : gắn kết dữ liệu ứng dụng AngularJS đến các thẻ HTML.
#### 5. Ưu điểm của angularJS
Cung cấp khả năng tạo ra các Single Page Aplication dễ dàng.
Cung cấp khả năng data binding tới HTML, khiến cho người dùng cảm giác linh hoạt, thân thiện.
Dễ dàng Unit test
Dễ dàng tái sử dụng các thành phần (Component)
Giúp lập trình viên viết code ít hơn với nhiều chức năng hơn.
Chạy được trên các loại trình duyệt, trên cả PC lẫn mobile.
#### 6. Nhược điểm
Không an toàn : được phát triển từ javascript cho nên ứng dụng được viết bởi AngularJS không an toàn. Nên có sự bảo mật và xác thực phía server sẽ giúp ứng dụng trở nên an toàn hơn.
Nếu người sử dụng ứng dụng của vô hiệu hóa JavaScript thì sẽ chỉ nhìn thấy trang cơ bản.
Phần giới thiệu về Angular JS của mình đến đây là kết thúc. Ở phần tiếp theo mình sẽ nói về Directive trong AngularJS.

### II. Sử dụng AngularJS bằng tool
Cách cài đặt như sau:
 - Bước 1: Tạo 1 folder bất kỳ ngoài màn hình desktop.
 - Bước 2: Mở folder vừa mới tạo, và chạy lệnh cmd.
 - Bước 3: Cài đặt yeoman angularjs băng lệnh sau: 
    **npm install -g grunt-cli bower yo generator-karma generator-angular**

    - Chạy:
    
    ![alt text](img-mark-down/chay.png "Logo Title Text 1")
    - Kết quả:

    ![alt text](img-mark-down/xong.PNG "Logo Title Text 1")

 - Bước 4: chạy lệnh **yo angular** để tải thư viện yo angular về folder của mình.

 ![alt text](img-mark-down/welcome.PNG "Logo Title Text 1")

  - Bước 5: Để cài nhanh ko cài  Sass,Bootstrap,.. nhấn **n** và **enter** và hết lựa chon y/n ... nhấn enter 

      - Quá trình cài đặt bắt đầu:

      ![alt text](img-mark-down/loading.PNG "Logo Title Text 1")

      - Thành công:

      ![alt text](img-mark-down/tai-xong.PNG "Logo Title Text 1")
 
- Bước 6: Để chạy thử trên IDE... bật cửa sổ cmd từ folder vừa tạo ...gõ lệnh **grunt serve**
    - Kết quả:

    ![alt text](img-mark-down/run-test.PNG "Logo Title Text 1")
    
    - IDE Display: 

    ![alt text](img-mark-down/ide-display.PNG "Logo Title Text 1")

- Bước 7: Gỡ cài đặt: gõ lệnh **npm uninstall -g [generator-name]** vào cmd của folder đó.

### III. Sử dụng AngularJS thủ công:

Tạo project như bình thường và thêm 
```javascript 
<script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
```
 vào cặp thẻ 
 ```javascript 
 <head></head>
 ```
 và sử dụng syntax của AngularJS như bình thường.

### IV.	YÊU CẦU

Tự tìm hiểu về AngularJS và viết báo cáo những nội dung có liên quan

### V.	NỘP BÀI

- doc: Báo Cáo (README.md).
- Tạo Project trên Github và gửi Link cho người hướng dẫn:
