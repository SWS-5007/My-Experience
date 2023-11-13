# Python - How to solve ReadTimeoutError on installing Python Packages?

When I install Python Packages, I am getting an error like below:

```
...
  File "E:\ServerProjects\Lib\site-packages\pip\_vendor\urllib3\response.py", line 560, in read
    with self._error_catcher():
  File "C:\Users\HOME\AppData\Local\Programs\Python\Python312\Lib\contextlib.py", line 155, in __exit__
    self.gen.throw(value)
  File "E:\ServerProjects\Lib\site-packages\pip\_vendor\urllib3\response.py", line 443, in _error_catcher
    raise ReadTimeoutError(self._pool, None, "Read timed out.")
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.

```

To Fix this error, I use this command

`sudo pip install --default-timeout=100 future`

And installed the packages again:

`pip install -r requirements.txt`
