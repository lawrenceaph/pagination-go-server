
# Go API Server on Cloud Run

This repository contains a Go server that provides an API returning a set of objects with pagination. It also serves HTML documentation at the root route. It can run on dockerized services like google cloud run or on a local or remote machine. The server can be used to test recursive functions with a real-world endpoint. Feel free to use the [current deployment](https://pagination-go-server-vxmdjsq65a-uc.a.run.app/) for testing or to deploy your own. 

## Features

- **Paginated API**: Provides data with pagination support, allowing clients to specify the page number and the number of objects per page.
- **HTML Documentation**: Serves HTML documentation at the root route (`/`).

## API Documentation

### Endpoint

#### `GET /api`

### Query Parameters

- `page` (optional): The page number to start fetching data from. Defaults to `1` if not provided or invalid.
- `perPage` (optional): The number of objects to return per page. Defaults to `10` if not provided or invalid. Maximum is `1000`.
- `longContent` (optional): If set to `true`, the content of each object will contain 50 words of "Lorem Ipsum" text.

### Response

The API returns a JSON object containing the requested objects and the next page number (if available).

#### Success Response

- **Code**: `200 OK`
- **Content**:
  ```json
  {
    "objects": [
      {
        "name": "random name 1",
        "content": "random content 1",
        "image": "https://placehold.co/600x400"
      },
      {
        "name": "random name 2",
        "content": "random content 2",
        "image": "https://placehold.co/600x400"
      }
      ...
    ],
    "nextPage": 2
  }
  ```

#### Error Response

- **Code**: `500 Internal Server Error`
- **Content**:
  ```json
  {
    "error": "error message"
  }
  ```

### Example Requests

#### Fetch Default Page

Fetches the first page with 10 objects per page (default behavior).

```bash
curl -X GET "https://pagination-go-server-vxmdjsq65a-uc.a.run.app/api"
```

#### Fetch Specific Page

Fetches the second page with 10 objects per page.

```bash
curl -X GET "https://pagination-go-server-vxmdjsq65a-uc.a.run.app/api?page=2"
```

#### Fetch Specific Page with Custom Objects per Page

Fetches the second page with 20 objects per page.

```bash
curl -X GET "https://pagination-go-server-vxmdjsq65a-uc.a.run.app/api?page=2&perPage=20"
```

#### Fetch with Long Content

Fetches the first page with 10 objects per page, with each object containing long "Lorem Ipsum" content.

```bash
curl -X GET "https://pagination-go-server-vxmdjsq65a-uc.a.run.app/api?page=1&perPage=10&longContent=true"
```

### Example Responses

#### Success Response

```json
{
  "objects": [
    {
      "name": "random name 11",
      "content": "random content 11",
      "image": "https://placehold.co/600x400"
    },
    {
      "name": "random name 12",
      "content": "random content 12",
      "image": "https://placehold.co/600x400"
    },
    ...
  ],
  "nextPage": 3
}
```

#### Error Response

```json
{
  "error": "error message"
}
```

## Running the Server Locally

To run this server locally, follow these steps:

1. Download the [pagination server file](https://github.com/lawrenceaph/pagination-go-server/releases/download/v0.1/pagination-server). 

2. Run the file. 

```  
./pagination-server 
```
3. Visit http://localhost:8080 to see the documentation or http://localhost:8080/api to test the api. 

### Example Local Requests

To fetch the first page with long content:

```bash
curl -X GET "http://localhost:8080/api?page=1&perPage=10&longContent=true"
```
 