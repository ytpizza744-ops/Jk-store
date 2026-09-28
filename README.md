<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>JK Store - Mobile Phones</title>

<style>
*{
    box-sizing:border-box;
    margin:0;
    padding:0;
}

body{
    font-family:Arial,sans-serif;
    background:#f5f5f5;
    color:#111;
}

header{
    background:#111827;
    color:white;
    padding:16px;
    position:sticky;
    top:0;
    z-index:10;
}

.nav{
    max-width:1100px;
    margin:auto;
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.logo{
    font-size:25px;
    font-weight:bold;
}

.cart{
    background:white;
    color:#111827;
    border:none;
    padding:10px 16px;
    border-radius:25px;
    font-weight:bold;
}

.hero{
    background:#111827;
    color:white;
    text-align:center;
    padding:45px 20px;
}

.hero h1{
    font-size:38px;
    margin-bottom:10px;
}

.hero p{
    color:#d1d5db;
}

.container{
    max-width:1100px;
    margin:30px auto;
    padding:0 15px;
}

.search{
    width:100%;
    padding:15px;
    border:1px solid #ddd;
    border-radius:12px;
    font-size:16px;
    margin-bottom:25px;
}

.products{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
    gap:20px;
}

.product{
    background:white;
    border-radius:15px;
    overflow:hidden;
    box-shadow:0 3px 12px #0001;
}

.phone{
    height:230px;
    background:#e9edf2;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:80px;
}

.details{
    padding:18px;
}

.details h2{
    font-size:20px;
    margin-bottom:8px;
}

.spec{
    color:#666;
    font-size:14px;
    line-height:1.6;
}

.price{
    font-size:23px;
    font-weight:bold;
    margin:15px 0;
}

.buy{
    width:100%;
    padding:13px;
    background:#111827;
    color:white;
    border:none;
    border-radius:10px;
    font-size:16px;
    font-weight:bold;
}

footer{
    text-align:center;
    padding:35px;
    color:#777;
}

.modal{
    display:none;
    position:fixed;
    inset:0;
    background:#0008;
    z-index:20;
    padding:20px;
}

.box{
    background:white;
    max-width:450px;
    margin:60px auto;
    padding:25px;
    border-radius:18px;
}

.close{
    float:right;
    border:none;
    background:#eee;
    padding:8px 12px;
    border-radius:50%;
}

input,textarea{
    width:100%;
    padding:13px;
    margin:8px 0 12px;
    border:1px solid #ddd;
    border-radius:9px;
    font-size:15px;
}

.order{
    background:#f3f4f6;
    padding:12px;
    border-radius:10px;
    margin:10px 0;
}
</style>
</head>

<body>

<header>
<div class="nav">
<div class="logo">📱 JK Store</div>

<button class="cart" onclick="openCart()">
🛒 Cart (<span id="count">0</span>)
</button>

</div>
</header>

<section class="hero">
<h1>JK Store</h1>
<p>Latest Mobile Phones at Great Prices</p>
</section>

<div class="container">

<input
class="search"
id="search"
placeholder="🔎 Search Mobile Phone..."
oninput="showProducts()"
>

<div class="products" id="products"></div>

</div>

<footer>
© 2026 JK Store | Mobile Phones
</footer>

<div class="modal" id="modal">

<div class="box">

<button class="close" onclick="closeModal()">✕</button>

<div id="modalContent"></div>

</div>

</div>

<script>

const products = [

{
id:1,
name:"JK Phone Pro",
price:24999,
spec:"8GB RAM • 128GB Storage • 5G"
},

{
id:2,
name:"JK Phone Max",
price:18999,
spec:"6GB RAM • 128GB Storage • 5G"
},

{
id:3,
name:"JK Phone Lite",
price:12999,
spec:"4GB RAM • 64GB Storage • 4G"
},

{
id:4,
name:"JK Phone Ultra",
price:29999,
spec:"12GB RAM • 256GB Storage • 5G"
}

];

let cart=[];

function money(number){

return "₹"+number.toLocaleString("en-IN");

}

function showProducts(){

let search=document
.getElementById("search")
.value
.toLowerCase();

let html="";

products
.filter(p=>p.name.toLowerCase().includes(search))
.forEach(p=>{

html+=`

<div class="product">

<div class="phone">
📱
</div>

<div class="details">

<h2>${p.name}</h2>

<div class="spec">
${p.spec}
</div>

<div class="price">
${money(p.price)}
</div>

<button class="buy"
onclick="addToCart(${p.id})">

Add to Cart

</button>

</div>

</div>

`;

});

document.getElementById("products").innerHTML=html;

}

function addToCart(id){

let product=products.find(p=>p.id===id);

cart.push(product);

document.getElementById("count").innerText=cart.length;

alert("Mobile cart mein add ho gaya!");

}

function openCart(){

let html="<h2>Your Cart</h2>";

if(cart.length===0){

html+="<p>Cart khaali hai.</p>";

}else{

let total=0;

cart.forEach((p,i)=>{

total+=p.price;

html+=`

<div class="order">

<b>${p.name}</b><br>

${money(p.price)}

</div>

`;

});

html+=`

<h3>Total: ${money(total)}</h3>

<br>

<button class="buy"
onclick="checkout()">

Checkout

</button>

`;

}

document.getElementById("modalContent").innerHTML=html;

document.getElementById("modal").style.display="block";

}

function checkout(){

document.getElementById("modalContent").innerHTML=`

<h2>Order Details</h2>

<input id="name" placeholder="Your Name">

<input id="phone"
placeholder="Mobile Number"
type="tel">

<textarea id="address"
placeholder="Full Address"></textarea>

<button class="buy"
onclick="sendOrder()">

📲 WhatsApp par Order Bhejo

</button>

`;

}

function sendOrder(){

let name=document.getElementById("name").value;

let phone=document.getElementById("phone").value;

let address=document.getElementById("address").value;

if(!name || !phone || !address){

alert("Please saari details bharo.");

return;

}

let message="JK STORE ORDER%0A%0A";

message+="Name: "+encodeURIComponent(name)+"%0A";

message+="Mobile: "+encodeURIComponent(phone)+"%0A";

message+="Address: "+encodeURIComponent(address)+"%0A%0A";

message+="Products:%0A";

cart.forEach(p=>{

message+=encodeURIComponent(p.name+" - "+money(p.price))+"%0A";

});

window.open(
"https://wa.me/919799413770?text="+message,
"_blank"
);

}

function closeModal(){

document.getElementById("modal").style.display="none";

}

showProducts();

</script>

</body>
</html>
