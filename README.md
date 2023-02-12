# onlineShopping
The shopping cart should allow users to browse products, add them to cart, and checkout. 

The users should be able to view their order history.

 The following features are required: 

1. User Authentication: Users should be able to sign up, login, and logout. 
2. Product Catalog: A list of products with their details (name, description, price, and image). 
3. Shopping Cart: A user should be able to add multiple products to their cart and view the total cost. 
4. Checkout: The user should be able to checkout, providing their shipping information and payment details. 
5. Order History: A user should be able to view a list of their past orders and the details of each order. 
6. Admin Panel: An admin panel should be provided to manage products and orders. 


User Authentication:
Start by creating a new Django project using the following command:

django-admin startproject my_shopping_cart

Create an app for authentication using the following command:
python manage.py startapp authentication

In the models.py file of the authentication app, define a custom user model to store the user's information:
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    pass

Update the AUTH_USER_MODEL setting in the settings.py file to use the custom user model:

AUTH_USER_MODEL = 'authentication.CustomUser'

Create the views, URLs, and templates to handle user registration, login, and logout.



Product Catalog:
Create a new app for the product catalog using the following command:
python manage.py startapp product_catalog
In the models.py file of the product_catalog app, define a model to store the product information:
from django.db import models

Create the views, URLs, and templates to display the product catalog and individual product details.
scss
class Product(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    image = models.ImageField(upload_to='products/')
Shopping Cart:
Create a new app for the shopping cart using the following command:
python manage.py startapp shopping_cart

In the models.py file of the shopping_cart app, define a model to store the items in the cart:
javascript
from django.db import models
from product_catalog.models import Product
class CartItem(models.Model):
    user = models.ForeignKey(CustomUser, on_delete=models.CASCADE)
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField(default=1)
Create the views, URLs, and templates to handle adding items to the cart, displaying the items in the cart, and updating the item quantities.

Checkout:
In the models.py file of the shopping_cart app, define a model to store the order information:
scss
class Order(models.Model):
    user = models.ForeignKey(CustomUser, on_delete=models.CASCADE)
    items = models.ManyToManyField(CartItem)
    shipping_address = models.TextField()
    payment_details = models.TextField()

Create the views, URLs, and templates to handle the checkout process and store the order information.

For the Order History feature, you will need to create a view that fetches the order history of a particular user. You can use Django's built-in authentication views to handle user authentication and retrieve the current user's order history. You can display this information to the user in a template.
For the Admin Panel feature, you will need to create a view that allows an administrator to manage products and orders. You can use Django's built-in admin interface for this or create a custom view that uses Django's authentication system to ensure that only administrators have access to the panel.
