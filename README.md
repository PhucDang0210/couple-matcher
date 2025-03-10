<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Ghé Cặp</title>
  <style>
    body {
      margin: 0;
      font-family: 'Comic Sans MS', cursive, sans-serif;
      background-color: #fce4ec;
    }
    .page {
      display: none;
      height: 100vh;
      background-size: cover;
      background-position: center;
      text-align: center;
      color: #ff66b2;
      padding-top: 100px;
    }
    .page.active {
      display: block;
    }
    input[type="text"], input[type="file"] {
      padding: 10px;
      width: 300px;
      margin-top: 10px;
      font-size: 16px;
      border: 2px solid #ff66b2;
      border-radius: 10px;
    }
    .warning {
      color: red;
      font-size: 14px;
      display: none;
    }
    .heart {
      font-size: 50px;
      color: red;
    }
    .button {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: #ff66b2;
      color: white;
      border: none;
      cursor: pointer;
      font-size: 16px;
      border-radius: 10px;
    }
    .button:hover {
      background-color: #d44b4f;
    }
    .back-button {
      background-color: #aaa;
    }
    .percentage {
      font-size: 30px;
      color: #ff66b2;
      margin-top: 20px;
    }
    .image-preview {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      margin: 20px;
      object-fit: cover;
    }
  </style>
</head>
<body>

  <!-- Trang 1: Nhập tên người bạn muốn ghép cặp -->
  <div class="page active" id="page1" style="background-image: url('https://cdn.pixabay.com/photo/2021/01/13/03/27/heart-5913128_960_720.png');">
    <h1>Nhập tên người bạn muốn ghép cặp!</h1>
    <input type="text" id="name1" placeholder="Nhập tên của người ấy...">
    <div class="warning" id="warning1">Hãy nhập tên của người ấy trước nhé!</div>
    <button class="button" onclick="goToPage2()">Tiếp tục</button>
  </div>

  <!-- Trang 2: Cung cấp ảnh của người ấy -->
  <div class="page" id="page2" style="background-image: url('https://cdn.pixabay.com/photo/2021/01/13/03/27/heart-5913128_960_720.png');">
    <h1>Cung cấp ảnh của bạn</h1>
    <input type="file" id="image1" accept="image/*" onchange="previewImage('image1', 'preview1')">
    <div class="warning" id="warning2">Hãy cho tôi biết ảnh của người ấy!</div>
    <img id="preview1" class="image-preview" src="" alt="Ảnh người ấy">
    <button class="button" onclick="goToPage3()">Tiếp tục</button>
  </div>

  <!-- Trang 3: Nhập tên của bạn -->
  <div class="page" id="page3" style="background-image: url('https://cdn.pixabay.com/photo/2021/01/13/03/27/heart-5913128_960_720.png');">
    <h1>Nhập tên của bạn!</h1>
    <input type="text" id="name2" placeholder="Nhập tên của bạn...">
    <div class="warning" id="warning3">Hãy nhập tên của bạn trước nhé!</div>
    <button class="button" onclick="goToPage4()">Tiếp tục</button>
  </div>

  <!-- Trang 4: Cung cấp ảnh của bạn -->
  <div class="page" id="page4" style="background-image: url('https://cdn.pixabay.com/photo/2021/01/13/03/27/heart-5913128_960_720.png');">
    <h1>Cung cấp ảnh của bạn</h1>
    <input type="file" id="image2" accept="image/*" onchange="previewImage('image2', 'preview2')">
    <div class="warning" id="warning4">Hãy cho tôi biết ảnh của bạn!</div>
    <img id="preview2" class="image-preview" src="" alt="Ảnh của bạn">
    <button class="button" onclick="showResult()">Tiếp tục</button>
  </div>

  <!-- Trang 5: Kết quả ghép cặp -->
  <div class="page" id="page5" style="background-image: url('https://cdn.pixabay.com/photo/2021/01/13/03/27/heart-5913128_960_720.png');">
    <div style="display: flex; justify-content: center; align-items: center;">
      <img id="finalImage1" class="image-preview" src="" alt="Ảnh người 1">
      <div style="text-align: center; padding: 20px;">
        <div class="heart">❤️</div>
        <h2 id="matchText">1% hợp nhau</h2>
        <p id="person1"></p>
        <p id="person2"></p>
      </div>
      <img id="finalImage2" class="image-preview" src="" alt="Ảnh người 2">
    </div>
    <button class="button back-button" onclick="goBack()">Quay lại</button>
  </div>

  <script>
    function goToPage2() {
      const name1 = document.getElementById("name1").value;
      if (name1.trim() === "") {
        document.getElementById("warning1").style.display = "block";
      } else {
        document.getElementById("warning1").style.display = "none";
        document.getElementById("page1").classList.remove("active");
        document.getElementById("page2").classList.add("active");
      }
    }

    function goToPage3() {
      const image1 = document.getElementById("image1").files.length;
      if (image1 === 0) {
        document.getElementById("warning2").style.display = "block";
      } else {
        document.getElementById("warning2").style.display = "none";
        document.getElementById("page2").classList.remove("active");
        document.getElementById("page3").classList.add("active");
      }
    }

    function goToPage4() {
      const name2 = document.getElementById("name2").value;
      if (name2.trim() === "") {
        document.getElementById("warning3").style.display = "block";
      } else {
        document.getElementById("warning3").style.display = "none";
        document.getElementById("page3").classList.remove("active");
        document.getElementById("page4").classList.add("active");
      }
    }

    function showResult() {
      const image2 = document.getElementById("image2").files.length;
      if (image2 === 0) {
        document.getElementById("warning4").style.display = "block";
      } else {
        document.getElementById("warning4").style.display = "none";
        document.getElementById("page4").classList.remove("active");
        document.getElementById("page5").classList.add("active");

        const name1 = document.getElementById("name1").value;
        const name2 = document.getElementById("name2").value;
        document.getElementById("person1").textContent = "Tên người bạn muốn ghép cặp: " + name1;
        document.getElementById("person2").textContent = "Tên của bạn: " + name2;

        // Hiển thị ảnh đã tải lên ở trang cuối
        const image1Src = URL.createObjectURL(document.getElementById("image1").files[0]);
        const image2Src = URL.createObjectURL(document.getElementById("image2").files[0]);
        document.getElementById("finalImage1").src = image1Src;
        document.getElementById("finalImage2").src = image2Src;

        // Kiểm tra cặp "Vũ Ngọc Khánh Ngân" và "Đặng Trọng Phúc"
        if ((name1 === "Vũ Ngọc Khánh Ngân" && name2 === "Đặng Trọng Phúc") || 
            (name1 === "Đặng Trọng Phúc" && name2 === "Vũ Ngọc Khánh Ngân")) {
          const percentage = 100;
          animatePercentage(percentage); // Hiển thị 100% với hiệu ứng tăng dần
        } else {
          let percentage = 1;
          const randomPercentage = Math.floor(Math.random() * (100 - 1 + 1)) + 1; // Tỷ lệ ngẫu nhiên từ 1% đến 100%
          animatePercentage(randomPercentage);
        }
      }
    }

    function animatePercentage(targetPercentage) {
      const percentageElement = document.getElementById("matchText");
      let currentPercentage = 0;

      const interval = setInterval(function() {
        currentPercentage++;
        percentageElement.innerHTML = currentPercentage + "% hợp nhau";
        if (currentPercentage >= targetPercentage) {
          clearInterval(interval);
        }
      }, 50);  // Tăng dần mỗi 50ms
    }

    function goBack() {
      document.getElementById("page5").classList.remove("active");
      document.getElementById("page1").classList.add("active");
    }

    function previewImage(inputId, previewId) {
      const file = document.getElementById(inputId).files[0];
      const reader = new FileReader();
      reader.onloadend = function () {
        document.getElementById(previewId).src = reader.result;
      }
      if (file) {
        reader.readAsDataURL(file);
      }
    }
  </script>

</body>
</html>
