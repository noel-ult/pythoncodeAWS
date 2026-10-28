# Student registration with Flask, S3, and MySQL

A Flask demonstration that accepts student details and a photo, uploads the photo to S3, and inserts the student's name, email, course, and photo URL into MySQL.

## Request flow

`GET /` renders `templates/index.html`. `POST /register` accepts multipart fields `name`, `email`, `course`, and `photo`. It uploads the file using its original filename, then performs a parameterized insert into `students` and returns a success message.

## Prerequisites and configuration

Use Python 3.12 to match the Dockerfile, a reachable MySQL database, an S3 bucket, and AWS credentials available to boto3 through the runtime's credential mechanism.

The current `app.py` hardcodes the database connection and bucket. It does **not** read custom database environment variables or a `.env` file. Configure these values locally before starting; move credentials into runtime configuration before sharing a deployment. Existing committed credentials should be replaced and rotated. Never copy them into documentation or new commits.

The MySQL connection is opened during module import, so even loading `/` requires database connectivity. No schema migration is provided. The application's insert requires a `students` table containing writable `name`, `email`, `course`, and `photo_url` columns. This example creates a compatible table in a disposable development database:

```sql
CREATE TABLE students (
  id BIGINT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  course VARCHAR(255) NOT NULL,
  photo_url TEXT NOT NULL
);
```

## Local run

After configuring your own database and bucket:

```sh
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/python app.py
```

Open http://localhost:5000. On Windows, use `.venv\Scripts\python.exe` and its corresponding pip executable.

## Container

```sh
docker build -t student-registration .
docker run --rm -p 8000:8000 student-registration
```

The container runs Gunicorn on port **8000**, while `python app.py` uses **5000**. Provide AWS credentials to the container through your deployment's credential setup and ensure its database is reachable. The image does not provision S3 or MySQL.

## Verification and limitations

Use disposable records and photos to check the form, resulting database row, and uploaded object. A constructed S3 URL does not grant read access; bucket/object access determines whether a photo loads. Reusing a filename can overwrite an object. The S3 upload and MySQL insert are separate operations, so a failed insert may leave an uploaded object.

There is no authentication, upload validation, automated test suite, or infrastructure definition in this branch. Do not describe this demo as a complete production registration system.

## More documentation

- [Source, command, and configuration reference](docs/REFERENCE.md)
- [Contributing](CONTRIBUTING.md)

<!-- developer-handbook-20261028 -->
[Source reference](docs/REFERENCE.md) · [Verification and operations](docs/OPERATIONS.md)
<!-- /developer-handbook-20261028 -->
