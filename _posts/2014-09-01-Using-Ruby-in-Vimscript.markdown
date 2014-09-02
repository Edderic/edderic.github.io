---
layout: default
---

Like programming in Ruby, editing in Vim, but don&#39;t enjoy writing in Vimscript as much?

While writing in markdown this week, I noticed that I was writing a lot of underline-style headers, and they were repetitive enough that I wanted to speed up the process through creating and using mappings. I wrote a Vimscript function that has most of it&#39;s innards in Ruby, because frankly, I am much more comfortable in Ruby.

One can make an H1-style header by writing a string of equal characters.

    Some H1-header
    ==============

Similarly, one can make H2-style headers by writing a string of underscores:

    I am an H2-header
    -----------------

The issue I wanted to address is that headers have variable lengths -- typing them manually by hand can be quite cumbersome. I wanted to make a snippet that dynamically generates underline-style headers, with lengths as long as the headers above them.  For example, the header &quot;Mary Had a Little Lamb&quot; has 22 characters. Therefore the underline (whether it be made of dashes or equal signs), should also be made of 22 characters.

    Mary Had a Little Lamb
    ----------------------

Here is the function I&#39;ve made in .vimrc

    function! AddCharStringAsLongAsHeaderString(char)
    ruby <<EOF
    {% highlight ruby %}
      character = Vim::evaluate('a:char')
      current_line = Vim::Buffer.current.line
      current_line.gsub(/\s*$/,'')
      current_line_length = current_line.length

      accumulated_string = '' + character * current_line_length

      Vim.command("execute 'normal! o#{accumulated_string}\e'")
    {% endhighlight %}
    EOF
    endfunction

As you can see, this is a Vimscript function that takes in an argument.  Inside the `ruby <<EOF` block is where Ruby is talking to Vim and vice versa.  `Vim::evaluate('a:char')` lets us evaluate the value of Vimscript function argument inside Ruby. We strip the extraneous spaces (if there are any). Then we generate the string of characters and pass that back to Vim via the the `Vim.command`.  Now we can do `:call AddCharStringAsLongAsHeaderString('-')` or `:call AddCharStringAsLongAsHeaderString('=')` to add dashes or equals signs accordingly. These calls can then be mapped to custom keyboard shortcuts in your .vimrc for faster editing.
