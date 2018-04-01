# jenkins-python
This is a jenkins project for python. This project requires pytest. pytest can be installed using below command.

[![Build Status](https://travis-ci.org/rpkharche/jenkins-python.svg?branch=master)](https://travis-ci.org/rpkharche/jenkins-python)
```
pip install -U pytest
```
## Sample tests below for main.py in tests
```python 
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```
## Following additional jenkins configuration is required in jenkins project for running tests and publishing Junit test reports
1. Jenkins Project -> configure-> build-> Add Build Step -> Execute windows batch command.
Enter below command. 
```
pytest --junitxml %WORKSPACE%/reports/results.xml %WORKSPACE%/tests/main.py
```
1. Jenkins Project -> configure-> Post Build Actions-> Add post-build Step -> Publish JUnit test result report
Enter following value in Test Report XMLS
```
reports/*.xml
```
