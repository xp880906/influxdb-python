## InfluxDB-Python-Aio
--------------

.. image:: https://travis-ci.org/influxdata/influxdb-python.svg?branch=master
    :target: https://travis-ci.org/influxdata/influxdb-python
.. image:: https://readthedocs.org/projects/influxdb-python/badge/?version=latest&style
    :target: http://influxdb-python.readthedocs.org/
    :alt: Documentation Status

.. image:: https://img.shields.io/coveralls/influxdata/influxdb-python.svg
  :target: https://coveralls.io/r/influxdata/influxdb-python
  :alt: Coverage

.. image:: https://img.shields.io/pypi/v/influxdb.svg
   :target: https://pypi.org/project/influxdb-aio/
   :alt: PyPI Status

--------------

### Statement
**This was forked from (https://github.com/influxdata/influxdb-python), and support asyncio.**<br/>
[Here](README.original.rst) is the original README document. You can find more detail about InfluxDB-Python (client) and also influxdb (database). Here is only some difference and basic usage.

InfluxDB-Python is a client for interacting with InfluxDB_.

Development of this library is maintained by:

| Github ID| URL |
| --- | --- |
| @aviau | (https://github.com/aviau) |
| @xginn8 | (https://github.com/xginn8) |
| @sebito91 | (https://github.com/sebito91) |

### Installation

Install, upgrade and uninstall influxdb-aio with these commands::

    $ pip install influxdb-aio
    $ pip install --upgrade influxdb-aio
    $ pip uninstall influxdb-aio

### Dependencies

The influxdb-python distribution is supported only on Python 3.6, 3.7, etc.


Main dependency is:

- httpx: A next generation HTTP client for Python. (https://github.com/encode/httpx)


### Examples
--------

Here's a basic example (for more see the examples directory)

    ~~~python
    import asyncio
    from influxdb_aio import InfluxDBClient

    json_body = [
        {
            "measurement": "cpu_load_short",
            "tags": {
                "host": "server01",
                "region": "us-west"
            },
            "time": "2009-11-10T23:00:00Z",
            "fields": {
                "value": 0.64
            }
        }
    ]

    async def init_client():
        client = await InfluxDBClient('localhost', 8086, 'root', 'root', 'example')
        await client.create_database('example')
        return client.write_points(json_body)


    async def main():
        client = await init_client()
        result = await client.query('select value from cpu_load_short;')
        print("Result: {0}".format(result))


    if __name__ == '__main__' :
        asyncio.get_event_loop().run_until_complete(main())
    ~~~
