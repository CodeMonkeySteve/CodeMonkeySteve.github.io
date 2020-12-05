---
title: String Conversions in Ruby
tags: [ruby]
---
Here’s a tip so simple and elegant it’s amazing I ever got along without it. Consider `String#to_f`:

```ruby
--> '12.34'.to_f
==> 12.34
```
Which works great, so long as the string is a valid number, but if not:

```ruby
--> 'splat'.to_f
==> 0.0
```

`#to_f` doesn’t throw an exception with invalid input, making it dangerous to use with any user-supplied data. I’ve seen various solutions that involve regular expressions, but these are kludgy and don’t handle all proper numeric representations.

Fortunately, Ruby provides type-cast-style methods to do proper conversions with validation:

```ruby
--> Float('12.34')
==> 12.34
--> Float('splat')
ArgumentError: invalid value for Float(): "splat"
```

It might look weird, until you realize that `Float` is both a class (`::Float`) and a kernel method (`Kernel.Float`). There are also methods for converting to an `Integer`, `Array`, or even back to a `String` (which is essentially just `#to_s`).
