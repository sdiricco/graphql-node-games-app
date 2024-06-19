# Query on Apollo client

[](./graphql.drawio.png)

You should see 4 main sections: **Operation**, **Variables**, **Response**, **Collection**

An **Operation** is a query in graphql syntax, the **Variables** are used during **Operation** while the **Response** is the response of query.

You can also save your **Operation** with **Variables** in a **Collection**

## GamesQuery

**Operation**
```graphql
query GamesQuery {
  games {
    id,
    title,
    platform
  }
}
```

**Response**
```json
{
  "data": {
    "games": [
      {
        "id": "1",
        "title": "Dark souls",
        "platform": [
          "Switch"
        ]
      },
      {
        "id": "2",
        "title": "Final Fantasy 7 Remake",
        "platform": [
          "PS5",
          "Xbox"
        ]
      },
      {
        "id": "4",
        "title": "Mario Kart",
        "platform": [
          "Switch"
        ]
      },
      {
        "id": "5",
        "title": "Pokemon Scarlet",
        "platform": [
          "PS5",
          "Xbox",
          "PC"
        ]
      },
      {
        "id": "9855",
        "title": "Super Gear Solid",
        "platform": [
          "XBox",
          "N64"
        ]
      }
    ]
  }
}
```

## GameQuery

**Operation**
```graphql
query GameQuery($id: ID!){
  game(id: $id) {
    id,
    title,
    platform
  }
}
```

**Variables**
```json
{
  "id": "4"
}
```


**Response**
```json
{
  "data": {
    "game": {
      "id": "4",
      "title": "Mario Kart",
      "platform": [
        "Switch"
      ]
    }
  }
}
```


## GameNestedQuery

**Operation**
```graphql
query GameNestedQuery($id: ID!){
  game(id: $id){
    title,
    reviews {
      id
      rating,
      content,
      author {
        id,
        name,
        verified
      }
    }
  }
}
```

**Variables**

```json
{
  "id": "4"
}
```


**Response**
```json
{
  "data": {
    "game": {
      "title": "Mario Kart",
      "reviews": [
        {
          "id": "4",
          "rating": 5,
          "content": "lorem ipsum",
          "author": {
            "id": "2",
            "name": "yoshi",
            "verified": false
          }
        }
      ]
    }
  }
}
```

## AuthorsQuery

**Operation**
```graphql
# Query the Authors from DB with following fields:
# id, name, verified

query AuthorsQuery {
  authors {
    id,
    name,
    verified
  }
}
```

**Variables**

```json
```

**Response**
```json
{
  "data": {
    "authors": [
      {
        "id": "1",
        "name": "mario",
        "verified": true
      },
      {
        "id": "2",
        "name": "yoshi",
        "verified": false
      },
      {
        "id": "3",
        "name": "peach",
        "verified": true
      }
    ]
  }
}
```

## AuthorQuery

**Operation**
```graphql
query AuthorQuery($id: ID!){
  author(id: $id) {
    id,
    name,
    verified
  }
}
```

**Variables**

```json
{
  "id": "2"
}
```

**Response**
```json
{
  "data": {
    "author": {
      "id": "2",
      "name": "yoshi",
      "verified": false
    }
  }
}
```

## ReviewsQuery

**Operation**
```graphql
# Query the Reviews from DB with following fields:
# id, content, rating

query ReviewsQuery {
  reviews {
    id,
    content,
    rating
  }
}

```

**Variables**

```json
```

**Response**
```json
{
  "data": {
    "reviews": [
      {
        "id": "1",
        "content": "lorem ipsum",
        "rating": 9
      },
      {
        "id": "2",
        "content": "lorem ipsum",
        "rating": 10
      },
      {
        "id": "3",
        "content": "lorem ipsum",
        "rating": 7
      },
      {
        "id": "4",
        "content": "lorem ipsum",
        "rating": 5
      },
      {
        "id": "5",
        "content": "lorem ipsum",
        "rating": 8
      },
      {
        "id": "6",
        "content": "lorem ipsum",
        "rating": 7
      },
      {
        "id": "7",
        "content": "lorem ipsum",
        "rating": 10
      }
    ]
  }
}
```

## ReviewQuery

**Operation**
```graphql
query ReviewQuery($id: ID!){
  review(id: $id) {
    id,
    content,
    rating
  }
}
```

**Variables**

```json
{
  "id": "2"
}
```

**Response**
```json
{
  "data": {
    "review": {
      "id": "2",
      "content": "lorem ipsum",
      "rating": 10
    }
  }
}
```

## AddGameQuery

**Operation**
```graphql
mutation AddGameMutation($game: AddGameInput!,){
  addGame(game: $game) {
    id,
    platform,
    title
  }
}
```

**Variables**

```json
{
  "game": {
    "title": "Super Gear Solid",
    "platform": ["XBox", "N64"]
  }
}
```

**Response**
```json
{
  "data": {
    "addGame": {
      "id": "9855",
      "platform": [
        "XBox",
        "N64"
      ],
      "title": "Super Gear Solid"
    }
  }
}
```

## EditGameQuery

**Operation**
```graphql
# Update game passing id and edit fields

mutation EditGameMutation($edits: EditGameInput!, $id: ID!){
  updateGame(edits: $edits, id: $id) {
    title,
    platform
  }
}
```

**Variables**

```json
{
  "id": "1",
  "edits": {
    "title": "Dark souls"
  }
}
```

**Response**
```json
{
  "data": {
    "updateGame": {
      "title": "Dark souls",
      "platform": [
        "Switch"
      ]
    }
  }
}
```

## DeleteGameQuery

**Operation**
```graphql
mutation DeleteGameMutation($id: ID!){
  deleteGame(id: $id) {
    id,
    title,
  }
}
```

**Variables**

```json
{
  "id": "3"
}
```

**Response**
```json
{
  "data": {
    "deleteGame": [
      {
        "id": "1",
        "title": "Dark souls"
      },
      {
        "id": "2",
        "title": "Final Fantasy 7 Remake"
      },
      {
        "id": "4",
        "title": "Mario Kart"
      },
      {
        "id": "5",
        "title": "Pokemon Scarlet"
      },
      {
        "id": "9855",
        "title": "Super Gear Solid"
      }
    ]
  }
}
```