# Rstfilter

This tool prints a Ruby script with execution results.

```
$ cat sample.rb
a = 1
b = 2
c = a + b
puts "Hello" * c

$ rstfilter sample.rb -a
a = 1                                              #=> 1
b = 2                                              #=> 2
c = a + b                                          #=> 3
puts "Hello" * c                                   #=> nil
#out: HelloHelloHello
```

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'rstfilter'
```

And then execute:

    $ bundle install

Or install it yourself as:

    $ gem install rstfilter

## Usage

```
Usage: rstfilter [options] SCRIPT
    -c, --comment                    Show result only on comment
    -o, --output                     Show output results
    -d, --decl                       Show results on declaration
        --no-exception               Do not show exception
    -a, --all                        Show all results/output
        --pp                         Use pp to represent objects
        --comment-indent=NUM         Specify comment indent size (default: 50)
        --verbose                    Verbose mode
```

## Implementation

With parser gem, rstfilter translates the given script and run it.

For example, the first example is translated to:

```ruby
(a = (1).__rst_record__(1, 5)).__rst_record__(1, 5)
(b = (2).__rst_record__(2, 5)).__rst_record__(2, 5)
(c = (a + b).__rst_record__(3, 9)).__rst_record__(3, 9)
(puts "Hello" * c).__rst_record__(4, 16)
```

and `__rst_record__` method records the results. After that, rstfilter prints the script with the results.
`--verbose` option shows the translated script and collected results.

## Contribution

Bug reports and pull requests are welcome on GitHub at https://github.com/ko1/rstfilter.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).