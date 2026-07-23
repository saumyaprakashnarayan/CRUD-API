# Task API

A beginner-friendly CRUD API built with **FastAPI** for creating and managing tasks. The project follows the workflow from *W2 - Build Your First CRUD API* and demonstrates how HTTP methods map to create, read, update, and delete operations.

## Features

- Create, read, update, and delete tasks
- Validate request bodies with Pydantic models
- Return useful HTTP status codes and error messages
- Built-in interactive API documentation with Swagger UI and ReDoc
- Health-check endpoint for verifying that the service is running
- In-memory task storage for simple learning and experimentation

## Technology

- Python 3.12 or later
- FastAPI
- Uvicorn
- Pydantic, included with FastAPI

## Project Structure

```text
crud/
├── main.py          # FastAPI application and task CRUD routes
├── pyproject.toml   # Project metadata and dependencies
├── README.md        # Project documentation
└── screenshots_swaggerUI/
										# Swagger UI screenshots
```

Screenshots of the interactive Swagger UI are available in the [`screenshots_swaggerUI/`](screenshots_swaggerUI/) folder.

## Setup

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the project dependencies:

```bash
python -m pip install -e .
```

If you use `uv`, the equivalent setup is:

```bash
uv sync
```

## Run the API

Start the development server from the project directory:

```bash
uvicorn main:app --reload
```

The API will be available at:

- API root: <http://127.0.0.1:8000/>
- Swagger UI: <http://127.0.0.1:8000/docs>
- ReDoc: <http://127.0.0.1:8000/redoc>
- OpenAPI schema: <http://127.0.0.1:8000/openapi.json>

## Endpoints

| Method | Endpoint | Description |
| --- | --- | --- |
| `GET` | `/` | Return API information |
| `GET` | `/health` | Check whether the API is running |
| `GET` | `/tasks` | Return all tasks |
| `GET` | `/tasks/{task_id}` | Return one task by ID |
| `POST` | `/tasks` | Create a task |
| `PUT` | `/tasks/{task_id}` | Replace a task's title and completion state |
| `DELETE` | `/tasks/{task_id}` | Delete a task |

## Data Models

### Create a task

`POST /tasks` expects a JSON body containing a title:

```json
{
	"title": "Read the FastAPI documentation"
}
```

New tasks start with `done` set to `false`.

### Update a task

`PUT /tasks/{task_id}` expects both the title and completion state:

```json
{
	"title": "Read the FastAPI documentation",
	"done": true
}
```

An empty or whitespace-only title is rejected with a `400 Bad Request` response.

## Example Requests

List all tasks:

```bash
curl http://127.0.0.1:8000/tasks
```

Get a specific task:

```bash
curl http://127.0.0.1:8000/tasks/1
```

Create a task:

```bash
curl -X POST http://127.0.0.1:8000/tasks \
	-H "Content-Type: application/json" \
	-d '{"title":"Practice CRUD operations"}'
```

Update a task:

```bash
curl -X PUT http://127.0.0.1:8000/tasks/1 \
	-H "Content-Type: application/json" \
	-d '{"title":"Learn FastAPI CRUD","done":true}'
```

Delete a task:

```bash
curl -i -X DELETE http://127.0.0.1:8000/tasks/1
```

## HTTP Responses

- `200 OK`: Successful read or update
- `201 Created`: Task created successfully
- `204 No Content`: Task deleted successfully
- `400 Bad Request`: Task title is empty
- `404 Not Found`: Task with the requested ID does not exist
- `422 Unprocessable Entity`: Request body or path parameter has an invalid format




