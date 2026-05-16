<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EmprendeControl PRO</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial, sans-serif;
}

body{
background:linear-gradient(to bottom,#f4f4f4,#ece3ff);
padding:20px;
color:#333;
}

header{
background:linear-gradient(135deg,#6a0dad,#8e44ec);
color:white;
padding:20px;
border-radius:15px;
text-align:center;
margin-bottom:20px;
box-shadow:0 4px 10px rgba(0,0,0,0.2);
}

header p{
margin-top:8px;
font-size:14px;
}

.logo-img{
width:120px;
margin-bottom:10px;
animation:flotar 3s ease-in-out infinite;
}

@keyframes flotar{
0%{transform:translateY(0px);}
50%{transform:translateY(-8px);}
100%{transform:translateY(0px);}
}

.container{
max-width:900px;
margin:auto;
}

.card{
background:white;
padding:20px;
border-radius:15px;
margin-bottom:20px;
box-shadow:0 4px 8px rgba(0,0,0,0.1);
}

.card h2{
margin-bottom:15px;
color:#6a0dad;
}

input, select{
width:100%;
padding:12px;
margin-bottom:12px;
border-radius:10px;
border:1px solid #ccc;
font-size:15px;
}

button{
width:100%;
padding:12px;
background:#6a0dad;
color:white;
border:none;
border-radius:10px;
font-size:16px;
cursor:pointer;
transition:0.3s;
}

button:hover{
background:#520b9e;
transform:scale(1.03);
}

.total-box{
text-align:center;
font-size:22px;
font-weight:bold;
color:#6a0dad;
}

#historial{
list-style:none;
}

#historial li{
background:#f9f9f9;
padding:15px;
border-radius:10px;
margin-bottom:10px;
border-left:6px solid #6a0dad;
}

.acciones{
margin-top:10px;
display:flex;
gap:10px;
}

.editar{
background:#ff9800;
}

.eliminar{
background:#e53935;
}

.vacio{
text-align:center;
color:gray;
padding:20px;
}

.grafico{
margin-top:15px;
background:#eee;
border-radius:10px;
overflow:hidden;
height:25px;
}

.barra{
height:100%;
background:#6a0dad;
text-align:center;
color:white;
line-height:25px;
}

footer{
text-align:center;
background:white;
padding:15px;
border-radius:15px;
box-shadow:0 4px 8px rgba(0,0,0,0.1);
margin-top:20px;
color:gray;
font-size:14px;
}

@media(max-width:600px){
body{
padding:10px;
}
}
</style>
</head>

<body>

<div class="container">

<header>
<img class="logo-img" src="https://cdn-icons-png.flaticon.com/512/3135/3135715.png" alt="logo">
<h1>📊 EmprendeControl PRO</h1>
<p>Organiza pedidos, ingresos y métodos de pago fácilmente</p>
</header>

<div class="card">
<h2>➕ Registrar Venta</h2>

<input type="text" id="cliente" placeholder="Nombre del cliente">

<input type="text" id="producto" placeholder="Producto o servicio">

<select id="categoria">
<option value="">Selecciona categoría</option>
<option>Comida</option>
<option>Ropa</option>
<option>Belleza</option>
<option>Tecnología</option>
<option>Otros</option>
</select>

<input type="number" id="monto" placeholder="Monto S/">

<select id="metodo">
<option value="">Método de pago</option>
<option>Tarjeta Crédito</option>
<option>Tarjeta Débito</option>
<option>Yape</option>
<option>Plin</option>
<option>Efectivo</option>
<option>Transferencia</option>
</select>

<button onclick="guardarVenta()">Guardar Venta</button>
</div>

<div class="card">
<h2>📈 Resumen General</h2>
<img src="https://cdn-icons-png.flaticon.com/512/2331/2331970.png" width="80" style="margin-bottom:10px;">
<div class="total-box">
Total Ingresos: S/ <span id="total">0</span>
</div>

<div class="grafico">
<div class="barra" id="barra">0%</div>
</div>
</div>

<div class="card">
<h2>🧾 Historial de Ventas</h2>
<ul id="historial"></ul>
</div>

<footer>
EmprendeControl PRO © 2026
</footer>

</div>

<script>
let ventas = JSON.parse(localStorage.getItem("ventas")) || [];
let editando = null;

function actualizarPantalla(){
const historial = document.getElementById("historial");
const totalTexto = document.getElementById("total");
const barra = document.getElementById("barra");

historial.innerHTML = "";

if(ventas.length === 0){
    historial.innerHTML = `
    <div class="vacio">
    No hay ventas registradas aún 📭
    </div>`;
}

let total = 0;

ventas.forEach((venta, index)=>{

    total += Number(venta.monto);

    historial.innerHTML += `
    <li>
    <strong>Cliente:</strong> ${venta.cliente}<br>
    <strong>Producto:</strong> ${venta.producto}<br>
    <strong>Categoría:</strong> ${venta.categoria}<br>
    <strong>Monto:</strong> S/ ${venta.monto}<br>
    <strong>Método:</strong> ${venta.metodo}<br>
    <strong>Fecha:</strong> ${venta.fecha}<br>

    <div class="acciones">
    <button class="editar" onclick="editarVenta(${index})">Editar</button>
    <button class="eliminar" onclick="eliminarVenta(${index})">Eliminar</button>
    </div>
    </li>
    `;
});

localStorage.setItem("ventas", JSON.stringify(ventas));

const porcentaje = Math.min(total,1000)/10;

barra.style.width = porcentaje + "%";
barra.textContent = porcentaje.toFixed(0) + "%";

totalTexto.textContent = total.toFixed(2);
}

function guardarVenta(){

const cliente = document.getElementById("cliente").value;
const producto = document.getElementById("producto").value;
const categoria = document.getElementById("categoria").value;
const monto = document.getElementById("monto").value;
const metodo = document.getElementById("metodo").value;

if(cliente === "" || producto === "" || categoria === "" || monto === "" || metodo === ""){
alert("Completa todos los campos");
return;
}

const fecha = new Date().toLocaleString();

const nuevaVenta = {
cliente,
producto,
categoria,
monto,
metodo,
fecha
};

if(editando === null){
ventas.push(nuevaVenta);
}else{
ventas[editando] = nuevaVenta;
editando = null;
}

limpiarCampos();
actualizarPantalla();
}

function editarVenta(index){
const venta = ventas[index];

cliente.value = venta.cliente;
producto.value = venta.producto;
categoria.value = venta.categoria;
monto.value = venta.monto;
metodo.value = venta.metodo;

editando = index;
}

function eliminarVenta(index){
ventas.splice(index,1);
actualizarPantalla();
}

function limpiarCampos(){
cliente.value = "";
producto.value = "";
categoria.value = "";
monto.value = "";
metodo.value = "";
}

actualizarPantalla();
</script>

</body>
</html>
