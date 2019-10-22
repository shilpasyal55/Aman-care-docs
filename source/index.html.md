---
title: Amancare Cover API docs

language_tabs: # must be one of https://git.io/vQNgJ
  - Ruby

toc_footers:
  - <a href='http://nugeninfo.com'>AmanCare Cover API Docs</a>


search: true
---

# Introduction

AmanCare Cover Api Docs

# Login-Signup

## Signup - Create User


> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1,
  "token": "7dhf8hfjhdjf8rrhjdjfhdf844"
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Email already taken"
}

```

This endpoint will save a new user.
For Supplier => Name,Address,Mobile,Email,Role,Password
For Vendor => Name,Address,Mobile,Email,GST,Role,Password
For MR => Name,Address,Mobile,Email,Qualification,Role,Password

### HTTP Request

`POST https://amancover.herokuapp.com/v1/users`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
mobile | String | Mobile number of user
name | String | User name
email | String | User email
password | String | Password of user
gst | String | Gst (only for vendor)
address | String | Address of user
qualification | String | Qualification of user(only for mr)
role | String | Value must be => admin,vendor,supplier or mr


## Login - Authentication

> Success-Response:

```json

HTTP 200 OK
{
  "token": "7dhf8hfjhdjf8rrhjdjfhdf844",
  "msg": 1,
  "verified": true,
  "role": "vendor"
}

```

> Error-Response

```json
HTTP 401 Unprocessable entity
{
     "msg": 0,
     "error": "Mobile/Password doesnot match"
}

```

Login/Authenticate User.
User can login with both email and mobile number

### HTTP Request

`POST https://amancover.herokuapp.com/v1/login`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
mobile | String | Mobile number/ Email of user
password | String | Password of user


## Verify Account

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Please enter correct OTP."
}

```

Verify User Account

### HTTP Request

`POST https://amancover.herokuapp.com/v1/verification`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
code | String | Code sent to user

<aside class="success">
 User must be authorized to verify account.Send user token in the header.
</aside>


## Resend Verification Code

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Error while resending Code"
}

```
Resend Verification Code to User

### HTTP Request

`GET https://amancover.herokuapp.com/v1/resendCode`

### Query Parameters

No Parameters

<aside class="success">
 User must be authorized to resend code.Send user token in the header.
</aside>

## Fetch Single User

> Success-Response:

```json

HTTP 200 OK
{
  "name": "shilpa",
  "mobile": "3848347843",
  "email": "data",
  "gst": "data",
  "address": "data",
  "role": "data",
  "verified": "data",
  "qualification": "data",
  "is_active": true,
  "created_by": "self",
  "photo": "/uploads/jdfh878.jpg",

}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Unable to find detail"
}

```

Fetch single user detail

### HTTP Request

`GET https://amancover.herokuapp.com/v1/getUser`

### Query Parameters

No Parameter

<aside class="success">
 User must be authorized to fetch data.Send user token in the header.
</aside>

## Update Password

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Your password was incorrect"
}

```

Update user Password when user is logged in

### HTTP Request

`POST https://amancover.herokuapp.com/v1/changePassword`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
old_password | String | Old Password of the user
new_password | String | New Password of the user

<aside class="success">
 User must be authorized to change password.Send user token in the header.
</aside>

## Send Code for Forgot Password

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Mobile Number not present in our database"
}

```

To reset password, Api will send code for resetting the password.

### HTTP Request

`POST https://amancover.herokuapp.com/v1/forgotPassword`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
mobile | String | Registered Mobile number of user


## Change Password (Forgot Password)

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Mobile Number not present in our database"
}

```

Change Password

### HTTP Request

`POST https://amancover.herokuapp.com/v1/updatePassword`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
code | String | Code sent to the registered mobile number
password | String | New Password


## Update User Info

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0
}

```

Update user credentials

### HTTP Request

`POST https://amancover.herokuapp.com/v1/updateUser`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
mobile | String | Mobile number of user
name | String | User name
email | String | User email
gst | String | Gst (only for vendor)
address | String | Address of user
qualification | String | Qualification of user(only for mr)

<aside class="success">
 User must be authorized. Send user token in the header.
</aside>

## Update/Save User Image

> Success-Response:

```json

HTTP 200 OK
{
    "msg": 1,
    "image": "/uploads/2b482b0f669fbd8f_100_Gift_Voucher.png"
}

```

> Error-Response

```json
HTTP 422 Unprocessable entity
{
     "msg": 0,
     "error": "Image can't be blank"
}

```

Update or save user image.
Only mr user id allowed to save image

### HTTP Request

`POST https://amancover.herokuapp.com/v1/updateImage`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
photo | String | photo of mr user

<aside class="success">
 User must be authorized to change password.Send user token in the header.
</aside>

# Categories

## Save Category

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Category name already taken"
}

```

Save new Category.
Only Admin can save the category otherwise you will get not authorized error.

### HTTP Request

`POST https://amancover.herokuapp.com/v1/categories`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
name | String | Name of category

<aside class="success">
 User must be authorized to change password.Send user token in the header.
</aside>

## Fetch All Categories

> Success-Response:

```json

HTTP 200 OK
[
  {
  "id": 1,
  "name": "caregory",
  "is_active": true,
  "created_at": "2019-09-24T15:36:55.632Z",
  "updated_at": "2019-09-24T15:36:55.632Z"
  }
]
```

Get all the categories

### HTTP Request

`GET https://amancover.herokuapp.com/v1/categories`


## Fetch Active Categories

> Success-Response:

```json

HTTP 200 OK
[
  {
  "id": 1,
  "name": "caregory",
  "is_active": true,
  "created_at": "2019-09-24T15:36:55.632Z",
  "updated_at": "2019-09-24T15:36:55.632Z"
  }
]

```

Get all active categories

### HTTP Request

`GET https://amancover.herokuapp.com/v1/activeCategories`


## Change Category status

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Error while updating Category"
}

```

Update category status to active and inactive.
Only admin can update the category status otherwise you will get the not authorized error


### HTTP Request

`POST https://amancover.herokuapp.com/v1/updateCategoryStatus`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
category_id | String | Id of category
status | String | true or false

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch Single Category

> Success-Response:

```json

HTTP 200 OK
{
    "id": 1,
    "name": "update cateory",
    "is_active": true,
    "created_at": "2019-09-24T15:36:55.632Z",
    "updated_at": "2019-09-24T15:48:42.141Z"
}
```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Category not found"
}

```
Fetch single category

### HTTP Request

`GET https://amancover.herokuapp.com/v1/categories/:id`

### Query Parameters

SEnd id in parameter

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Update Category

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Category not found"
}

```
Update single category.
Only admin can update the category otherwise you will get the not authorized error


### HTTP Request

`POST https://amancover.herokuapp.com/v1/updateCategory`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
name | String | Name of category
category_id | String | ID of category

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

# Products

## Save Product

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Product name can't be blank"
}

```

Save new Product.
Only admin can save the products otherwise you will get the not authorized error

### HTTP Request

`POST https://amancover.herokuapp.com/v1/products`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
name | String | Name of Product
quantity | String | Quantity of Product
category_id | String | Category
size | String | size of product
color | String | color of product
price | String | price of product
image | String | image of product


<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Update Product

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Unable to update product"
}

```

Update the existing product.
Only admin can update the product otherwise you will get not authorized error


### HTTP Request

`POST https://amancover.herokuapp.com/v1/updateProduct`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
name | String | Name of Product
quantity | String | Quantity of Product
category_id | String | Category
size | String | size of product
color | String | color of product
price | String | price of product
image | String | image of product
image_updated | String | send true or false if image is updated
id | String | id of product

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch Single Product

> Success-Response:

```json

HTTP 200 OK
  {
      "id": 1,
      "category_id": 1,
      "user_id": 1,
      "name": "jhj",
      "size": "uy",
      "quantity": "7",
      "color": "red",
      "price": "89",
      "image": null,
      "created_at": "2019-09-21T06:17:51.157Z",
      "updated_at": "2019-09-21T06:17:51.157Z",
      "is_active": true,
      "category_name": "xyz"
  }

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Unable to find Product"
}

```

Fetch Single Product details

### HTTP Request

`GET https://amancover.herokuapp.com/v1/products/:id`

### Query Parameters

Send Id in the url

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch All Products

> Success-Response:

```json

HTTP 200 OK
[
    {
        "id": 1,
        "category_id": 1,
        "user_id": 1,
        "name": "jhj",
        "size": "uy",
        "quantity": "7",
        "color": "red",
        "price": "89",
        "image": null,
        "created_at": "2019-09-21T06:17:51.157Z",
        "updated_at": "2019-09-21T06:17:51.157Z",
        "is_active": true,
        "category_name": "xyz"
    },
    {
        "id": 2,
        "category_id": 1,
        "user_id": 1,
        "name": "jhjjdhfjdf",
        "size": " uy",
        "quantity": " 7",
        "color": " reddfdf",
        "price": " 89",
        "image": "/uploads/3cfbd092d5cf1e63Logo__1_.png",
        "created_at": "2019-09-21T06:22:32.113Z",
        "updated_at": "2019-09-21T06:22:32.113Z",
        "is_active": true,
        "category_name": "xyz"
    }
]

```

Fetch All Product details

### HTTP Request

`GET https://amancover.herokuapp.com/v1/products`

### Query Parameters

No Parameters

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

# Orders

## Save Order

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1,
  "order_id": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "material can't be blank"
}

```

Save new Order

### HTTP Request

`POST https://amancover.herokuapp.com/v1/orders`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
product_id | String | Id of Product
material | String | material of Product
quantity | String | quantity of the product
price | String | price
brand_logo | String | Photo of brand logo
firm_name | String | Firm name
address | String | Address
mobile | String | Mobile
payment_mode | String | ed cod, online
user_id | String | user id of vendor ( Send it only if vendor is created by mr)

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch All Orders

> Success-Response:

```json

HTTP 200 OK
  [
    {
        "id": 3,
        "user_id": 3,
        "product_id": 1,
        "material": "cotton",
        "quantity": "2",
        "price": "10",
        "brand_logo": "/uploads/76bf21e4ee7c401b_100_Gift_Voucher.png",
        "firm_name": "jhjh",
        "address": "dkjf",
        "mobile": "78787878",
        "created_at": "2019-09-30T07:52:42.492Z",
        "updated_at": "2019-09-30T07:52:42.492Z",
        "confirmed": false,
        "payment_status": null,
        "payment_description": null,
        "order_by_role": "mr",
        "order_by_id": 2,
        "payment_mode": "cod",
        "payment_id": null,
        "product_name": "nugennnd",
        "user_name": "varun1",
        "order_by_name": "aman",
        "order_by_mobile": "7894561230"
    }
  ]

```

Fetch all orders of all users.
Payment status initialy => "not initialized"

### HTTP Request

`GET https://amancover.herokuapp.com/v1/orders`

### Query Parameters

No parameters

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch Single Order detail

> Success-Response:

```json

HTTP 200 OK
{
    "id": 3,
    "user_id": 3,
    "product_id": 1,
    "material": "cotton",
    "quantity": "2",
    "price": "10",
    "brand_logo": "/uploads/76bf21e4ee7c401b_100_Gift_Voucher.png",
    "firm_name": "jhjh",
    "address": "dkjf",
    "mobile": "78787878",
    "created_at": "2019-09-30T07:52:42.492Z",
    "updated_at": "2019-09-30T07:52:42.492Z",
    "confirmed": false,
    "payment_status": null,
    "payment_description": null,
    "order_by_role": "mr",
    "order_by_id": 2,
    "payment_mode": "cod",
    "payment_id": null,
    "product_name": "nugennnd",
    "user_name": "varun1",
    "order_by_name": "aman",
    "order_by_mobile": "7894561230"
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Unable to find order"
}

```

get single order detail

### HTTP Request

`GET https://amancover.herokuapp.com/v1/orders/:id`

### Query Parameters

Send order id in url

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Order Confirmation by Admin

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "not authorized"
}

```

Confirm order place by admin.
Order can only be confirmed by admin otherwise you will get not authorized error.

### HTTP Request

`POST https://amancover.herokuapp.com/v1/orderConfirmation`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
order_id | String | Id of Order

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch all orders of particular user

> Success-Response:

```json

HTTP 200 OK
  [
    {
      "id": 3,
      "user_id": 3,
      "product_id": 1,
      "material": "cotton",
      "quantity": "2",
      "price": "10",
      "brand_logo": "/uploads/76bf21e4ee7c401b_100_Gift_Voucher.png",
      "firm_name": "jhjh",
      "address": "dkjf",
      "mobile": "78787878",
      "created_at": "2019-09-30T07:52:42.492Z",
      "updated_at": "2019-09-30T07:52:42.492Z",
      "confirmed": false,
      "payment_status": null,
      "payment_description": null,
      "order_by_role": "mr",
      "order_by_id": 2,
      "payment_mode": "cod",
      "payment_id": null,
      "product_name": "nugennnd",
      "user_name": "varun1",
      "order_by_name": "aman",
      "order_by_mobile": "7894561230"
    }
  ]

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "No orders found"
}

```

Fetch all orders of particular user

### HTTP Request

`GET https://amancover.herokuapp.com/v1/fetchUserOrders`

### Query Parameters

No Parameters

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>


## Payment of Order

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Unable to update Payment status.Please Try Again"
}

```

```json

HTTP 402 OK
{
  "msg": 0,
  "error": "Payment Failed"
}

```

Do Payment of the order. By Default the payment status is "not_initialized".
If successfull then send "success" else "failed"

### HTTP Request

`POST https://amancover.herokuapp.com/v1/paymentConfirmation`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
order_id | String | Id of Order
payment_id | String | Id of Payment
payment_status | String | By default "not_initialized", otherwise send "success" and "failed"
payment_description | String | if failed then send the description of the failure

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

# User Locations

## Save last location

> Success-Response:

```json

HTTP 200 OK
{
  "msg": 1
}

```

> Error-Response:

```json

HTTP 422 OK
{
  "msg": 0,
  "error": "Unable to update location"
}

```

Save last location of current user

### HTTP Request

`POST https://amancover.herokuapp.com/v1/user_long_lats`

### Query Parameters

{
  "long_lat": {"longitude": 1.90384, "latitude": 2.3490}
}


<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch last location of current user

> Success-Response:

```json

HTTP 200 OK
{
    "id": 3,
    "user_id": 8,
    "long_lat": {
        "latitute": 2.349,
        "longitude": 1.90384
    },
    "created_at": "2019-10-11T05:25:10.071Z",
    "updated_at": "2019-10-11T05:25:10.071Z"
}

```


Fetch last location of current user.
``If no location found, then api will return
{
    "msg": 0
}
``

### HTTP Request

`GET https://amancover.herokuapp.com/v1/userLocation`

### Query Parameters

No Parameters

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>

## Fetch last location of all users

> Success-Response:

```json

HTTP 200 OK
[
    {
        "id": 4,
        "user_id": 8,
        "long_lat": {
            "latitude": 2.245,
            "longitude": 1.24
        },
        "created_at": "2019-10-11T05:35:41.614Z",
        "updated_at": "2019-10-11T05:35:53.231Z"
    }
]

```

Fetch last location of all users. Only Admin is allowed to fetch all locations


### HTTP Request

`GET https://amancover.herokuapp.com/v1/fetchAllUserLocations`

### Query Parameters

No Parameters

<aside class="success">
 User must be authorized.Send user token in the header.
</aside>




