API
===

.. module:: betamax

.. autoclass:: Betamax
    :members:

.. autoclass:: betamax.configure.Configuration
    :members:


Examples
--------

Let `example.json` be a file in a directory called `cassettes` with the 
content:

.. code:: javascript

    {
      "http_interactions": [
        {
          "request": {
            "body": "",
            "headers": {
              "User-Agent": "python-requests/v1.2.3"
            },
            "method": "GET",
            "uri": "https://httpbin.org/get"
          },
          "response": {
            "body": {
              "string": "example body",
              "encoding": "utf-8"
            },
            "headers": {},
            "status_code": 200,
            "url": "https://httpbin.org/get"
          }
        }
      ],
      "recorded_with": "betamax"
    }

The following snippet will not raise any exceptions

.. code:: python

    from betamax import Betamax
    from requests import Session


    s = Session()

    with Betamax(s, cassette_library_dir='cassettes') as betamax:
        betamax.use_cassette('example', record='none')
        r = s.get("https://httpbin.org/get")

On the other hand, this will raise an exception:

.. code:: python

    from betamax import Betamax
    from requests import Session


    s = Session()

    with Betamax(s, cassette_library_dir='cassettes') as betamax:
        betamax.use_cassette('example', record='none')
        r = s.post("https://httpbin.org/post",
                   data={"key": "value"})