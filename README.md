# ![hashids](https://avatars1.githubusercontent.com/u/8481000?v=3&s=200 "Hashids")

Hashids
=======
[![Build status](https://travis-ci.org/snaiper80/hashids-erlang.svg "Build status")](https://travis-ci.org/snaiper80/hashids-erlang)

The [Erlang][1] port of [Hashids][2] from JavaScript.

  [1]: http://www.erlang.org/
  [2]: http://www.hashids.org/


## Installation

Add Hashids as a dependency to rebar.config
```erlang
{deps,
    [
        {hashids, ".*",  {git, "git://github.com/snaiper80/hashids-erlang.git",  {tag, "1.0.4"}}}
    ]
}.
```

## Usage

Hashids encodes a integer or a list of integers.

```erlang
1> hashids:new().   % create a new hashids context with default options
{hashids_context,"this is my salt",8,
                 "5N6y2rljDQak4xgzn8ZR1oKYLmJpEbVq3OBv9WwXPMe7",
                 "UHuhtcITCsFifS","AdG0"}

2> hashids:new([]). % same as new/0
{hashids_context,"this is my salt",8,
                 "5N6y2rljDQak4xgzn8ZR1oKYLmJpEbVq3OBv9WwXPMe7",
                 "UHuhtcITCsFifS","AdG0"}

3> Ctx = hashids:new([{salt, "this is my salt"}, {min_hash_length, 8}]).
{hashids_context,"this is my salt",8,
                 "5N6y2rljDQak4xgzn8ZR1oKYLmJpEbVq3OBv9WwXPMe7",
                 "UHuhtcITCsFifS","AdG0"}

4> Encoded = hashids:encode(Ctx, 12345).
"B0NkK9A5"

5> Encoded2 = hashids:encode(Ctx, [12345, 6789]).
"Y9awcOLv"
```

decode/2 returns a list of numbers

```erlang
6> hashids:decode(Ctx, Encoded).
[12345]

7> hashids:decode(Ctx, Encoded2).
[12345,6789]
```

You can use customized characters (least 16 characters long)

```erlang
Ctx = hashids:new([{salt, "this is my salt"},
                   {min_hash_length, 8}, {default_alphabet, "ABCDEFGhijklmn34567890-:"}]).
```

## License

This software is licensed under [the MIT license](LICENSE).
