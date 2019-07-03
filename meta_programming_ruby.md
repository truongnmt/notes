# Ruby Rails

Created: Jun 25, 2019 4:06 PM
Updated: Jul 02, 2019 7:03 PM

# Metaprogramming

## The M Word

### Ghost town and marketplaces

Source code contains variables, classes, methods, ... this is *language constructs.*

In many programming language, after compiler has finished its job, thinks like variables, methods just locations in memory. Can't ask class for its instance methods. In language such as C++, runtime is a quite place, a ghost town.

Meanwhile in Ruby, runtime is more like a busy market place. Most language constructs are still there. 

> You can walk up to language construct and ask it question about itself. This is called introspection.

    class Movie < ActiveRecord::Base
    end
    
    movie = Movie.create
    movie.title = "Doctor Strange"
    movie.title   # => "Doctor Strange"

Movie#title and Movie#title = 

There methods are nowhere to be found in the source code. How can title and title= exist if they're not defined anywhere?

You can find out by looking how ActiveRecord works. First the table name is straight forward. AR looks at the name of the class through introspection and then applies some simple conventions. Class name is Movie, AR maps it to a table named movies. (The library know how to find plurals for English words)

What about methods? AR defines them automatically. AR reads the schema at runtime, discover that movies table has two columns name title and director. So that AR defines methods such as Movie#title and Movie#title= out of thin air while the program runs.

> Metaprogramming is writing code that manipulates language constructs at runtime

Code Generator vs Metap.

Code gen means that you use a program to generate or otherwise manipulate a second, distinct program - and then you run the second program.

## The Object Model

### Class Definition

    class D
    	def x; 'x'; end
    end
    
    class D
    	def y; 'y'; end
    end
    
    
    
    obj = D.new
    obj.x    # => "x"
    obj.y    # => "y"

When the previous code mention class D for the first time,