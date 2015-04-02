# File standards

This is a short and concise guide for keeping your text files sane while working
in a team.

It's language agnostic, and applies to any programming environment.
There are some language exceptions (like _golang_) that have their own
formatting tools, but this applies to the majority of text files.


### Remove trailing whitespace

Trailing whitespace can add a lot of noise to your work, making you spend more
time merging files you never touched.

Imagine a scenario where _Bob_ commits `main.m` with trailing whitespace.
_Alice_ is editing a completely different file, `constants.h`. She navigates
around the code, and her tools automatically strip whitespace from `main.m`.

By the time _Alice_ submits her PR, _Bob_ has edited `main.m` again.
Alice has to resolve merge conflicts on that file now, even though she never
touched it at the first place.

By now, you might be thinking "sure, it's Alice's fault... she should turn off
automatic whitespace trimming".
Well, this doesn't solve the other problem - you can always __add or remove__
whitespace __accidentally__, which will bring you to the same merge conflicts.


### Ensure a new line at the end of a file

UNIX tools expect your files to end with an empty line, and most of your high-level tools (like IDEs) are using them internally. Not ending your files
with a new line can make terminal outputs look bad, confuse scripts that concatenate, count lines, etc.

Here's a [Stack Overflow thread](http://stackoverflow.com/questions/729692/why-should-files-end-with-a-newline)
and a [Stack Exchange one](http://unix.stackexchange.com/questions/18743/whats-the-point-in-adding-a-new-line-to-the-end-of-a-file)
with a bunch of references. You should read them.


### Use spaces instead of tabs

People tend to use tabs for indenting the source code because everyone can set
their tab width to anything they like. The problem with this approach occurs
when people start aligning their lines by equals signs, colons, commas, etc.

The actual problem is that you start mixing tabs and spaces, and the following snippet
looks bad on two different settings:


The other problem occurs if Bob is using tabs and Alice uses spaces.
Even the simplest snippet of code looks awful if they have different tab widths:

``` ruby
# The upper two lines are indented using two spaces.
# Third line is indented using one tab

# Tab width = 2
def full_name(person)
  first_name = person.first_name.capitalize
  last_name  = person.last_name.capitalize
  "#{first_name} #{last_name}"
end

# Tab width = 4
def full_name
  first_name = person.first_name.capitalize
  last_name  = person.last_name.capitalize
    "#{first_name} #{last_name}"
end
```

Languages have community standards. If your code adopts to them,
it won't be outstanding from the rest of open-source libraries you're using
and it'll be easier to read. For example, _Ruby_ prefers 2 spaces for
indentation, _Python_, _Javascript_, _Objective-C_ and many other languages 4.


### Charset

In the majority of cases, you want to use UTF-8. Many editors and IDEs will
automatically default to UTF-8, so you might be already using it.
It's always worth to double check.
At the end of the day, emoji are a pretty important part of a developer's life.


### .editorconfig

Most of today's editors have plugins that support [.editorconfig](http://editorconfig.org/)
files. These files are describing the rules defined above (and many more), and
you should consider adding one to your project.

When an editor sees the `.editorconfig` file, it'll override your personal
settings with the team's.
The cool part about `.editorconfig` is - you can override just certain files or
directories.


### The rest

There are a few more topics not required here, such as [line endings](https://en.wikipedia.org/wiki/Newline),
maximum line length, etc. These are a bit less important and usually language
specific.
