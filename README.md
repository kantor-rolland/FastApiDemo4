# FastApiDemo4

A SQLAlchemy ORM demonstration project showcasing one-to-many relationships between database entities using SQLite.

## Features

- **SQLAlchemy ORM** - Declarative model definitions with relationship mapping
- **One-to-Many Relations** - Article has many Comments relationship pattern
- **SQLite Database** - Default persistence layer with optional PostgreSQL support
- **Session Management** - Context manager-based session handling for clean resource management

## Project Structure

```
FastApiDemo4/
├── main.py                                    # Entry point: demo CRUD operations
├── models/
│   └── article_comment_onetomany.py          # ORM models: Article, Comment
└── README.md
```

## Models

### Article
```python
Article(
    id: int (primary key)
    title: str
    comments: List[Comment]  # one-to-many relationship
)
```

### Comment
```python
Comment(
    id: int (primary key)
    content: str
    article_id: int (foreign key to articles)
)
```

## Usage

### Installation

Requires Python 3.7+ and SQLAlchemy:
```bash
pip install sqlalchemy
```

### Running the Demo

```bash
python main.py
```

This will:
1. Create SQLite database tables (`test.db`)
2. Insert a sample article with two comments
3. Query and print the article with its comments

**Output:**
```
Article ID: 1, Number of Comments: 2
Comment ID: 1
Comment ID: 2
```

## Database Configuration

### SQLite (Default)
```python
SQLALCHEMY_DATABASE_URL = 'sqlite:///./test.db'
```

### PostgreSQL (Commented - Uncomment to use)
```python
SQLALCHEMY_DATABASE_URL = f'postgresql://{DB_USER}:{DB_PASS}@localhost/fastapi_week4'
```

Set environment variables:
- `DB_USER` - PostgreSQL username
- `DB_PASS` - PostgreSQL password

## Key Patterns

- **Declarative ORM** - Models inherit from `declarative_base()`
- **Foreign Keys** - Child entities reference parent via `ForeignKey()` column
- **Relationships** - Parent entity declares `relationship()` to access children
- **Auto-create Tables** - `Base.metadata.create_all()` initializes schema
- **Session Context** - `with Session() as session:` ensures proper cleanup

## Future Enhancements

- [ ] Integrate FastAPI endpoints
- [ ] Add Alembic migrations
- [ ] Implement additional relationship types (many-to-many, etc.)
- [ ] Add data validation with Pydantic schemas