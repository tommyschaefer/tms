---
layout: post
title: Maybe Ruby
---

This afternoon I was looking for a small Ruby project to practice with, and I
decided to build a `Maybe` implementation. Here's what I came up with...

```
module Maybe
  Just = Struct.new(:value) do
    def to_s
      value.to_s
    end

    def then(...)
      Just.new(value.then(...))
    end
  end

  Nothing = Class.new do
    def ==(other)
      other.is_a? Nothing
    end

    def to_s
      ""
    end

    def then(*)
      self
    end
  end

  module_function

  def just(value)
    Just.new(value)
  end

  def nothing
    Nothing.new
  end
end
```

Which can be used like so:

```
Animal = Struct.new(:name, :sound)

animals = [
  Animal.new("Pig", Maybe.just("oink")),
  Animal.new("Snail", Maybe.nothing),
  Animal.new("Cow", Maybe.just("moo")),
  Animal.new("Worm", Maybe.nothing),
  Animal.new("Dog", Maybe.just("woof"))
]

sounds = animals.map do |animal|
  animal.sound.then { _1.upcase + "!!" }.to_s
end

puts sounds

# =>
# OINK!!
#
# MOO!!
#
# WOOF!!
```

I likely wont reach for this often, if ever, but it was a really fun and helpful
exercise! I tend to create domain specific values when I need to do things like
this, but it also might be handy to have a generalized tool available too.
