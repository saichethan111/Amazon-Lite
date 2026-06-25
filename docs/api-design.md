Functional Requirements:

1. As soon as user logs in he should go to the landing page.
2. User should be able to search for a product.
3. User should be able to see the products he searched for.
4. User should be able to buy the products.

APIs:
1. Products:
   Description: Search the product
   API: Request: userId/searchProduct?productId=xxx
        Response: productDetails like name, price, availableQuantity
   Description: Add product to the cart
   API: Request: userId/addProduct?productId=xxx
        Response: NONE
   Description: Buying the product
   API: Request: userId/buyProduct
        Response: NONE
2. User:
   Description: Authenticate the user
      API: Request: users/getUser?userId=xxx
      Response: userDetails like name.
3. 

Additional Requirements: Search should return similar products (Like if user searched for iphone15 
and it is not present in the inventory then other products under the same category shall be returned).