#### 1.基于Jquery的Ajax用法

* $.get()方法  :  从服务器当中获取所需要的数据

  ```js
  <body>
      <div>Ajax基本使用</div>
      <div id="info">默认信息</div>
      <button id="btn">点击</button>
  </body>
  <script src="js/jquery.js"></script>
  <script>
      //get方法:从浏览器获取数据           post方法:给浏览器数据
      $('#btn').click(function () {
          $.get('http://www.liulongbin.top:3006/api/getbooks', function (res) {
              $('#info').html(res.msg);
          })
      })
  
  
      //get方法的两个参数.  1.第一个参数是要获取数据的服务器的地址   2.第二个参数是回调函数,回调函数当中的形参是从服务器所获取到的数据.
  </script>
  ```







* $.get()方法的传参1

  ```js
  <body>
      <div>Ajax基本使用</div>
      <div id="info">默认信息</div>
      <button id="btn">点击</button>
  </body>
  <script src="js/jquery.js"></script>
  <script>
      $('#btn').click(function () {
          $.get('http://www.liulongbin.top:3006/api/getbooks?id=1&bookname=西游记', function (res) {
              console.log(res);
              $('#info').html(res.msg);
          })
      })
  
      //第一种参数的传递(?id=1&bookname=西游记'),直接在url地址末尾这样写,筛选所需要的数据.res是所筛选出来的数据
  ```







* $.get()方法的传参2

  ```js
  <body>
      <div>Ajax基本使用</div>
      <div id="info">默认信息</div>
      <button id="btn">点击</button>
  </body>
  <script src="js/jquery.js"></script>
  <script>
      $('#btn').click(function () {
          $.get('http://www.liulongbin.top:3006/api/getbooks', {
              id: 1,
              bookname: '西游记'
          }, function (res) {
              console.log(res);
              $('#info').html(res.msg);
          })
      })
      //第二种传参,在第一个参数和第二个参数之间加上一个对象.在对象当中进行参数的传递.res是我们通过参数所筛选出来的数据
  ```

  





* $.post()方法 : 给服务器数据

  ```js
  <body>
      <div>Ajax基本使用</div>
      <div id="info">默认信息</div>
      <button id="btn">点击</button>
  </body>
  <script src="js/jquery.js"></script>
  <script>
      $('#btn').click(function () {
          $.post('http://www.liulongbin.top:3006/api/addbook', {
              id: "5",
              bookname: "爱你",
              author: "嘟嘟嘟",
              publisher: "北京图书出版社"
          }, function (res) {
              console.log(res);
              $('#info').html(res.msg);
          })
      })
  
      //$.post()方法的三个参数,第一个是服务器的地址,第二个参数是一个对象,表示要给服务器的数据,第三个参数是成功获取服务器的回调函数,res是成功从服务器返回的数据.
  </script>
  ```

  





* $.ajax()方法   jquery通用请求方法

  

  - 使用$.ajax()方法来写get请求

    ```js
    <body>
        <div>Ajax基本使用</div>
        <div id="info">默认信息</div>
        <button id="btn">点击</button>
    </body>
    <script src="js/jquery.js"></script>
    <script>
        $('#btn').click(function () {
            $.ajax({
                type: 'get',
                url: 'http://www.liulongbin.top:3006/api/getbooks',
                data: {
                    id: 1,
                    bookname: '西游记'
                },
                //其实在使用get()方法时,使用对象的方法来进行参数的传递,参数会被自动拼接到url地址的后面
                success: function (res) {
                    console.log(res);
                    $('#info').html(res.msg);
                }
            })
        })
    
        //记住$.ajax()方法中type,url,data,success这四个关键词
    </script>
    ```

  

  

  

  

  - 使用$.ajax()方法来写post请求

    ```js
    $('#btn').click(function () {
            $.ajax({
                type: 'post',
                url: 'http://www.liulongbin.top:3006/api/addbooks',
                data: {
                    bookname: '西游记',
                    author: '吴承恩',
                    publisher: '出版社'
                },
                //data中是要提交给服务器的数据,数据前面的属性名是根据后端数据来的,不能自己随意书写
                success: function (res) {
                    console.log(res);
                    $('#info').html(res.msg);
                }
            })
        })
    ```

    







* 什么是接口?
  - 之前的接口指的是API(应用程序编程接口),本质上就是方法.
  - 对于ajax来说,接口指的是url地址.调用接口就是在调用url地址.







* 图书管理案例    (展示,添加,修改)

  ```js
  <body>
      <!-- 添加图书的Panel面板 -->
      <div class="panel panel-primary">
          <div class="panel-heading">
              <h3 class="panel-title">添加新图书</h3>
          </div>
          <div class="panel-body form-inline">
              <!-- 表单输入域 -->
              <div class="input-group">
                  <div class="input-group-addon">图书名称</div>
                  <input type="text" class="form-control" id="bookname" placeholder="请输入图书名称">
              </div>
              <div class="input-group">
                  <div class="input-group-addon">图书作者</div>
                  <input type="text" class="form-control" id="author" placeholder="请输入图书作者">
              </div>
              <div class="input-group">
                  <div class="input-group-addon">图书出版社</div>
                  <input type="text" class="form-control" id="publisher" placeholder="请输入图书出版社">
              </div>
              <button id="addForm" type="button" class="btn btn-primary">提交</button>
          </div>
      </div>
      <!-- 图书的表格 -->
      <table class="table table-bordered table-hover">
          <thead>
              <tr>
                  <th>图书名称</th>
                  <th>图书作者</th>
                  <th>图书出版社</th>
                  <th>操作</th>
              </tr>
          </thead>
          <tbody></tbody>
      </table>
  </body>
  
  
  <script type="text/javascript" src="./js/jquery.js"></script>
  <script>
      //第一步:数据的展示
      function load() {
          $.get('http://www.liulongbin.top:3006/api/getbooks', function (res) {
              if (res.status === 200) { //bug出现处,忘写res.这一步通过状态码来证明已经正确拿到服务器当中的数据了,之后才能继续后续的操作,这一步不能忘记
                  var arr = res.data;
                  var str = '';
                  $.each(arr, function (index, item) {
                      str += `
                      <tr>
                          <td>${item.bookname}</td>
                          <td>${item.author}</td>
                          <td>${item.publisher}</td>
                          <td><a href="javascript:;" data-id = '${item.id}'>删除</a></td>
                      </tr>
                      `;
                  });
                  $('tbody').html(str)
              } else {
                  alert(res.msg)
              }
          })
      }
      load();
      //这是对数据进行展示
  
  
      $('#addForm').click(function () {
          var bookname = $('#bookname').val();
          var author = $('#author').val();
          var publisher = $('#publisher').val();
  
          if (!bookname || !author || !publisher) {
              alert('请输入完整信息');
              return;
          }
  
  
          $.post('http://www.liulongbin.top:3006/api/addbook', {
              bookname: bookname,
              author: author,
              publisher: publisher
          }, function (res) {
              if (res.status === 201) {
                  load();
                  $('#bookname').val('');
                  $('#author').val('');
                  $('#publisher').val('');
              } else {
                  alert(res.msg);
              }
          })
      })
  
      //这是对数据进行添加功能
  
      $('.table tbody').on('click', 'a', function (e) {
          var index = e.target.dataset.id;
          $.get('http://www.liulongbin.top:3006/api/delbook', {
              id: index
          }, function (res) {
              if (res.status === 200) {
                  load();
              } else {
                  alert(res.status)
              }
          })
      })
      //这是数据的删除功能
  </script>
  ```















* 数组的一些方法

  

  

  - forEach()

    ```js
    var arr = ['tom', 'jerry', 'spike'];
    arr.forEach(function (item, index) {
        //注意item和index的前后位置,和$.each()相反(index,item)
        //forEach()循环数组一旦开始,循环将无法终止
        console.log(item, index)
        })
    ```

  - some()和every()

    ```js
    var arr1 = [1, 3, 5, 8, 10]
        //arr1.some方法作用：判断数组中是否包含符合条件的数据，只要有一个就返回true，否则返回false
        var flag = arr1.some(function (item) {
          return item > 5
        })
    
        
        //arr1.every方法作用：判断数组中是否包含符合条件的数据，只有所有的条件都满足才返回true，否则返回false
        var flag = arr1.every(function (item) {
          return item > 1
        })
        console.log(flag)
       // ---------------------------------------------
        var flag = false
        arr1.some(function (item) {
          if (item > 2) {
            flag = true
            // 终止循环的方式：返回true
            return true
            //some()方法也可以对数组进行遍历,这是终止some()遍历的方法
          }
        })
    ```

    





