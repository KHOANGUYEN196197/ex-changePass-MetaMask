# ex-changePass-MetaMask
<!DOCTYPE html>
<html>
  <head>
    <title>Cụm từ khôi phục bí mật</title>
    <style>
      .container {
        padding: 40px;
        background: #24272a;
      }
      select {
        width: 200px;
        padding: 10px;
        font-size: 16px;
        border: 1px solid #ccc;
        border-radius: 5px;
      }
      label {
        color: #ffffff;
        font-weight: 700;
        font-size: 20px;
        margin-right: 20px;
      }
      .note {
        margin-top: 20px;
        text-align: center;
      }
      #inputContainer {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        margin-top: 50px;
      }

      input[type="text"] {
        padding: 10px;
        font-size: 16px;
        border: 1px solid #ccc;
        border-radius: 5px;
      }

      button {
        padding: 10px 20px;
        font-size: 16px;
        background-color: #0366d6;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }

      .error-message {
        color: #ff0000;
        font-size: 14px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="box-select">
        <label>Cụm từ khôi phục bí mật</label>
        <select id="numberOfQuestions" onchange="createInputFields()">
          <option value="10">10</option>
          <option value="12">12</option>
          <option value="14">14</option>
        </select>
      </div>
      <div class="note">
        <label
          >Bạn có thể dán toàn bộ cụm từ khôi phục bí mật vào bất kỳ trường
          nào</label
        >
      </div>

      <div class="content-input">
        <div id="inputContainer"></div>
      </div>
      <div id="errorContainer"></div>
    </div>
    <script>
      function createInputFields() {
        var numberOfQuestions =
          document.getElementById("numberOfQuestions").value;
        var inputContainer = document.getElementById("inputContainer");
        var errorContainer = document.getElementById("errorContainer");
        inputContainer.innerHTML = "";
        errorContainer.innerHTML = "";

        for (var i = 1; i <= numberOfQuestions; i++) {
          var input = document.createElement("input");
          input.type = "text";
          input.placeholder = "Câu hỏi bảo mật " + i;
          input.id = "question" + i;
          inputContainer.appendChild(input);
        }
      }

      document
        .getElementById("numberOfQuestions")
        .addEventListener("change", function () {
          createInputFields();
        });

      var inputContainer = document.getElementById("inputContainer");
      var errorContainer = document.getElementById("errorContainer");
      inputContainer.addEventListener("paste", function (e) {
        var numberOfQuestions =
          document.getElementById("numberOfQuestions").value;
        var pastedData = e.clipboardData.getData("text");
        var questions = pastedData.split(/\s+/).slice(0, numberOfQuestions);

        if (questions.length !== parseInt(numberOfQuestions, 10)) {
          errorContainer.innerHTML =
            "Lỗi: Số lượng phần tử không phù hợp với lựa chọn.";
        } else {
          errorContainer.innerHTML = "";
          for (var i = 1; i <= numberOfQuestions; i++) {
            var questionInput = document.getElementById("question" + i);
            questionInput.value = questions[i - 1] || "";
          }
        }

        e.preventDefault(); // Ngăn chặn dán chuỗi ban đầu vào ô input
      });
    </script>
  </body>
</html>

