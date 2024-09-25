**Overview**

The collection is designed to validate the functionality of the Grocery Store API, including endpoints for listing products, managing carts, placing orders, and more. Each request is accompanied by tests to verify the status code, response structure, and specific field values.

**Base URL:**

https://simple-grocery-store-api.glitch.me

**API Tests Included**

**1. API Status**

Method: GET

Endpoint: /status

Description: Checks if the API is up and running.

Assertions:
  Status code is 200.
  The API status should be UP.

**javascript**

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
pm.test("Status should be UP", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.status).to.eql("UP");
});

**2. List All Products**

Method: GET

Endpoint: /products

Description: Retrieves all available products.

Assertions: Status code is 200.

**javascript**

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

**3. List a Product by ID**

Method: GET

Endpoint: /products/:productId

Description: Fetches the details of a product using its ID.

Assertions:

  Status code is 200.
  
  Product name, price, category, and stock status should match the expected values.

**javascript**

pm.test("Product Name", () => {
    pm.expect(response.name).to.eql("Green Cabbage Organic");
});
pm.test("Product Price", () => {
    pm.expect(response.price).to.eql(3.02);
});
pm.test("Product Category", () => {
    pm.expect(response.category).to.eql("fresh-produce");
});
pm.test("Product in Stock", () => {
    pm.expect(response.inStock).to.eql(true);
});

**4. Create a New Cart**

Method: POST

Endpoint: /carts

Description: Creates a new shopping cart.

Assertions:

  Status code is 201.
  
  A valid cartId is returned.

**javascript**

pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});
pm.test("Response has valid cartId", () => {
    const response = pm.response.json();
    pm.expect(response).to.haveOwnProperty("cartId");
    pm.expect(response.cartId).to.be.a("string");
});

**5. Add Items to Cart**

Method: POST

Endpoint: /carts/:cartId/items

Description: Adds items to the cart.

Assertions:

  Status code is 201.
  
  The items are successfully added to the cart.

**6. Negative Tests: Missing or Invalid Authorization**

Method: Various

Description: These tests check for proper handling of requests without valid authentication tokens.

Assertions:

  Status code is 401.
  
  Error message should indicate missing or invalid authorization headers.

**javascript**

pm.test("Error Message", () => {
    const response = pm.response.json();
    pm.expect(response.error).to.eql("Missing Authorization header.");
});

**7. Invalid Input Tests**

Method: GET

Description: These tests validate how the API handles invalid inputs, such as invalid product categories or exceeding result limits.

Assertions:

  Status code is 400.
  
  Error message for invalid query parameters.

**javascript**

pm.test("Error Message", () => {
    const response = pm.response.json();
    pm.expect(response.error).to.have.string("Invalid value for query parameter 'category'.");
});


**How to Use the Collection**

1.Clone the repository: git clone https://github.com/sarahgsilveira/postman-trelloapi-tests

2.Import the Postman collection into your Postman application.

3.Set up your environment variables:

  baseURL: The base URL for the API.

  acessToken: Your API token.
  
  cartId: The ID of the cart to perform cart-related operations.

4.Run the tests using Postman's Collection Runner or integrate them into a CI/CD pipeline.

**Conclusion**

This test collection provides thorough coverage of the Grocery Store API. It includes tests for successful operations as well as error scenarios, ensuring that the API behaves as expected in both normal and edge cases. You can expand the tests or customize them to match your specific requirements.
