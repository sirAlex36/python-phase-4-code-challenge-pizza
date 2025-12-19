Pizza Restaurant API
This project is a Flask-based RESTful API that manages relationships between Pizzas and Restaurants using a many-to-many relationship through a RestaurantPizza join table.

🛠 Tech Stack
Language: Python 3.8.13

Framework: Flask 2.2.2

Database: SQLAlchemy with Flask-SQLAlchemy 3.0.3

Serialization: SQLAlchemy-Serializer

Migration: Flask-Migrate

🚀 Environment Setup & Troubleshooting
During development, a specific build error was encountered: AttributeError: install_layout. This was resolved by pinning the build tools in the Pipfile.

Build Fix: Forced setuptools == 58.2.0 to ensure compatibility with Python 3.8 on Debian/Ubuntu systems.

Compatibility Fix: Pinned Werkzeug == 2.2.2 to resolve the ImportError: cannot import name 'url_quote' common in Flask 2.2.x.

📊 Database Schema
The project implements a Many-to-Many relationship:

Restaurant: Has many Pizzas through RestaurantPizza.

Pizza: Has many Restaurants through RestaurantPizza.

RestaurantPizza: Acts as the join table, containing price, pizza_id, and restaurant_id.

🛠 Features
1. Data Validation
Price Validation: Implemented @validates('price') in the RestaurantPizza model to ensure all pizza prices are between 1 and 30.

2. Advanced Serialization
Used SerializerMixin with custom serialize_rules to provide clean JSON output and prevent infinite recursion loops:

Index Views: Configured to show basic details only.

Show Views: Dynamically configured to include nested relationship data (e.g., showing a Restaurant's pizzas) while stopping the recursion back to the parent object.

API endpoints
GET  /restaurant  Returns list of all restaurants.
GET  /restaurant/<int:id>  Returns details of speciic restaurant and its pizzas
DELETE  /restaurants/<int:id>  Delete a restaurant and its associate records.
GET  /pizzas   Return a list of all available pizzas.
POST  /restaurant_pizzas   create a new pizza/restaurant association (validates price).