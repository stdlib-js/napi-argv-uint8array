<!--

@license Apache-2.0

Copyright (c) 2022 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->

# argv_uint8array

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Convert a Node-API value to an unsigned 8-bit integer array.

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- Package usage documentation. -->

<section class="installation">

## Installation

```bash
npm install @stdlib/napi-argv-uint8array
```

</section>

<section class="usage">

## Usage

```javascript
var headerDir = require( '@stdlib/napi-argv-uint8array' );
```

#### headerDir

Absolute file path for the directory containing header files for C APIs.

```javascript
var dir = headerDir;
// returns <string>
```

</section>

<!-- /.usage -->

<!-- Package usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- Package usage examples. -->

<section class="examples">

## Examples

```javascript
var headerDir = require( '@stdlib/napi-argv-uint8array' );

console.log( headerDir );
// => <string>
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="usage">

### Usage

```c
#include "stdlib/napi/argv_uint8array.h"
```

#### stdlib_napi_argv_uint8array( env, value, \*\*data, \*length, \*message, \*err )

Converts a Node-API value to an unsigned 8-bit integer array.

```c
#include "stdlib/napi/argv_uint8array.h"
#include <node_api.h>
#include <stdint.h>

static napi_value addon( napi_env env, napi_callback_info info ) {
    napi_value value;

    // ...

    uint8_t *X;
    int64_t len;
    napi_value err;
    napi_status status = stdlib_napi_argv_uint8array( env, value, &X, &len, "Must be a typed array.", &err );
    assert( status == napi_ok );
    if ( err != NULL ) {
        assert( napi_throw( env, err ) == napi_ok );
        return NULL;
    }

    // ...
}
```

The function accepts the following arguments:

-   **env**: `[in] napi_env` environment under which the function is invoked.
-   **value**: `[in] napi_value` Node-API value.
-   **data**: `[out] uint8_t**` pointer for returning a reference to the output array.
-   **length**: `[out] int64_t*` pointer for returning the number of array elements.
-   **message**: `[in] char*` error message.
-   **err**: `[out] napi_value*` pointer for storing a JavaScript error. If not provided a number, the function sets `err` with a JavaScript error; otherwise, `err` is set to `NULL`.

```c
napi_status stdlib_napi_argv_uint8array( const napi_env env, const napi_value value, uint8_t **data, int64_t *length, const char *message, napi_value *err );
```

The function returns a `napi_status` status code indicating success or failure (returns `napi_ok` if success).

#### STDLIB_NAPI_ARGV_UINT8ARRAY( env, X, len, argv, index )

Macro for converting an add-on callback argument to an unsigned 8-bit integer array.

```c
#include "stdlib/napi/argv_uint8array.h"
#include "stdlib/napi/argv.h"
#include <node_api.h>
#include <stdint.h>

static void fcn( const uint8_t *X, const int64_t xlen, uint8_t *Y, const int64_t ylen ) {
    int64_t len;
    int64_t i;

    if ( xlen > ylen ) {
        len = ylen;
    } else {
        len = xlen;
    }
    for ( i = 0; i < len; i++ ) {
        Y[ i ] = X[ i ];
    }
}

// ...

static napi_value addon( napi_env env, napi_callback_info info ) {
    // Retrieve add-on callback arguments:
    STDLIB_NAPI_ARGV( env, info, argv, argc, 2 );

    // Convert the first argument to a C type:
    STDLIB_NAPI_ARGV_UINT8ARRAY( env, X, xlen, argv, 0 );

    // Convert the second argument to a C type:
    STDLIB_NAPI_ARGV_UINT8ARRAY( env, Y, ylen, argv, 1 );

    // ...

    fcn( X, xlen, Y, ylen );
}
```

The macro expects the following arguments:

-   **env**: environment under which the callback is invoked.
-   **X**: output variable name for the array.
-   **len**: output variable name for the array length.
-   **argv**: name of the variable containing add-on callback arguments.
-   **index**: argument index.

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section to include cited references. If references are included, add a horizontal rule *before* the section. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="references">

</section>

<!-- /.references -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2023. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/napi-argv-uint8array.svg
[npm-url]: https://npmjs.org/package/@stdlib/napi-argv-uint8array

[test-image]: https://github.com/stdlib-js/napi-argv-uint8array/actions/workflows/test.yml/badge.svg?branch=v0.0.1
[test-url]: https://github.com/stdlib-js/napi-argv-uint8array/actions/workflows/test.yml?query=branch:v0.0.1

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/napi-argv-uint8array/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/napi-argv-uint8array?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/napi-argv-uint8array.svg
[dependencies-url]: https://david-dm.org/stdlib-js/napi-argv-uint8array/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://gitter.im/stdlib-js/stdlib/

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/napi-argv-uint8array/main/LICENSE

</section>

<!-- /.links -->
