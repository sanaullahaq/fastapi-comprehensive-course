# FastAPI Comprehensive Course

[![Course Video](https://img.shields.io/badge/YouTube-Course%20Video-red)](https://youtu.be/0sOvCWFmrtA?si=RxYSVX9r9823AFFe)

A complete social media / blog API built with FastAPI, following the freeCodeCamp / Teclado course by Sanjeev Thiyagarajan. Features user authentication, post CRUD, voting/liking system, database migrations, Docker containerization, CI/CD, and production deployment guides.

## Tech Stack

| Category         | Technology                            |
| ---------------- | ------------------------------------- |
| Framework        | FastAPI, Uvicorn                      |
| ORM              | SQLAlchemy                            |
| Database         | PostgreSQL                            |
| Migrations       | Alembic                               |
| Validation       | Pydantic / pydantic-settings          |
| Auth             | JWT (python-jose), passlib + bcrypt   |
| Testing          | pytest, TestClient (httpx)            |
| Containerization | Docker / Docker Compose               |
| CI/CD            | GitHub Actions                        |
| Production       | Gunicorn + Uvicorn workers, Nginx     |

## Project Structure

```
.
├── app/
│   ├── main.py              # App entry point, CORS, routers
│   ├── config.py            # Environment config via BaseSettings
│   ├── database.py          # SQLAlchemy engine & session
│   ├── models.py            # ORM models: Post, User, Vote
│   ├── schemas.py           # Pydantic request/response schemas
│   ├── oauth2.py            # JWT token creation & verification
│   ├── utils.py             # Password hashing helpers
│   ├── calculation.py       # Demo math/BankAccount class
│   └── routers/
│       ├── posts.py         # Post CRUD endpoints
│       ├── users.py         # User registration & retrieval
│       ├── auth.py          # Login & token issuance
│       └── votes.py         # Vote/like endpoints
├── tests/
│   ├── conftest.py          # Fixtures (DB, client, auth, posts)
│   ├── test_calculation.py  # Unit tests
│   ├── test_users.py        # User & auth tests
│   ├── test_posts.py        # Post CRUD tests
│   └── test_votes.py        # Vote tests
├── alembic/                 # Migrations (7 revisions)
├── setups/                  # Setup guides & config files
└── .github/workflows/       # CI/CD pipeline
```

## Topics Covered

### 1. FastAPI Fundamentals
- Path operations (GET, POST, PUT, DELETE)
- Routers with `APIRouter`
- CORS Middleware

### 2. Pydantic Schemas & Validation
- Request/response schemas
- Nested models, `from_attributes`
- `EmailStr`, `conint`, `Field`

### 3. SQLAlchemy ORM
- Engine, sessionmaker, declarative models
- Relationships, foreign keys, composite PKs
- Queries: filter, join, group by, count

### 4. CRUD Operations
- Pagination (`limit`, `skip`, `search`)
- Aggregation with `func.count()`
- Post ownership & authorization

### 5. User Management
- Registration with password hashing
- Email uniqueness
- Response schema excluding password

### 6. Authentication (JWT)
- OAuth2PasswordBearer + OAuth2PasswordRequestForm
- Token creation, verification, expiration
- `get_current_user` dependency

### 7. Voting/Like System
- Direction-based votes (upvote / remove)
- Duplicate & non-existent vote handling

### 8. Configuration Management
- pydantic-settings BaseSettings
- Environment variables & `.env` files

### 9. Database Migrations (Alembic)
- `--autogenerate`, revision, upgrade, downgrade
- 7 incremental revisions reflecting real development

### 10. Testing with Pytest
- TestClient, dependency_overrides
- Fixtures: isolated DB, auth client, seeded data
- Parametrized tests, exception testing

### 11. Docker & Containerization
- Multi-stage Dockerfile
- Docker Compose (dev + prod profiles)
- `wait-for-it.sh` for service ordering

### 12. Production Deployment
- Ubuntu VM setup, PostgreSQL configuration
- Systemd service with Gunicorn + Uvicorn workers
- Nginx reverse proxy, UFW firewall

### 13. CI/CD (GitHub Actions)
- Automated testing with PostgreSQL service container
- Docker image build & push to Docker Hub

## API Endpoints

| Method | Endpoint         | Description              | Auth |
| ------ | ---------------- | ------------------------ | ---- |
| GET    | `/`              | Health check             | No   |
| POST   | `/posts/`        | Create post              | Yes  |
| GET    | `/posts/`        | List posts (paginated)   | Yes  |
| GET    | `/posts/{id}`    | Get post with vote count | Yes  |
| PUT    | `/posts/{id}`    | Update post (owner only) | Yes  |
| DELETE | `/posts/{id}`    | Delete post (owner only) | Yes  |
| POST   | `/users/`        | Register user            | No   |
| GET    | `/users/{id}`    | Get user details         | No   |
| POST   | `/login`         | Login, get JWT token     | No   |
| POST   | `/vote/`         | Upvote / remove vote     | Yes  |

## Running Locally

```bash
# Install dependencies
pip install -r req.txt

# Start with Docker Compose
docker compose up -d

# Or run directly (requires PostgreSQL running)
alembic upgrade head
uvicorn app.main:app --reload
```

## Testing

```bash
pytest -v -s --disable-warnings
```
