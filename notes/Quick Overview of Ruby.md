https://paper.dropbox.com/doc/Intro-to-Ruby--AL4HGItw1LYbAcjGv4Wn~s5YAg-Qfk1WmqVWFnpm17c4EWZc#:uid=153219621954509491819747&h2=Syntax

# Intro to Ruby

----------


## Description

“A programmer’s best friend”, ruby is a perfectly object-oriented language. On it’s own, you need one of the following editors to write Ruby script:


- [VIM](http://vim.sourceforge.net/) (Vi IMproved) is a very simple text editor. This is available on almost all Unix machines and now Windows as well. Otherwise, your can use your favorite vi editor to write Ruby programs.
- [RubyWin](https://homepage1.nifty.com/markey/ruby/rubywin/index_e.html) is a Ruby Integrated Development Environment (IDE) for Windows.
- Ruby Development Environment [(RDE)](https://homepage2.nifty.com/sakazuki/rde_en/) is also a very good IDE for windows users.


## Syntax

File extension - **.rb**

**Hello World in Ruby**

    #!/usr/bin/ruby -w
    
    puts "Hello, Ruby!";

**puts** stdouts to console

**Whitespace**

    a + b #interpreted as a+b ( Here a is a local variable)
    a  +b #interpreted as a(+b) ( Here a is a method call)

**BEGIN and END**

    BEGIN {
       code1
    }
    
    code2
    
    END {
       code3
    }
    
    # Order is code 1, code 2, code 3

Code in **BEGIN** will always execute first and code in **END** will always execute last.

**Comments**

    # This is a comment.

**Methods**
You do not have to explicitly return in Ruby.


## Resources

The following link contains all other info regarding standard Ruby syntax. This should be easy to pick up on since Ruby has the standard OOP structure.
https://www.tutorialspoint.com/ruby/index.htm

