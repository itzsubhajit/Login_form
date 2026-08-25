# Flask Login Page

A simple Flask app with a styled login form — animated gradient background, glowing heading text, and a bounce effect on the sign-in button.

## Features

- Clean, dark UI built with plain HTML/CSS (no frontend framework required)
- Subtle animated background shift
- Glowing text effect on the heading
- Bounce micro-interaction on the submit button
- Success/error message banner driven by the Flask `message` variable

## Project structure

```
.
├── app.py
├── templates/
│   └── login.html
└── README.md
```

## Requirements

- Python 3.8+
- Flask

## Setup

1. Clone the repository

   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```

2. (Recommended) Create and activate a virtual environment

   ```bash
   python -m venv venv
   source venv/bin/activate      # macOS / Linux
   venv\Scripts\activate         # Windows
   ```

3. Install dependencies

   ```bash
   pip install flask
   ```

4. Run the app

   ```bash
   python app.py
   ```

5. Open your browser at [http://127.0.0.1:5000](http://127.0.0.1:5000)

## How it works

`app.py` currently hardcodes the credentials (`Admin` / `1234`) and passes a `message` string to `login.html` indicating whether the login was successful. The template checks for the word "successful" in that message to decide whether to show a green success banner or a red error banner.

```python
@app.route('/')
def login():
    username = "Admin"
    password = "1234"
    if username == "Admin" and password == "1234":
        message = "Login successful!"
    else:
        message = "Login failed!"
    return render_template('login.html', message=message)
```

> **Note:** The form in `login.html` currently posts to `/`, but the route doesn't yet read `request.form['username']` / `request.form['password']`. To make the form actually authenticate submitted credentials, update the route to accept `POST` requests and read the form data, for example:
>
> ```python
> from flask import request
>
> @app.route('/', methods=['GET', 'POST'])
> def login():
>     message = ""
>     if request.method == 'POST':
>         username = request.form.get('username')
>         password = request.form.get('password')
>         if username == "Admin" and password == "1234":
>             message = "Login successful!"
>         else:
>             message = "Login failed!"
>     return render_template('login.html', message=message)
> ```

## Disclaimer

This is a demo/learning project. Credentials are hardcoded and there is no session management, password hashing, or CSRF protection — **do not use this as-is in production**.

## License

MIT — feel free to use and modify.
