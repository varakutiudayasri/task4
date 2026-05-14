<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Task 4 Project</title>

  <style>
    *{
      margin:0;
      padding:0;
      box-sizing:border-box;
      font-family:Arial, sans-serif;
    }

    body{
      background:#f4f4f4;
      color:#333;
    }

    header{
      background:#222;
      color:white;
      padding:15px 30px;
      display:flex;
      justify-content:space-between;
      align-items:center;
    }

    nav a{
      color:white;
      text-decoration:none;
      margin-left:20px;
    }

    section{
      padding:40px 20px;
    }

    .hero{
      text-align:center;
      padding:60px 20px;
      background:white;
    }

    .hero h1{
      font-size:40px;
      margin-bottom:10px;
    }

    .projects{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
      gap:20px;
      margin-top:20px;
    }

    .card{
      background:white;
      padding:20px;
      border-radius:10px;
      box-shadow:0 2px 8px rgba(0,0,0,0.1);
    }

    /* TO DO */

    .todo-container{
      background:white;
      padding:20px;
      border-radius:10px;
      max-width:500px;
      margin:auto;
    }

    .todo-container input{
      width:70%;
      padding:10px;
    }

    .todo-container button{
      padding:10px 15px;
      cursor:pointer;
    }

    ul{
      list-style:none;
      margin-top:20px;
    }

    li{
      background:#eee;
      padding:10px;
      margin-bottom:10px;
      display:flex;
      justify-content:space-between;
      border-radius:5px;
    }

    /* PRODUCTS */

    .controls{
      margin-bottom:20px;
      display:flex;
      gap:10px;
      flex-wrap:wrap;
    }

    .product-list{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
      gap:20px;
    }

    .product{
      background:white;
      padding:20px;
      border-radius:10px;
      box-shadow:0 2px 8px rgba(0,0,0,0.1);
    }

    footer{
      text-align:center;
      padding:20px;
      background:#222;
      color:white;
      margin-top:40px;
    }

    @media(max-width:600px){
      header{
        flex-direction:column;
      }

      nav{
        margin-top:10px;
      }
    }
  </style>
</head>

<body>

  <header>
    <h2>My Portfolio</h2>

  <nav>
      <a href="#about">About</a>
      <a href="#todo">To-Do</a>
      <a href="#products">Products</a>
    </nav>
  </header>
  <!-- HERO -->

  <section class="hero">
    <h1>Varakuti Udaya Sri</h1>
    <p>Web Developer | Student</p>
  </section>

  <!-- ABOUT -->

  <section id="about">
    <h2>About Me</h2>

  <div class="projects">

  <div class="card">
        <h3>HTML & CSS</h3>
        <p>Responsive web design using modern layouts.</p>
      </div>

  <div class="card">
        <h3>JavaScript</h3>
        <p>Interactive websites with DOM manipulation.</p>
      </div>

  <div class="card">
        <h3>Projects</h3>
        <p>Quiz App, Portfolio, To-Do App and Product Page.</p>
      </div>

  </div>
  </section>
  
  <!-- TODO APP -->

  <section id="todo">
    <h2 style="text-align:center; margin-bottom:20px;">To-Do List</h2>

  <div class="todo-container">

  <input type="text" id="taskInput" placeholder="Enter task">
      <button onclick="addTask()">Add</button>

  <ul id="taskList"></ul>

  </div>
  </section>

  <!-- PRODUCT PAGE -->

  <section id="products">
    <h2 style="text-align:center; margin-bottom:20px;">Products</h2>

   <div class="controls">
      <select id="filter" onchange="displayProducts()">
        <option value="All">All Categories</option>
        <option value="Electronics">Electronics</option>
        <option value="Fashion">Fashion</option>
      </select>

  <select id="sort" onchange="displayProducts()">
        <option value="default">Sort By</option>
        <option value="low">Price Low-High</option>
        <option value="high">Price High-Low</option>
      </select>
    </div>

  <div class="product-list" id="productList"></div>

  </section>

  <footer>
    <p>© 2026 My Portfolio Project</p>
  </footer>

  <script>

    // TODO APP

    let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

    function saveTasks(){
      localStorage.setItem("tasks", JSON.stringify(tasks));
    }

    function renderTasks(){

      const taskList = document.getElementById("taskList");
      taskList.innerHTML = "";

      tasks.forEach((task, index) => {

        taskList.innerHTML += `
          <li>
            ${task}
            <button onclick="deleteTask(${index})">Delete</button>
          </li>
        `;
      });
    }

    function addTask(){

      const input = document.getElementById("taskInput");

      if(input.value.trim() === ""){
        alert("Enter a task");
        return;
      }

      tasks.push(input.value);

      saveTasks();
      renderTasks();

      input.value = "";
    }

    function deleteTask(index){

      tasks.splice(index, 1);

      saveTasks();
      renderTasks();
    }

    renderTasks();

    // PRODUCT PAGE

    const products = [
      {
        name:"Headphones",
        category:"Electronics",
        price:1500
      },

      {
        name:"Smart Watch",
        category:"Electronics",
        price:3000
      },

      {
        name:"T-Shirt",
        category:"Fashion",
        price:700
      },

      {
        name:"Shoes",
        category:"Fashion",
        price:1200
      }
    ];

    function displayProducts(){

      const filter = document.getElementById("filter").value;
      const sort = document.getElementById("sort").value;

      let filtered = [...products];

      if(filter !== "All"){
        filtered = filtered.filter(
          product => product.category === filter
        );
      }

      if(sort === "low"){
        filtered.sort((a,b) => a.price - b.price);
      }

      if(sort === "high"){
        filtered.sort((a,b) => b.price - a.price);
      }

      const productList = document.getElementById("productList");

      productList.innerHTML = "";

      filtered.forEach(product => {

        productList.innerHTML += `
          <div class="product">
            <h3>${product.name}</h3>
            <p>Category: ${product.category}</p>
            <p>Price: ₹${product.price}</p>
          </div>
        `;
      });
    }

    displayProducts();

  </script>

</body>
</html>
