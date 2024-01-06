<head>
 
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  
  <link href="style.css" rel="stylesheet" type="text/css" />
  <script src="script.js"></script>
  
  <style>
    * {
      box-sizing: border-box;
      /*框線*/
      font-family: sans-serif;
      /*無襯線體*/
    }

    body {
      margin: 0;
      /*框線*/
      padding: 0;
      /*填充*/
      width: 100%;
      height: 100vh;
      display: flex;
      /*彈性*/
      justify-content: center;
      /*水平對齊*/
      align-items: center;
      /*垂直對齊*/
      background-color: #000000;
    }

    .container {
      width: 500px;
      height: 500px;
      display: grid;
      background-color: #000000;
      grid-gap: 5px;
      /*間隙*/
      grid-template-columns: 33% 33% 33%;
      /*水平空間*/
      grid-auto-rows: 33% 33% 33%;
      /*垂直空間*/
    }

    .card {
      position: relative;
      /*相對於自己原來應在的"位置"*/
      background-color: #000000;
      cursor: pointer;
      /*手型鼠標*/
    }

    .card::before {
      position: absolute;
      /*絕對位置*/
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      display: flex;
      /*彈性*/
      justify-content: center;
      /*水平對齊*/
      align-items: center;
      /*垂直對齊*/
      font-weight: bold;
      /*粗體字*/
      font-size: 8rem;
      animation: animate .6s linear;
      /*動畫*/
    }

    .card.x::before {
      content: "X";
      /*內容*/
    }

    .card.o::before {
      content: "O";
    }

    .card.x::before {
      background-color: #005757;
      color: #D0D0D0
    }

    .card.o::before {
      background-color: #007979;
      color: #4F4F4F
    }

    #d1 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
      /*陰影*/
    }

    #d2 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d3 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d4 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d5 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d6 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d7 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d8 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    #d9 {
      box-shadow: 0px 0px 0px inset red, 0px 0px 50px #A6FFFF;
    }

    .winner {
      display: flex;
      /*彈性*/
      flex-direction: column;
      /*彈性方向*/
      /*欄*/
      align-items: center;
      /*對齊項目*/
      justify-content: center;
      /*對齊內容*/
      position: fixed;
      /*固定定位*/
      width: 400px;
      height: 200px;
      padding: 20px 40px;
      /*填充*/
      background-color: #fff;
      font-size: 2rem;
      border-radius: 20px;
      /*圓角*/
      text-align: center;
      /*對齊*/
      animation: animate .5s linear;
      /*動畫*/
    }

    @keyframes animate {

      /*動畫*/
      from {
        opacity: 0;
        /*不透明度*/
      }

      to {
        opacity: 1;
      }
    }

    .winner button {
      margin-top: 20px;
      /*上邊界距*/
      width: 80px;
      height: 35px;
      line-height: 35px;
      /*間距*/
      padding: 0;
      /*填充*/
      border: 0;
      /*邊框*/
      outline: 0;
      /*輪廓*/
      border-radius: 20px;
      /*圓角*/
      cursor: pointer;
      /*手型鼠標*/
      color: #fff;
      background-color: #BF360C;
    }
  </style>
</head>

<body>

  <div class="container">
    <div class="card" data-index="1" id="d1"></div>
    <div class="card" data-index="2" id="d2"></div>
    <div class="card" data-index="3" id="d3"></div>
    <div class="card" data-index="4" id="d4"></div>
    <div class="card" data-index="5" id="d5"></div>
    <div class="card" data-index="6" id="d6"></div>
    <div class="card" data-index="7" id="d7"></div>
    <div class="card" data-index="8" id="d8"></div>
    <div class="card" data-index="9" id="d9"></div>

  </div>

</body>

<script>
  const cards = Array.from(document.querySelectorAll(".card"));   /*常數*//*陣列*/
  const winner = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [1, 5, 9], [3, 5, 7], [1, 4, 7], [2, 5, 8], [3, 6, 9]];
  let firstPlayer = [], secondPlayer = [], count = 0;
  /*******************************************************/
  function check(array) {
    let finalResult = false;   /*偽元素*/
    for (let item of winner) {
      let res = item.every(val => array.indexOf(val) !== -1);
      if (res) {
        finalResult = true;
        break;
      }
    }
    return finalResult;
  }
  /*******************************************************/
  function winnerpleyr(p) {
    const modal =   /*撐滿*/ document.createElement("div");   /*文件*/
    const player = document.createTextNode(p);
    const replay = document.createElement("button");
    modal.classList.add("winner");
    modal.appendChild(player);
    replay.appendChild(document.createTextNode("Replay"));

    replay.onclick = function () {rep()};
    modal.appendChild(replay);
    document.body.appendChild(modal);
  }
  /*******************************************************/
  function draw() {
    if (this.classList == "card") {
      count++;
      if (count % 2 !== 0) {
        this.classList.add("x");
        firstPlayer.push(Number(this.dataset.index));
        if (check(firstPlayer)) {
          winnerpleyr("⦙⦙⦙⦙⦙⦙⦙🏆 X⦙⦙⦙⦙⦙⦙⦙");
          return true;
        }
      } else {
        this.classList.add("o");
        secondPlayer.push(Number(this.dataset.index));
        if (check(secondPlayer)) {
          winnerpleyr("⦙⦙⦙⦙⦙⦙⦙🏆 O⦙⦙⦙⦙⦙⦙⦙");
          return true;
        }
      }
      if (count === 9) {
        winnerpleyr("⦙⦙⦙⦙⦙⦙⦙X🤝O⦙⦙⦙⦙⦙⦙⦙");
      }
    }
  }
  /*******************************************************/
  function rep() {
    const w = document.querySelector(".winner");

    firstPlayer = [];
    secondPlayer = [];
    count = 0;
    w.remove();
    [].forEach.call(cards, function (el) {
      el.classList.remove("x");
      el.classList.remove("o");
    });


  }


  /*******************************************************/
  cards.forEach(card => card.addEventListener("click", draw));   /*事件處理*/

</script>

</html>
