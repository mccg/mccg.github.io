---
layout: post
title: "enumerize in elixir"
category: Dev
tags: ["elixir"]
date: 2018-02-09
comments: true

---

>**Summary**:
There is a need to define a ``struct``'s type, then some logic will use it.
The concept is similar to [``enumerize``](https://github.com/brainspec/enumerize) gem in ruby and something like ``enum`` in C++.
However, ``Enum`` in elixir is a module that related to enumerable things.
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
- In elixir, I'd like to use format like ``Browser.Type.firefox`` as the value of browser's type:
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
- First, by using ``use Deftype.Use, unquote(opts)``,
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
  Let's use ``deftype`` in practice.
  After adding codes into ``browser.ex``, the completed file should be:
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
  Don't forget to require "XXXType" eachtime you use it in a new module.
  Now, code becomes more clean when you define enumeration.
  By this way, you don't have to define function or macro anymore to declare something's type.

