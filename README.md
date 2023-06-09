<!DOCTYPE html>
<html>
<head>
    <title>Billing System</title>
    <style>
        body {
            font-family: Monospace, sans-serif;
            background-color: #66ffff;
            margin: 0;
            padding: 20px;
           
        }

        h1 {
            text-align: center;
        }

        form {
            max-width: 400px;
            margin: 0 auto;
        }

        label {
            display: block;
            margin-bottom: 5px;
        }

        input[type="text"],
        input[type="tel"],
        input[type="number"] {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
            margin-bottom: 10px;
        }

        input[type="number"] {
            width: 50px;
        }

        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }

        .result {
            margin-top: 20px;
            border: 1px solid #ccc;
            padding: 10px;
        }
    </style>
    <script>
        function calculateTotal() {
            var items = {
                "Chicken Biryani 1kg": 0,
                "Chicken Biryani 1/2kg": 0,
                "Chicken Biryani 1/4kg": 0,
                "Kushka 1kg": 0,
                "Kushka 1/2kg": 0,
                "Kushka 1/4kg": 0,
                "Egg Biryani 1kg": 0,
                "Egg Biryani 1/2kg": 0,
                "Mutton Biryani 1kg": 0,
                "Mutton Biryani 1/2kg": 0,
                "Mutton Biryani 100g": 0
            };

            // Retrieve the quantities of each item
            for (var item in items) {
                items[item] = parseInt(document.getElementById(item.replace(/ /g, '')).value) || 0;
            }

            var total = 0;
            var orderedItems = "";

            // Calculate the total and create the ordered items string
            for (var item in items) {
                var quantity = items[item];
                if (quantity > 0) {
                    var amount = calculateAmount(item, quantity);
                    orderedItems += item + ": " + quantity + " - Amount: Rs" + amount.toFixed(2) + "<br>";
                    total += amount;
                }
            }

            // Display the ordered items and total
            document.getElementById("orderedItems").innerHTML = orderedItems;
            document.getElementById("totalAmount").innerHTML = "Total Amount: Rs" + total.toFixed(2);
        }

        function calculateAmount(item, quantity) {
            // Add your own logic to calculate the amount based on the item and quantity
            // This is just a placeholder
            var prices = {
                "Chicken Biryani 1kg": 200,
                "Chicken Biryani 1/2kg": 100,
                "Chicken Biryani 1/4kg": 50,
                "Kushka 1kg": 150,
                "Kushka 1/2kg": 90,
                "Kushka 1/4kg": 70,
                "Egg Biryani 1kg": 100,
                "Egg Biryani 1/2kg": 60,
                "Mutton Biryani 1kg": 300,
                "Mutton Biryani 1/2kg": 150,
                "Mutton Biryani 100g": 100
            };

            return prices[item] * quantity;
        }

        function generateBill() {
            var customerName = document.getElementById("customerName").value;
            var phoneNumber = document.getElementById("phoneNumber").value;
            var billNumber = document.getElementById("billNumber").value;
            var orderedItems = document.getElementById("orderedItems").innerHTML;
            var totalAmount = document.getElementById("totalAmount").innerHTML;

            var billDetails = "<strong>Customer Name:</strong> " + customerName + "<br>" +
                              "<strong>Phone Number:</strong> " + phoneNumber + "<br>" +
                              "<strong>Bill Number:</strong> " + billNumber + "<br><br>" +
                              "<strong>Ordered Items:</strong><br>" +
                              orderedItems + "<br>" +
                              "<strong>" + totalAmount + "</strong>";

            // Display the generated bill
            document.getElementById("billDetails").innerHTML = billDetails;
        }
    </script>
</head>
<body>
    <h1>Billing System</h1>

    <form>
        <label for="customerName">Customer Name:</label>
        <input type="text" id="customerName" required>

        <label for="phoneNumber">Phone Number:</label>
        <input type="tel" id="phoneNumber" required>

        <label for="billNumber">Bill Number:</label>
        <input type="text" id="billNumber" required><br><br>

        <label for="chickenBiryani1kg">Chicken Biryani 1kg:</label>
        <input type="number" id="ChickenBiryani1kg" min="0" value="0">

        <label for="chickenBiryani1/2kg">Chicken Biryani 1/2kg:</label>
        <input type="number" id="ChickenBiryani1/2kg" min="0" value="0">

        <label for="chickenBiryani1/4kg">Chicken Biryani 1/4kg:</label>
        <input type="number" id="ChickenBiryani1/4kg" min="0" value="0">

        <label for="kushka1kg">Kushka 1kg:</label>
        <input type="number" id="Kushka1kg" min="0" value="0">

        <label for="kushka1/2kg">Kushka 1/2kg:</label>
        <input type="number" id="Kushka1/2kg" min="0" value="0">

        <label for="kushka1/4kg">Kushka 1/4kg:</label>
        <input type="number" id="Kushka1/4kg" min="0" value="0">

        <label for="eggBiryani1kg">Egg Biryani 1kg:</label>
        <input type="number" id="EggBiryani1kg" min="0" value="0">

        <label for="eggBiryani1/2kg">Egg Biryani 1/2kg:</label>
        <input type="number" id="EggBiryani1/2kg" min="0" value="0">

        <label for="muttonBiryani1kg">Mutton Biryani 1kg:</label>
        <input type="number" id="MuttonBiryani1kg" min="0" value="0">

        <label for="muttonBiryani1/2kg">Mutton Biryani 1/2kg:</label>
        <input type="number" id="MuttonBiryani1/2kg" min="0" value="0">

        <label for="muttonBiryani100g">Mutton Biryani 100g:</label>
        <input type="number" id="MuttonBiryani100g" min="0" value="0">

        <br><br>

        <button type="button" onclick="calculateTotal()">Calculate Total</button>
        <button type="button" onclick="generateBill()">Generate Bill</button>

        <br><br>

        <div class="result">
            <h3>Ordered Items:</h3>
            <div id="orderedItems"></div>
            <div id="totalAmount"></div>
        </div>

        <br><br>

        <div id="billDetails"></div>
    </form>
</body>
</html>
