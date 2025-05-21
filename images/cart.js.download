let listProductHTML = document.querySelector('.listProduct');
let listmodalHTML = document.querySelector('.listmodal');
let listCartHTML = document.querySelector('.listCart');
let totalPrice = document.querySelector('#totalPrice');
let subtotal = document.querySelector('#subtotal');
let iconCart = document.querySelector('.icon-cart');
let iconCartSpan = document.querySelector('#icon-cart span');
let iconCarttSpan = document.querySelector('.icon-cartt span');
let body = document.querySelector('body');
let closeCart = document.querySelector('.close');
let products = [];
let cart = [];


// iconCart.addEventListener('click', () => {
//     body.classList.toggle('showCart');
// })
// closeCart.addEventListener('click', () => {
//     body.classList.toggle('showCart');
// })



    const addDataToHTML = () => {
    // remove datas default from HTML

        // add new datas
        if(products.length > 0) // if has data
        {
            products.forEach(product => {
                let newProduct = document.createElement('div');
                newProduct.dataset.id = product.id;
                newProduct.classList.add('item');
                newProduct.innerHTML = 
                
                `<div class="filterDiv ${product.Productname} " >
  <div class="card" id="card" style="width: 18rem; border:#fff;"  >
  <div id="hide-i"  >
  <div id="hide-icons" class="hide-icons" >
    <span id="heart" class="bicon"><i id="bi" class="bi bi-heart"></i></span>
    <span id="cmyBtn" class="bicon"><a href="shop.html" style="color:inherit;"><i id="bi" class="bi bi-search" data-bs-toggle="modal"
             data-bs-target="#modalsta" onclick=modal() style="cursor:pointer;"></i></a></span>
  
    <span id="cart" class="bicon"><i id="bi" class="bi bi-cart2" style="width:20px;"></i></span>
  </div>
                <img src="${product.image}" class="card-img-top" alt="..." style="height: 13rem;"></div> 
              <div class="card-body "style="background-color:none; padding:1px 5px;" >
                <h5 class="card-title text-uppercase " id="productnam" style="color:#bbb; ">${product.Productname}</h5>
                <p class="card-text " style="color:#666;">${product.Producttext}</p>
                <p class="price"  id="price"style="color:#bbb;">$${product.Price}</p>
     
                </div>  </div>
 </div>
 <button class="addCart w-100" id="addcart">Add To Cart</button>
 
 
  `;
                listProductHTML.appendChild(newProduct);
            });
        }
    }
   
    
   
    
    listProductHTML.addEventListener('click', (event) => {
        let positionClick = event.target;
        if(positionClick.classList.contains('addCart')){
            let id_product = positionClick.parentElement.dataset.id;
            addToCart(id_product);
        }
    })


const addToCart = (product_id) => {
    let positionThisProductInCart = cart.findIndex((value) => value.product_id == product_id);
    if(cart.length <= 0){
        cart = [{
            product_id: product_id,
            quantity: 1
        }];
    }else if(positionThisProductInCart < 0){
        cart.push({
            product_id: product_id,
            quantity: 1
        });
    }else{
        cart[positionThisProductInCart].quantity = cart[positionThisProductInCart].quantity + 1;
    }
    addCartToHTML();
    addCartToMemory();
}
const addCartToMemory = () => {
    localStorage.setItem('cart', JSON.stringify(cart));
}

const addCartToHTML = () => {
    listCartHTML.innerHTML = '';
    let totalQuantity = 0;
    if(cart.length > 0){
        cart.forEach(item => {
            totalQuantity = totalQuantity +  item.quantity;
            let newItem = document.createElement('li');
            newItem.classList.add('item');
            newItem.dataset.id = item.product_id;

            let positionProduct = products.findIndex((value) => value.id == item.product_id);
            let info = products[positionProduct];
            listCartHTML.appendChild(newItem);
            newItem.innerHTML = `
            <div class="colmn">
             <div class="image">
                    <img src="${info.image}" width="100px">
                </div>
               
                </div>
                <div class="colmn">
             <div class="name fs-6 text-uppercase">
                ${info.Productname}
                </div>
                <p class="fs-6">Black</p>
                <div  >Total: $<span class="totalPrice" id="totalPrice">${info.Price*item.quantity}<span></div> 
                </div>
                <div class="quantity"><br>
                    <span class="minus"> -</span>
                    <span style="background-color:#fff; color:#555; id="quantity">${item.quantity}</span>
                    <span class="plus">+</span>
                    </div>  <br><br>
            `;
        })
   

    }
 
    iconCartSpan.innerText = totalQuantity;
    iconCarttSpan.innerText = totalQuantity;
  
   
}


listCartHTML.addEventListener('click', (event) => {
    let positionClick = event.target;
    if(positionClick.classList.contains('minus') || positionClick.classList.contains('plus')){
        let product_id = positionClick.parentElement.parentElement.dataset.id;
        let type = 'minus';
        if(positionClick.classList.contains('plus')){
            type = 'plus';
        }
        changeQuantityCart(product_id, type);
    }
})
const changeQuantityCart = (product_id, type) => {
    let positionItemInCart = cart.findIndex((value) => value.product_id == product_id);
    if(positionItemInCart >= 0){
        let info = cart[positionItemInCart];
        switch (type) {
            case 'plus':
                cart[positionItemInCart].quantity = cart[positionItemInCart].quantity + 1;
                break;
        
            default:
                let changeQuantity = cart[positionItemInCart].quantity - 1;
                if (changeQuantity > 0) {
                    cart[positionItemInCart].quantity = changeQuantity;
                }else{
                    cart.splice(positionItemInCart, 1);
                }
                break;
        }
    }
    addCartToHTML();
    addCartToMemory();
 }

const initApp = () => {
    // get data product
    fetch('product.json')
    .then(response => response.json())
    .then(data => {
        products = data;
        addDataToHTML();
      
        // get data cart from memory
        if(localStorage.getItem('cart')){
            cart = JSON.parse(localStorage.getItem('cart'));
            addCartToHTML();
            addmodalToHTML();
        }
    })
}
initApp();