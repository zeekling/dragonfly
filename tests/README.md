# System tests


## Pytest

The tests assume you have the "dragonfly" binary in `<root>/build-dbg` directory.
You can override the location of the binary using `DRAGONFLY_PATH` environment var.
### Before you start
Please make sure that you have python 3 installed on you local host.
If have more both python 2 and python 3 installed on you host, you can run the tests with the following command:
```
python3 -m pytest -xv dragonfly
```
It is advisable to use you python virtual environment: [python virtual environment](https://docs.python.org/3/library/venv.html).
To activate it, run:
```
source <virtual env name>/bin/activate
```
Then install all the required dependencies for the tests:
```
pip install -r dragonfly/requirements.txt
```
### Running the tests
to run pytest, run:
`pytest -xv dragonfly`

## Writing tests
The [Getting Started](https://docs.pytest.org/en/7.1.x/getting-started.html) guide is a great resource to become familiar with writing pytest test cases.

Pytest will recursively search the `tests/dragonfly` directory for files matching the patterns `test_*.py` or `*_test.py` for functions matching these [rules](https://docs.pytest.org/en/7.1.x/explanation/goodpractices.html#conventions-for-python-test-discovery):
- Functions or methods outside of a class prefixed by `test`
- Functions or methods prefixed by `test` inside a class prefixed by `Test` (without an `__init__` method)

**Note**: When making a new directory in `tests/dragonfly` be sure to create an `__init__.py` file to avoid [name conflicts](https://docs.pytest.org/en/7.1.x/explanation/goodpractices.html#tests-outside-application-code)

### Interacting with Dragonfly
Pytest allows for parameters with a specific name to be automatically resolved through [fixtures](https://docs.pytest.org/en/7.1.x/explanation/fixtures.html) for any test function. The following fixtures are to be used to interact with Dragonfly when writing a test:
| Name  | Type | [Scope](https://docs.pytest.org/en/7.1.x/how-to/fixtures.html?highlight=scope#scope-sharing-fixtures-across-classes-modules-packages-or-session) | Description
| ----- | ---- | ----- | ----------- |
| tmp_dir | [pathlib.Path](https://docs.python.org/3/library/pathlib.html) | Session | The temporary directory the Dragonfly binary will be running in. The environment variable `DRAGONFLY_TMP` is also set to this value |
| test_env | `dict` | Session | The environment variables used when running Dragonfly as a dictionary |
| client | [redis.Redis](https://redis-py.readthedocs.io/en/stable/connections.html#generic-client) | Class | The redis client to interact with the Dragonfly instance |
| async_client | [aioredis.Redis](https://aioredis.readthedocs.io/en/latest/api/high-level/#aioredis.client.Redis) | Class | The async redis client to interact with the Dragonfly instance |

### Passing CLI commands to Dragonfly
To pass custom flags to the Dragonfly executable two class decorators have been created. `@dfly_args` allows you to pass a list of parameters to the Dragonfly executable, similarly `@dfly_multi_test_args` allows you to specify multiple parameter configurations to test with a given test class.

In the case of `@dfly_multi_test_args` each parameter configuration will create one Dragonfly instance which each test will receive a client to as described in the [above section](#interacting-with-dragonfly)

Parameters can use environmental variables with a formatted string where `"{<VAR>}"` will be replaced with the value of the `<VAR>` environment variable. Due to [current pytest limtations](https://github.com/pytest-dev/pytest/issues/349) fixtures cannot be passed to either of these decorators, this is currently the provided way to pass the temporary directory path in a CLI parameter.

### Test Examples
- **[snapshot_test](./dragonfly/snapshot_test.py)**: Example test using `@dfly_args`, environment variables and pre-test setup
- **[generic_test](./dragonfly/generic_test.py)**: Example test using `@dfly_multi_test_args`
- **[connection_test](./dragonfly/connection_test.py)**: Example for testing running with multiple asynchronous connections.

### Writing your own fixtures
The fixture functions located in [conftest.py](./dragonfly/conftest.py).
You can write your own fixture inside this file, as seem fit. Just make sure, before adding new fixture that there maybe one already written.
Try to make the fixture running at the smallest scope possible to ensure that the test can be independent of each other (this will ensure no side effect - match our policy of "share nothing").

### Managing test environment
Do forget to add any new dependency that you may created to [dragonfly/requirement.txt](./dragonfly/requirements.txt) file.
You can do so by running
```
pip3 freeze > requirements.txt 
```
from [dragonfly](./dragonfly/) directory.

# Integration tests
Integration tests are located in the `integration` folder.

To simplify running integration test each package should have its own Dockerfile. The Dockerfile should contain everything needed in order to test the package against Dragonfly. Docker can assume Dragonfly is running on localhost:6379.
To run the test:
```
docker build -t [test-name] -f [test-dockerfile-name] .
docker run --network=host [test-name]
```

## Node-Redis
Integration test for node-redis client.
Build:
```
docker build -t node-redis-test -f ./node-redis.Dockerfile .
```
Run:
```
docker run --network=host node-redis-test
```

to run only selected tests use:

```
docker run --network=host node-redis-test npm run test -w ./packages/client -- --redis-version=2.8 -g <regex>
```

In general, you can add this way any option from [mocha framework](https://mochajs.org/#command-line-usage).

## ioredis
Integration tests for ioredis client.
Build:
```
docker build -t ioredis-test -f ./ioredis.Dockerfile .
```
Run:
```
docker run --network=host mocha [options]
```
The dockerfile already has an entrypoint setup. This way, you can add your own arguments to the mocha command.

Example 1 - running all tests inside the `unit` directory:
```
docker run -it --network=host ioredis mocha "test/unit/**/*.ts"
```
Example 2 - running a single test by supplying the `--grep` option:
```
docker run -it --network=host ioredis mocha --grep "should properly mark commands as transactions" "test/unit/**/*.ts"
```

For more details on the entrypoint setup, compare the `ioredis.Dockerfile`
with the npm test script located on the `package.json` of the ioredis project.

## Jedis
Integration test for the Jedis client.
Build:
```
docker build -t jedis-test -f ./jedis.Dockerfile .
```
Run:
```
docker run --network=host jedis-test
```
