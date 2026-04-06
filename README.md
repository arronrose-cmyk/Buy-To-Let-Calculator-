# Buy-To-Let-Calculator-<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Property Deal Analyser</title>
<style>
body { font-family: Arial; background:#f4f4f4; padding:15px; }
.container {
  max-width: 420px;
  margin:auto;
  background:white;
  padding:15px;
  border-radius:12px;
}
input, button {
  width:100%;
  padding:10px;
  margin-top:8px;
}
button {
  background:#1e88e5;
  color:white;
  border:none;
  border-radius:8px;
}
.result {
  margin-top:15px;
  font-size:14px;
}
h3 { margin-top:20px; }
</style>
</head>

<body>
<div class="container">

<h2>Deal Analyser</h2>

<h3>Purchase</h3>
<input id="purchase" placeholder="Purchase Price (£)">
<input id="refurb" placeholder="Refurb Cost (£)">
<input id="fees" placeholder="Buying Costs (£)">

<h3>Finance</h3>
<input id="ltv" placeholder="Refinance LTV (%)" value="75">
<input id="rate" placeholder="Interest Rate (%)">
<input id="fee" placeholder="Mortgage Fee (%)" value="0">

<h3>End Value</h3>
<input id="gdv" placeholder="End Value (£)">

<h3>Rental</h3>
<input id="rent" placeholder="Monthly Rent (£)">
<input id="costs" placeholder="Monthly Costs (£)">

<h3>Investor</h3>
<input id="invest" placeholder="Investor Cash (£)">
<input id="return" placeholder="Investor Return (%)">

<h3>Stress Test</h3>
<input id="stress" placeholder="Stress Rate (%)" value="8">

<button onclick="calc()">Analyse Deal</button>

<div class="result" id="output"></div>

</div>

<script>
function calc() {

let purchase = +document.getElementById("purchase").value || 0;
let refurb = +document.getElementById("refurb").value || 0;
let fees = +document.getElementById("fees").value || 0;

let totalCost = purchase + refurb + fees;

let ltv = document.getElementById("ltv").value / 100;
let rate = document.getElementById("rate").value / 100;
let fee = document.getElementById("fee").value / 100;

let gdv = +document.getElementById("gdv").value || 0;

let loan = gdv * ltv;
let feeAmount = loan * fee;
let totalLoan = loan + feeAmount;

let monthlyInterest = totalLoan * rate / 12;

let rent = +document.getElementById("rent").value || 0;
let costs = +document.getElementById("costs").value || 0;

let profit = rent - costs - monthlyInterest;

let annualProfit = profit * 12;

let cashLeft = totalCost - loan;

let investor = +document.getElementById("invest").value || 0;
let investorReturn = (document.getElementById("return").value / 100) || 0;

let investorPay = investor * investorReturn;

let stressRate = document.getElementById("stress").value / 100;
let stressPayment = totalLoan * stressRate / 12;

let stressProfit = rent - costs - stressPayment;

document.getElementById("output").innerHTML =

"<b>--- DEAL SUMMARY ---</b><br>" +
"Total Invested: £" + totalCost.toFixed(0) + "<br>" +
"Refinance Loan: £" + loan.toFixed(0) + "<br>" +
"Cash Left In Deal: £" + cashLeft.toFixed(0) + "<br><br>" +

"<b>--- CASHFLOW ---</b><br>" +
"Monthly Payment: £" + monthlyInterest.toFixed(0) + "<br>" +
"Monthly Profit: £" + profit.toFixed(0) + "<br>" +
"Annual Profit: £" + annualProfit.toFixed(0) + "<br><br>" +

"<b>--- STRESS TEST ---</b><br>" +
"Stress Payment: £" + stressPayment.toFixed(0) + "<br>" +
"Stress Profit: £" + stressProfit.toFixed(0) + "<br><br>" +

"<b>--- INVESTOR ---</b><br>" +
"Investor Payback: £" + investorPay.toFixed(0) + "<br>";

}
</script>

</body>
</html>
