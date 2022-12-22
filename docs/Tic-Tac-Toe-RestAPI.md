# REST API for Tic-Tac-Toe

I tried building a REST API for my Tic-Tac-Toe game which contains game logic and can be integrated with a front-end of the developer's choice i.e, web app or mobile app etc.

Some important details -

- Language - [**Python (v3.11.0)**](https://www.python.org/)
- Framework - [**Flask**](https://flask.palletsprojects.com/en/2.2.x/)
- API Language - [**JSON**](https://www.w3schools.com/whatis/whatis_json.asp)
- Github Repo - [https://github.com/nkitanand/tictactoe_RestAPI.git](https://github.com/nkitanand/tictactoe_RestAPI.git) 


## Background 
-------------
### What is an API?

API stands for Application Programming Interface. It is a **technique** in programming world that is **used by several applications to talk to each other**.

### Why do we need API?

Let's say you are writing a program in C++ to solve some complex mathematical problems. Obviously, you are going to need some maths library that your program will use eventually. 
Now, You have two options -

1. Either you can write the library on your own. (which is not practical)
2. Alternatively, you can find some open source library (or paid library if you are $RICH ;-)) and use that to write your program. 

However, consider a situation where no library is available in C++ language as per your requirement but a library exists in python which exactly meets your requirement. Now, It would be awesome if there was a way to use python library in C++ program without much difficulty. That's where API comes in picture. 

Using API both programming language (C++ and python in this case) agree to talk to each other and take advantage of each other's functionality. Language used for communicating in API is usually JSON or XML. Using this intermediary language they can communicate with each other.

### Understanding API using our Tic-Tac-Toe example.

Let's say there is a Tic-Tac-Toe game as a web app. This game has two components - 

1. Front-End - dealing with the look and presentation of game
2. Back-End  - dealing with the logic of the game

Both components interact with each other using this API method. They use JSON to communicate. Ideally, during the start of projects both teams will agree on a JSON format that they can work with. This JSON will contain data like state of Gameboard, player info and state, winner status, etc.

``` mermaid
sequenceDiagram
    participant F as Front-End
    participant B as Back-End
    F->>+B: JSON (current game state)
    Note right of B: Execute game logic
    B->>-F: JSON response (updated game state)
```

<details>
  <summary>
    Diagram Explanation
  </summary>
Initially Front-End will create an empty board and present to web user. After user play his move, frontend will send JSON data representing the current game state to the backend. Backend after receiving the JSON data (i.e, the game state after user has played) will read the JSON to get details about the game state. Thereafter, backend will use logic to find optimal move for bot to play. Backend will update the JSON with new game state after bot has played it's move. Backend will send this updated JSON to frontend. Frontend after receiving this new JSON data will update the game board with bot's move and will wait for the User to play his next move. And this cycle continues until game is over.
</details>

## Architecture
---------------
 
JSON designed for our API is based on the schema given below.

<details>
  <summary>
    JSON Schema for our API
  </summary>
```JSON
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "Game": {
      "type": "string"
    },
    "Status": {
      "type": "string"
    },
    "Winner": {
      "type": "null"
    },
    "GameBoardState": {
      "type": "object",
      "properties": {
        "Box 1": {
          "type": "null"
        },
        "Box 2": {
          "type": "null"
        },
        "Box 3": {
          "type": "null"
        },
        "Box 4": {
          "type": "null"
        },
        "Box 5": {
          "type": "null"
        },
        "Box 6": {
          "type": "null"
        },
        "Box 7": {
          "type": "null"
        },
        "Box 8": {
          "type": "null"
        },
        "Box 9": {
          "type": "null"
        }
      },
      "required": [
        "Box 1",
        "Box 2",
        "Box 3",
        "Box 4",
        "Box 5",
        "Box 6",
        "Box 7",
        "Box 8",
        "Box 9"
      ]
    }
  },
  "required": [
    "Game",
    "Status",
    "Winner",
    "GameBoardState"
  ]
}
```
</details>

<details>
  <summary>
    JSON Example
  </summary>
```JSON
{
    "Game": "Tic Tac Toe", 
    "Status": "In Progress", 
    "Winner": null, 
    "GameBoardState": {
        "Box 1": null, 
        "Box 2": null, 
        "Box 3": null, 
        "Box 4": null, 
        "Box 5": null, 
        "Box 6": null, 
        "Box 7": null, 
        "Box 8": null, 
        "Box 9": null
        }
    }
```
</details>