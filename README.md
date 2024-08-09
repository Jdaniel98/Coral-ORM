# Coral ORM

Coral ORM is a simple Object-Relational Mapping (ORM) library for Python, designed to make database interactions more pythonic and easier to manage.

## Features

- Simple model definition
- Basic CRUD operations
- Connection pooling
- Query building
- Data validation

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/coral-orm.git
   cd coral-orm
   ```

2. Install the required dependencies:
   ```
   pip install -r requirements.txt
   ```

## Database Setup

Before running the example, you need to set up a PostgreSQL database:

1. Install PostgreSQL if you haven't already.

2. Create a new database and user:
   ```sql
   CREATE DATABASE library_db;
   CREATE USER library_user WITH PASSWORD 'library_pass';
   GRANT ALL PRIVILEGES ON DATABASE library_db TO library_user;
   ```

3. Update the database configuration in `examples/example_usage.py` if necessary.

## Running the Example

The `examples` directory contains a sample application demonstrating the use of Coral ORM in a library management system.

To run the example:

1. Navigate to the `examples` directory:
   ```
   cd examples
   ```

2. Run the script:
   ```
   python example_usage.py
   ```

This will create the necessary tables, insert some sample data, and perform various queries to demonstrate the ORM's functionality.

## Usage

To use Coral ORM in your own project:

1. Configure the database connection in your main application file:
   ```python
   from coral_orm.config import DatabaseConfig, DatabaseManager

   config = DatabaseConfig(
       host='localhost',
       port=5432,
       database='your_database',
       user='your_user',
       password='your_password'
   )

   DatabaseManager.initialize(config)
   ```

2. Define your models:
   ```python
   from coral_orm.model import Model
   from coral_orm.fields import CharField, IntegerField, DateTimeField

   class YourModel(Model):
       name = CharField(max_length=100)
       age = IntegerField()
       created_at = DateTimeField()
   ```

3. Use your models to interact with the database:
   ```python
   # Create
   new_instance = YourModel(name="Example", age=25, created_at=datetime.now())
   new_instance.save()

   # Read
   instances = YourModel.filter(age=25)
   for instance in instances:
       print(instance.name)

   # Update
   instance = YourModel.get(name="Example")
   instance.age = 26
   instance.save()

   # Delete
   instance.delete()
   ```

4. Remember to close connections when your application shuts down:
   ```python
   DatabaseManager.close_all()
   ```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.
 
