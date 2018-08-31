# Test-driven Flask tutorial

**TL;DR:** Maybe you already know about the new [Flask Mega Tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) by Miguel Grinberg, probably one of the best tutorials ever written about Flask. And there also is his awesome book "Flask web development", which is now updated to Flask 1.x in it's 2nd edition, where you learn to build a social blog application called flasky from scratch.
What you definitely know is the official Flask tutorial, in which you also build a blog app called Flaskr. Somebody had the great idea to rewrite this official tutorial in the test-driven way calling it [flaskr-tdd](https://github.com/mjhea0/flaskr-tdd). This is my attempt to rewrite flasky in test-driven style.

**DISCLAIMER:** I am no flask expert, not even a professional programmer at all. I'm learning flask and like to share my experience about that. And what is worse, English is not my first language (as you definitely noticed already). Any improvements concerning my human and programming language used in this blog are appreciated. Just send a PR.
I also have no personal or financial relationship with Miguel Grinberg, I only deeply admire his work. So if you should decide to buy a book about Flask, pick the one above and be happy.

OK, let's go!

## 1. Get your tools

- pipenv
- flask (of course)
- pytest, pytest-cov

Maintaining a clean python environment has been a source of frustration in the past, so we're using `pipenv`, the latest approach managing dependencies more easily. Pytest is just as modular as Flask with it's powerful fixture system and it is using Python's `assert`-statement, the most pythonic way of testing ever (IMHO). In TDD we surely want test coverage, so we install the pytest-cov plugin too.

```shell
pip install pipenv --user
mkdir flasky-tdd
cd flasky-tdd
pipenv install flask
pipenv install pytest pytest-cov --dev
```

Now we got app- & dev-dependencies nicely handled by a single *Pipfile*, no need for a separate *requirements-dev.txt*.

## 2. Test driving your Flask app

Most of you know the steps of TDD, I repeat them briefly:

1. Write a failing unit-test
2. Make it pass (somehow)
3. Refactor (make it good)

### Application structure

In the 1st step I do what I shouldn't: I skip step 2 for some reasons. I could present you the hello world few liner one file app from the official docs, but this has some shortcommings when testing comes in: The app-object is already created, but we want a fresh app instance for every single test, right? The solution is to move the creation of the flask app into a so called 'factory function'. 
We also want distinct parts of the app like user-authentication to be reusable, therefore we use blueprints. And finally we want different configurations for production, testing and development to be created dynamically at runtime.
This forced us to write some boilerplate right from the start (5 dirs & 8 files), but this will definitely pay off later. Fortunately each file only contains a few lines of code.

```shell
touch conftest.py
mkdir tests
```

Create tests/test_base.py with
```python
from flask import current_app


def test_app_exists(client):
    assert current_app
```
First we test if an instance of our app was successfully created. Now run `pytest` in the virtualenv, it should fail:
```shell
pipenv shell
pytest
```

