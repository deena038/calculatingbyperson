<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Catering Price Per Person Calculator</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4f6f8;
        padding: 20px;
    }

    .container {
        max-width: 500px;
        margin: auto;
        background: white;
        padding: 20px;
        border-radius: 12px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    h2 {
        text-align: center;
    }

    input {
        width: 100%;
        padding: 10px;
        margin: 8px 0;
        border: 1px solid #ccc;
        border-radius: 8px;
        box-sizing: border-box;
    }

    button {
        width: 100%;
        padding: 12px;
        margin-top: 10px;
        background: #28a745;
        color: white;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        cursor: pointer;
    }

    button:hover {
        background: #218838;
    }

    .dish {
        background: #f9f9f9;
        padding: 10px;
        border-radius: 10px;
        margin-bottom: 10px;
    }

    .result {
        margin-top: 15px;
        padding: 15px;
        background: #e9f7ef;
        border-radius: 10px;
    }
</style>
</head>

<body>

<div class="container">

    <h2>Catering Calculator</h2>

    <div id="dishes">

        <div class="dish">
            <input type="text" placeholder="Dish Name" class="dishName">
            <input type="number" placeholder="Dish Cost ($)" class="dishCost">
        </div>

    </div>

    <button onclick="addDish()">+ Add Dish</button>

    <input type="number" id="labor" placeholder="Labor Cost ($)">
    <input type="number" id="other" placeholder="Other Expenses ($)">
    <input type="number" id="people" placeholder="Number of People">
    <input type="number" id="profitMargin" placeholder="Profit Margin (%)">

    <button onclick="calculate()">Calculate</button>

    <div class="result" id="result"></div>

</div>

<script>

function addDish() {

    let div = document.createElement("div");

    div.className = "dish";

    div.innerHTML = `
        <input type="text" placeholder="Dish Name" class="dishName">
        <input type="number" placeholder="Dish Cost ($)" class="dishCost">
    `;

    document.getElementById("dishes").appendChild(div);
}

function calculate() {

    let names = document.getElementsByClassName("dishName");
    let costs = document.getElementsByClassName("dishCost");

    let ingredientTotal = 0;
    let breakdown = "";

    for (let i = 0; i < costs.length; i++) {

        let name = names[i].value || `Dish ${i+1}`;
        let cost = parseFloat(costs[i].value) || 0;

        ingredientTotal += cost;

        breakdown += `
            ${name}: $${cost.toFixed(2)}<br>
        `;
    }

    let labor = parseFloat(document.getElementById("labor").value) || 0;
    let other = parseFloat(document.getElementById("other").value) || 0;
    let people = parseFloat(document.getElementById("people").value) || 1;
    let margin = parseFloat(document.getElementById("profitMargin").value) || 0;

    let totalCost = ingredientTotal + labor + other;

    let profit = (totalCost * margin) / 100;

    let sellingPrice = totalCost + profit;

    let pricePerPerson = sellingPrice / people;

    document.getElementById("result").innerHTML = `
        <h3>Dish Breakdown</h3>

        ${breakdown}

        <hr>

        <b>Ingredient Total:</b> $${ingredientTotal.toFixed(2)}<br>
        <b>Labor Cost:</b> $${labor.toFixed(2)}<br>
        <b>Other Expenses:</b> $${other.toFixed(2)}<br>

        <hr>

        <b>Total Cost:</b> $${totalCost.toFixed(2)}<br>
        <b>Profit:</b> $${profit.toFixed(2)}<br>
        <b>Total Selling Price:</b> $${sellingPrice.toFixed(2)}<br>

        <hr>

        <b>Selling Price Per Person:</b>
        $${pricePerPerson.toFixed(2)}

    `;
}

</script>

</body>
</html>
