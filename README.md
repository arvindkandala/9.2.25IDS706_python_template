# 9.2.25IDS706_python_template
First I created a new repository with a README file

Then I made these:
  hello.py — simple demo functions (say_hello, add)
  test_hello.py — unit tests with pytest  
  Makefile — one-line commands for install, test, lint, format, clean
  requirements.txt — pinned dev dependencies


The project structure looks like this:
.
├── hello.py
├── test_hello.py
├── Makefile
├── requirements.txt
└── .github/
    └── workflows/
        └── python.yml

I then set up a virtual environment to code in:
  python3 -m venv ~/.IDS706_python_template
  source ~/.IDS706_python_template/bin/activate

I then put some utilities inside my Makefile:
  install:
  	pip install --upgrade pip &&\
  		pip install -r requirements.txt
  
  format:
  	black *.py
  
  lint:
  	flake8 hello.py
  
  test:
  	python -m pytest -vv --cov=hello test_hello.py
  
  clean:
      rm -rf __pycache__ .pytest_cache .coverage
  
  all: install format lint test


I put my dependencies in my requirements.txt file:
  pylint
  flake8
  pytest
  click
  black
  pytest-cov

I then ran:
  make install



I then inputed code in my hello.py
  #function that says hello
  def say_hello(name: str) -> str:
      """Return a greeting message to students in the IDS class."""
      return f"Hello, {name}, welcome to Data Engineering Systems (IDS 706)!"
  
  #function that adds integers together
  def add(a: int, b: int) -> int:
      """Return the sum of two numbers."""
      return a + b



I then created a file to test hello.py, checking that the say_hello and add functions work as needed:

  from hello import say_hello, add
  
  def test_say_hello():
      assert (
          say_hello("Annie")
          == "Hello, Annie, welcome to Data Engineering Systems (IDS 706)!"
      )
  
  def test_add():
      assert add(2, 3) == 5


I then ran the following to test, format, lint, and clean my code:
  make test
  make format
  make lint
  make clean


I then committed and pushed my changes to GitHub:
  git add .
  git commit -m "Initial commit with Python template setup"   
  git push origin main

Then I enables Github Actions:
  name: Python Template for IDS706

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: '3.11'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Lint with flake8
      run: flake8 hello.py
    - name: Run tests
      run: pytest --cov=hello



Usage examples:

run "make test" in terminal

example output:
tests/test_hello.py::test_say_hello PASSED
tests/test_hello.py::test_add PASSED
---------- coverage: platform linux, python 3.11 ----------
Name      Stmts   Miss  Cover
-----------------------------
hello.py      6      0   100%


Very useful for developing and testing code for all softwares!
