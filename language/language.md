!SLIDE
# Language Changes #

!SLIDE center
## current directory is no longer in load path ##

    @@@ ruby
    require_relative

!SLIDE smaller bullets
# instance_exec #
* instance_eval with arguments


!SLIDE
# Arity checking on lambda #

    @@@ ruby
    def hello &block
      yield "hello"
    end

     x = lambda { puts "ha ha" }
     hello &x
     
!SLIDE
# Blocks can accept block arguments #

    @@@ ruby
    def hello &block
      block.call { puts "oh boi"}
    end

    hello { |&b| puts "hi there" }

!SLIDE bullets incremental

* Encoding
* New lambda syntax
* New hash syntax








