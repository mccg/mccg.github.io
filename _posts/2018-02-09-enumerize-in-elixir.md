---
layout: post
title: "enumerize in elixir"
category: Dev
tags: ["elixir"]
date: 2018-02-09
comments: true

---
>**Summary**:
There's a need to define some struct's type and some logics are going to use it.
It's similar to [``enumerize``](https://github.com/brainspec/enumerize) gem in ruby and something like ``enum`` in C++.
On reflection, I found an approach to create a ``deftype`` macro.

## Functionality we need in elixir
- Assuming we defined a ``Browser`` module, which includes some types like "chrome", "firefox" and "edge".
- Similar functionality C++ codes:
  ```cpp
  struct Browser {
    enum class Type {
      Unknown = 0,
      Chrome = 1,
      Firefox = 2,
      Edge = 3
    };

    void handleSomething() {
      doSomething(Browser::Type::Firefox);
      doSomething(Browser::Type::Unknown);
    }
  };
  ```
- In elixir, I'd like to use ``Browser.Type.firefox`` as the value of browser's type:
  ```elixir
  defmodule Browser do
    defstruct type: Browser.Type.unknown, other_props: nil

    def handle_something() do
      do_something(Browser.Type.firefox)
      do_something(Browser.Type.unknown)
    end
  end
  ```
  Now, we have to finish the rest of the codes to make codes above work.

## To implement a ``deftype``
- Let's define a module ``Deftype``. Then let ``deftype`` define a new module.
  By using ``use Deftype.Use, unquote(opts)``,
  we are able to define macros inside "Type" module.

- ``deftype.ex``:
  ```elixir
  defmodule Deftype.Use do
    defmacro __using__(opts) do
      Enum.map opts, fn {k, v} ->
        quote do
          defmacro unquote(:"#{k}")() do
            unquote(v)
          end
        end
      end
    end
  end

  defmodule Deftype do
    defmacro deftype(module, opts) do
      quote do
        defmodule unquote(module) do
          use Deftype.Use, unquote(opts)
        end
      end
    end
  end
  ```
  Then we add codes into ``browser.ex``, so the completed file is:
  ```elixir
  import Deftype
  deftype Browser.Type,
    unknow: 0,
    chrome: 1,
    firefox: 2,
    edge: 3

  defmodule Browser do
    require Browser.Type

    defstruct type: Browser.Type.unknown, other_props: nil

    def handle_something() do
      do_something(Browser.Type.firefox)
      do_something(Browser.Type.unknown)
    end
  end
  ```
  It's a little bit inconvenient to require "XXXType" everytime you use it in a new module.
  On the bright side, code becomes more clean when you define enumeration.

