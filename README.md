# Setuptools with Protobuf and GRPC compilation

Fork of setuptools-protobuf that adds GRPC compilation

## Dependencies

The plugin requires the external ``protoc`` executable that is part of the
[protobuf project](https://github.com/protocolbuffers/protobuf) to be present.
On Debian systems, this executable is shipped in the ``protobuf-compiler`` package.

If the ``protoc_version`` option is specified, the specified version of protoc
will be downloaded from github. When it is not specified, a ``protoc`` binary is
expected to be present in the environment. You can override the binary with the
PROTOC environment variable.

Optionally, it can also generate typing hints if the ``mypy`` extra is selected.

There is no separate ``install_proto`` command; generated files (e.g. \_pb2.py
files) are placed in the source tree and expected to be installed by other
install commands.

## Usage

You can configure `setuptools-protobuf-grpc` in either `setup.py`, `setup.cfg` or `pyproject.toml`.

### setup.py

```python
from setuptools_protobuf_grpc import Protobuf

setup(
...
    setup_requires=['setuptools-protobuf-grpc'],
    protobufs=[Protobuf('example/foo.proto')],
)
```

### setup.cfg

```ini
...

[options]
setup_requires =
    setuptools
    setuptools-protobuf-grpc
```

### pyproject.toml

```toml
[build-system]
requires = ["setuptools", "setuptools-protobuf-grpc"]

[tool.setuptools-protobuf-grpc]
protobufs = ["example/foo.proto"]

# Generate typing hints:
mypy = true

# Optionally, set the specific protoc version to use:
protoc_version = '25.1'
```

## GitHub actions

To install protoc in a GitHub action, you can use the
[setup-protoc](https://github.com/arduino/setup-protoc) action:

```yaml
- name: Install Protoc
  uses: arduino/setup-protoc@v2
```
