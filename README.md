# Full Stack Trivia API Final Project

## Project Description
Trivia app is a web application that allow people to play trivia and seeing who's the most knowledgeable of the bunch. The application is able to:

1) Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2) Delete questions.
3) Add questions and require that they include question and answer text.
4) Search for questions based on a text query string.
5) Play the quiz game, randomizing either all questions or within a specific category.

Follow the instructions below to get started! Also check out my [blog](https://towardsdatascience.com/reflection-on-my-first-api-project-67d6cee31ce4?source=friends_link&sk=601fe90519dba868771830c22dfe39cb) to see my reflection and takeaways from compeleting this project!

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

#### Installing frontend dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the `frontend` directory of this repository. After cloning, open your terminal and run:

```bash
npm install
```

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:

```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

## Running Your Frontend in Dev Mode

The frontend app was built using create-react-app. In order to run the app in development mode use ```npm start```. You can change the script in the ```package.json``` file. 

Open [http://localhost:3000](http://localhost:3000) to view it in the browser. The page will reload if you make edits.<br>

```bash
npm start
```

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

## API Reference

### Getting Started
- Backend Base URL: http://127.0.0.1:5000/
- Frontend Base URL: http://127.0.0.1:3000/

### Error Handling
Errors are returned in the following json format:
```
{
    'success': False,
    'error': 404,
    'message': 'Resource not found. Input out of range.'
}
```
The API returns 4 types of errors:
- 400: bad request
- 404: not found
- 422: unprocessable
- 500: internal server error

### Endpoints

##### GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Example: ```curl http://127.0.0.1:5000/categories | jq '.'```
```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true
}
```
##### GET '/questions'
- Fetches all the questions in the database. The questions are paginated with 10 questions each page.
- Example: ```curl http://127.0.0.1:5000/questions | jq '.'```
```
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "questions": [
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    }, 
    ...
    {
      "answer": "The Palace of Versailles", 
      "category": 3, 
      "difficulty": 3, 
      "id": 14, 
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }
  ], 
  "success": true, 
  "total_questions": 19
}
```
##### DELETE '/questions/int:id'
- Delete the question that was specified by its id in the url parameter.
- Example: ```curl -X DELETE http://127.0.0.1:5000/questions/17 | jq '.'```
```
{
    "success": "True",
    "deleted": 17
}
```

##### POST '/questions'
- Create a new question. The new question must have all four information. 
- Example: ```curl -X POST - H "Content-Type: application/json" -d '{"question": "Who is Oleksii Iovytsia?", "answer": "Junior full stack developer", "difficulty": 1, "category": "5"}' http://127.0.0.1:5000/questions | jq '.'```
```
{
  "success": true
  "created": 19
  "total_questions": 19
}
```

##### POST '/questions/search'
- User type in a string to search for a question and it will return all the questions that contain this string. 
- Example: ```curl -X POST -H "Content-Type: application/json" -d '{"searchTerm": "author"}' http://127.0.0.1:5000/questions/search | jq '.'```

```
{
  "questions": [
    {
      "answer": "Tom Cruise",
      "category": 5,
      "difficulty": 4,
      "id": 4,
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    }
  ],
  "success": true,
  "total_questions": 1
}
```

##### GET '/categories/int:id/questions'
- Get questions only in a specific category
- Example: ```curl http://127.0.0.1:5000/categories/3/questions | jq '.'```

```
{
  "current_category": "Geography",
  "questions": [
    {
      "answer": "Lake Victoria",
      "category": 3,
      "difficulty": 2,
      "id": 13,
      "question": "What is the largest lake in Africa?"
    },
    {
      "answer": "The Palace of Versailles",
      "category": 3,
      "difficulty": 3,
      "id": 14,
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }
  ],
  "success": true,
  "total_questions": 2
}

```

##### POST '/quizzes'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Example: ```curl -X POST -H "Content-Type: application/json" -d '{"previous_questions": [3, 5], "quiz_category": {"type": "Entertainment", "id": "5"}}' http://127.0.0.1:5000/quizzes | jq '.'```
```
{
  "question": {
    "answer": "Apollo 13",
    "category": 5,
    "difficulty": 4,
    "id": 2,
    "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
  },
  "success": true
}

```
## Author and Acknowledgement
- Oleksii Iovytsia contributed to API(```__init.py__```), test file(```test_flaskr.py```) and this ReadMe file. 
- The project and other files are credicted to [Udacity](https://www.udacity.com/)
# trivia-api
