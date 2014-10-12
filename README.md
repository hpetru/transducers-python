# transducers-python

[Transducers](http://clojure.org/transducers) are composable algorithmic transformations. They are independent from the context of their input and output sources and specify only the essence of the transformation in terms of an individual element. Because transducers are decoupled from input or output sources, they can be used in many different processes - collections, streams, channels, observables, etc. Transducers compose directly, without awareness of input or creation of intermediate aggregates.

[Generators and Generator Functions](https://wiki.python.org/moin/Generators) are composable algorithmic transformations that return iterable, lazy sequences known as Generators. Due to the per-yield iteration of generators in composed form, generators provide a very similar path to input and output source decoupling to transducers. Specifically, transducers compose against the reducing function, ultimately applying their transformation to the x argument of a reducing function of parameters (r, x), in a recursive process. The Python generators defined here as arguments to reduce apply their transform per call from reduce to yield (x) in this context.

The transducers-python implementation is still compatible with Clojure style tranducers, but these must be composed with transducers.rcompose against the reducer argument to transducers.transduce.

For more information about Clojure transducers and transducer semantics see the introductory [blog post](http://blog.cognitect.com/blog/2014/8/6/transducers-are-coming) and this [video](https://www.youtube.com/watch?v=6mTbuzafcII).

## Installation

    pip install transducers ## other arguments TBD

## Documentation

[link](tbd)

## Usage

```python
import transducers as T
from operator import add
from fractions import Fraction

def geometric_series(a, r):
    power = 0
    yield a
    while True:
        power += 1
        yield a * r**power

T.transduce(T.compose(T.taking(3), T.mapping(float)),
            add,
            Fraction(0, 1),
            geometric_series(Fraction(1, 1), Fraction(1, 2)))

# > 1.75
```

For more examples of use, see the test suite tests/transducer_tests.py.

## Contributing

This library is open source, developed internally by [Cognitect](http://cognitect.com). Issues can be filed using [GitHub Issues](https://github.com/cognitect-labs/transducers-python/issues).

This project is provided without support or guarantee of continued development.
Because transducers-python may be incorporated into products or client projects, we prefer to do development internally and do not accept pull requests or patches.

## Copyright and License

Copyright © 2014 Cognitect

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
