# Python3
Cheat sheet for Python 3

## Neat Tricks
### List operations 
* `list[ : n ]` does not include index `n`
* `list[ n : ]` includes index `n`
* `list1.extend([list2])` returns `None`
* `list1.extend(value)` returns `None`

## Equality operators
* `is` checks that 2 arguments refer to the same object (memory location)
* `==` checks that 2 arguments have the same value.

## Useful API

## Style Guide
[PEP8](https://www.python.org/dev/peps/pep-0008/) is a widely used style guide for Python. [Pycodestyle](https://pypi.python.org/pypi/pycodestyle/) is an automated style checker for PEP8. There is also a SublimeLinter plugin for it called [SublimeLinter-pycodestyle](https://github.com/SublimeLinter/SublimeLinter-pycodestyle).


## Changelog

### Important changes from Python 2 to 3
* `print var` is now a function and needs to be called with parentheses: `print(var)` 
* `xrange` is replaced by `range` . There is NO `xrange`
* `a, b, *rest = range(10) // a = 0, b = 1, rest = [2, 3, 4, .., 9]`
* `a, *rest, b = range(10) // a = 0, rest = [1, 2, .., 8], b = 9`
* Division
  * Floor division `5 // 2 = 2`
  * Whole number division (result in float) `5 / 2 = 2.5`
* Raising exceptions `raise NameError('message)'`
* Catching exceptions `except NameError as err:`
* For iterators have to call `next(generator_name)`
* For loop variables and the global namespace leak
* `TypeError` is raised as warning if we try to compare unorderable types.
* call `list(generator)` returns list from a generator
* Following functions return generator:
  * `zip()`
  * `map()`
  * `filter()`
  * `dictionary.keys()`
  * `dictionary.values()`
  * `dictionary.items()`
* Return directly from a generator `yield from gen()`
* `round` rounds `0.5` to the nearest even integer