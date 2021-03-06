formencode_jsonschema
=====================

Converts [formencode](http://www.formencode.org/en/latest/)'s schema to
[JSON Schema](http://json-schema.org/)
using [Marshmallow](https://marshmallow.readthedocs.org/en/latest/).

[![PyPI version](https://badge.fury.io/py/formencode_jsonschema.svg)](https://badge.fury.io/py/formencode_jsonschema)
[![Build Status](https://travis-ci.org/Hardtack/formencode_jsonschema.svg?branch=master)](https://travis-ci.org/Hardtack/formencode_jsonschema)
[![Documentation Status](https://readthedocs.org/projects/formencode-jsonschema/badge/?version=latest)](http://formencode-jsonschema.readthedocs.org/en/latest/?badge=latest)

How to use it
-------------

You can use it like this.

```python
>>> from myproject.schemas import SomeFormencodeSchema
>>> from formencode_jsonschema import JSONSchema
>>> json_schema = JSONSchema()
>>> formencode_schema = SomeFormencodeSchema()
>>> result = json_schema.dump(formencode_schema)
>>> result.data
{
	"type": "object",
	"required": ["foo", ...],
    "properties": {
    	"foo": {
        	"type": "string"
        },
        "bar": ...
    }
}
```

Typed validator
---------------

You can explicitly define validator as JSON typed validator.

```python
from formencode import Schame, validators as v
from formencode_jsonschema import typed, JSONSchema


class SomeFormencodeSchema(Schema):
    foo = typed.BooleanTyped(v.UnicodeString(), required=False)
    bar = typed.JSONTyped({
    	"type": "string",
    }, v.Int())
```

```python
>>> json_schema = JSONSchema()
>>> formencode_schema = SomeFormencodeSchema()
>>> result = json_schema.dump(formencode_schema)
>>> result.data
{
	"type": "object",
	"required": ["bar"],
    "properties": {
    	"foo": {
        	"type": "boolean"
        },
        "bar": {
        	"type": "string"
        }
    }
}
```

Documentation
-------------

Document of formencode_jsonshcmea is hosted on [RTD](http://formencode-jsonschema.readthedocs.org/).
