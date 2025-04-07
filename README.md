# Recipe App API

This is the backend API for a Recipe App built with Python (Django), PostgreSQL, and Docker Compose. It provides a set of endpoints for managing recipes, ingredients, and users. The API allows you to create, read, update, and delete recipes, as well as manage the authentication and authorization of users.

## Table of Contents
- [Technologies Used](#technologies-used)
- [Setup Instructions](#setup-instructions)
  - [Prerequisites](#prerequisites)
  - [Clone the Repository](#clone-the-repository)
  - [Setup with Docker Compose](#setup-with-docker-compose)
  - [Running the Application](#running-the-application)
  - [Migrate Database](#migrate-database)
- [API Endpoints](#api-endpoints)
  - [Authentication](#authentication)
  - [Recipes](#recipes)
  - [Ingredients](#ingredients)
  - [Users](#users)
- [Testing](#testing)
- [License](#license)

## Technologies Used

- **Backend Framework**: Django
- **Database**: PostgreSQL
- **Containerization**: Docker, Docker Compose
- **Authentication**: JWT (JSON Web Tokens)
- **API Documentation**: Swagger (via Django REST Framework)

## Setup Instructions

### Prerequisites

- Make sure you have the following installed:
  - [Docker](https://www.docker.com/get-started) (includes Docker Compose)
  - [Git](https://git-scm.com/)
  - [Python](https://www.python.org/downloads/) (optional, in case you want to run the app without Docker)

### Clone the Repository

```bash
git clone https://github.com/koladee/recipe-app-api.git
cd recipe-app-api


### Setup with Docker Compose

1. Navigate to the project directory and build the Docker containers using Docker Compose.

    ```bash
    docker-compose build
    ```

2. Start the containers.

    ```bash
    docker-compose up
    ```

    This will start the Django application along with PostgreSQL in separate containers.

### Running the Application

Once the containers are running, the API will be available at [http://localhost:8000](http://localhost:8000).

### Migrate Database

Before running the application, you need to migrate the database to set up the tables.

```bash
docker-compose exec web python manage.py migrate
```

This will apply all the database migrations for the app.

### Create Superuser (optional)

To access the Django Admin panel, create a superuser.

```bash
docker-compose exec web python manage.py createsuperuser
```

Follow the prompts to create an admin user.

### Seed Database (optional)

You can seed the database with some sample data by running:

```bash
docker-compose exec web python manage.py loaddata recipes/fixtures/sample_data.json
```

## API Endpoints

The following are the main API endpoints available in this recipe app API.

### Authentication

- **POST** `/api/auth/login/`: Login and receive a JWT token.
    - **Request Body**:
    ```json
    {
      "username": "user",
      "password": "password"
    }
    ```
    - **Response**:
    ```json
    {
      "token": "your-jwt-token"
    }
    ```

- **POST** `/api/auth/register/`: Register a new user.
    - **Request Body**:
    ```json
    {
      "username": "new_user",
      "password": "new_password",
      "email": "new_user@example.com"
    }
    ```

- **POST** `/api/auth/logout/`: Logout and invalidate the JWT token.

### Recipes

- **GET** `/api/recipes/`: Get a list of all recipes.
    - **Response**:
    ```json
    [
      {
        "id": 1,
        "title": "Spaghetti Bolognese",
        "ingredients": [
          "Spaghetti",
          "Ground Beef",
          "Tomato Sauce"
        ],
        "instructions": "Cook spaghetti. Brown the ground beef. Mix with sauce."
      }
    ]
    ```

- **POST** `/api/recipes/`: Create a new recipe.
    - **Request Body**:
    ```json
    {
      "title": "New Recipe",
      "ingredients": ["Ingredient1", "Ingredient2"],
      "instructions": "Step 1, Step 2."
    }
    ```

- **GET** `/api/recipes/{id}/`: Get a specific recipe by ID.
    - **Response**:
    ```json
    {
      "id": 1,
      "title": "Spaghetti Bolognese",
      "ingredients": [
        "Spaghetti",
        "Ground Beef",
        "Tomato Sauce"
      ],
      "instructions": "Cook spaghetti. Brown the ground beef. Mix with sauce."
    }
    ```

- **PUT** `/api/recipes/{id}/`: Update a specific recipe.
    - **Request Body**:
    ```json
    {
      "title": "Updated Recipe",
      "ingredients": ["Updated Ingredient1", "Updated Ingredient2"],
      "instructions": "New instructions."
    }
    ```

- **DELETE** `/api/recipes/{id}/`: Delete a specific recipe by ID.

### Ingredients

- **GET** `/api/ingredients/`: Get a list of all ingredients.

- **POST** `/api/ingredients/`: Add a new ingredient.
    - **Request Body**:
    ```json
    {
      "name": "Tomato"
    }
    ```

### Users

- **GET** `/api/users/`: Get a list of all users.

- **GET** `/api/users/{id}/`: Get a specific user by ID.

## Testing

To run the tests, ensure the Docker containers are running and use the following command:

```bash
docker-compose exec web python manage.py test
```

This will run the Django test suite and check for any issues.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

