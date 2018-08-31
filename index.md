# Test-driven Flask tutorial

**TL;DR:** Maybe you already know about the new [Flask Mega Tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) by Miguel Grinberg, probably one of the best tutorials ever written about Flask. And there also is his awesome book "Flask web development", which is now updated to Flask 1.x in it's 2nd edition, where you learn to build a social blog application called flasky from scratch.
What you definitely know is the official Flask tutorial, in which you also build a blog app called Flaskr. Somebody had the great idea to rewrite this official tutorial in the test-driven way calling it [flaskr-tdd](https://github.com/mjhea0/flaskr-tdd). This is my attempt to rewrite flasky in test-driven style.

**DISCLAIMER:** I am no flask expert, not even a professional programmer at all. I'm learning flask and like to share my experience about that. And what is worse, English is not my first language (as you definitely noticed already). Any improvements concerning my human and programming language used in this blog are appreciated. Just send a PR.
I also have no personal or financial relationship with Miguel Grinberg, I only deeply admire his work. So if you should decide to buy a book about Flask, pick the one above and be happy.

OK, let's go!

## 1. Get your tools

Maintaining a clean python environment has been a source of frustration in the past, so we're using `pipenv`, the latest approach managing dependencies more easily.

```shell
pip install pipenv --user
mkdir flasky-tdd
cd flasky-tdd
pipenv install flask
pipenv install pytest pytest-cov --dev
```


