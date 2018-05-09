# clojure-cheatsheet

### Create a new Clojure project

```bash
lein new app project-name
```

### Run the project

```bash
lein run
```

### Build a standalone Clojure project

Build a standalone file that you can execute with Java.

```bash
lein uberjar
```

This command creates a file `target/uberjar/project-name-0.1.0-SNAPSHOT-standalone.jar`

### Run the standalone file built from a Clojure project

```bash
java -jar target/uberjar/project-name-0.1.0-SNAPSHOT-standalone.jar
```

### Run REPL

```bash
lein repl
```

### Truthy and Falsey values

In Clojure only two values are *Falsey*: `false` and `nil`.

The whole rest of values are *Truthy*.

### Function Calls, Macro Calls, and Special Forms

*Function Calls* are expressions that have a function expression as the operator.

*Macro Calls*?

*Special Forms*, unlike *Function Calls*, don't always evaluate all of their operands. 

### Built-in functions

#### `doc` - display documentation of given function

```clojure
(doc +)
```

#### Add

```clojure
(+ 1 2 3)
; => 6
```

#### Subtract

```clojure
(- 32 2)
; => 30
```

#### Divide

```clojure
(/ 8 3)
; => 8/3
```

#### Multiply

```clojure
(* 9 -4)
; => -36
```

#### Return first item in the collection

```clojure
(first [3 6 9])
; => 3
```

#### Concatenate strings

```clojure
(str "abc" "QWE" "123")
; => "abcQWE123"
```

#### `if` - general structure

```clojure
(if boolean-form
  then-form
  optional-else-form)
```

`if` returns a value returned by `then-form` or `optional-else-form`,
depending on `boolean-form` value. If you don't provide `optional-else-form`
and `boolean-form` returns `false`, then `if` returns `nil`.

#### `do` - *wrap up* multiple forms and run each of them

```clojure
(do (println "Qwerty")
  99)
; print line "Qwerty"
; return value 99
```

#### `when` - general structure

Use it if you want to do multiple things when `boolean-form` is `true`,
and always want to return `nil` when `boolean-form` is `false`.

```clojure
(when boolean-form
  then-form1
  then-form2
  then-form3
  then-form...)
```

#### `nil?` - return `true` if `nil` else return `false`

```clojure
(nil? nil)
; => true
```

```clojure
(nil? 214)
; -> false
```

#### `=` - return `true` if all given args are equal, else return `false`

```clojure
(= 1 2 1 1 2)
; => false
```

```clojure
(= 1 1 1)
; => true
```

#### `or` - return either the first *truthy* value or the last value

```clojure
(or nil false :my-little-key :my-second-key)
; => :my-little-key
```

```clojure
(or (= 1 2) nil false)
; => false
```

```clojure
(or false nil)
; => nil
```

```clojure
(or nil)
; => nil
```

#### `and` - return the first *falsey* value or, if no values are *falsey*, the last *truthy* value

```clojure
(and :background-color :foreground-color)
; => :foreground-color
```

```clojure
(and :font-color nil (or false))
; => nil
```

```clojure
(and false)
; => false
```

#### `hash-map` - return a *hash-map* built with given arg-pairs

```clojure
(hash-map :add + :sub - :div / :mul *)
; => {:add ... :sub ... :div ... :mul ...}
```

#### `get` - return the value mapped to key, otherwise return `nil`

```clojure
(get {:a 1 :b 2} :b)
; => 2
```

```clojure
(get {:a 1 :b 2} :c)
; => nil
```

#### `get-in` - look up values in nested maps

```clojure
(get-in {:a 1 :b {:x "xxx" :y "yyy"}} [:b :x])
; => "xxx"
```

#### Look up a value in a map by treating the map like a function

```clojure
({:a 1 :b 2} :a)
; => 1
```

#### Look up a value in a map by treating a keyword like a function

```clojure
(:a {:a 1 :b 2})
; => 1
```

#### `get` - return *n*th element of a vector

```clojure
(get [1 2 3] 0)
; => 1
```

#### `vector` - return a vector built with given args

```clojure
(vector 1 "asf" 4.3)
; => [1 "asf" 4.3]
```

#### `conj` - append an element to a vector

```clojure
(conj [1 2 3] 4)
; => [1 2 3 4]
```

#### `list` - return a list built with given args

```clojure
(list 1 "two" {3 4})
; => (1 "two" {3 4})
```

#### `nth` - get an element from a list

```clojure
(nth '(:a :b :c) 0)
; => :a
```

#### `conj` - prepend an element to a list

```clojure
(conj '(1 2 3) 4)
; => (4 1 2 3)
```

#### `hash-set` - return a hash-set built with given args

```clojure
(hash-set 1 1 2 1 21 1)
; => #{1 21 2}
```

#### `conj` - add a value to a hash-set

```clojure
(conj #{:a :b} :c)
; => #{:c :b :a}
```

```clojure
(conj #{:a :b} :b)
; => #{:b :a}
```

#### `set` - create a hash-set from a list or vector

```clojure
(set [1 2 1 1 3 2])
; => #{1 3 2}
```

#### `contains?`

```clojure
(contains? #{:a :b} :a)
; => true
```

```clojure
(contains? #{:a :b} :c)
; => false
```

#### Look up a value in a hast-set by treating a keyword like a function

```clojure
(:a #{:a :b})
; => :a
```

```clojure
(:c #{:a :b})
; => nil
```

#### `get` - return a value from a hash-set, else return `nil`

```clojure
(get #{:a :b} :a)
; => :a
```

```clojure
(get #{:a :b} :c)
; => nil
```

Confusing (because in this example `get` always returns `nil`):

```clojure
(get #{:a nil} nil)
; => nil
```

#### `inc` - increment by 1

```clojure
(inc 1.1)
; => 2.1
```

#### `map`

```clojure
(map inc [0 1 2 3])
; => (1 2 3 4)
```

### Naming values with `def`

You can use `def` to *bind* a name to a value in Clojure:

```clojure
(def posts-to-update [342, 827356, 172, 928375, 1434])

posts-to-update
; => [342, 827356, 172, 928375, 1434]
```

### Data Structures

In Clojure, all data structures are immutable.

#### Numbers

```clojure
93    ; integer
3.42  ; float
4/3   ; ratio
```

#### Strings

```clojure
"It's me!"
"\"This is the Unix philosophy: Write
programs that do one thing and do
it well. Write programs to work
together. Write programs to handle
text streams, because that is a
universal interface\" - Douglas McIlroy"
```

#### Keywords

Keywords are primarily used as keys in maps.

Keyword examples:

```clojure
:first-name
:last-name
:age
:my-keyword-example
```

#### Hash-Maps

```clojure
{}  ; empty hash-map
```

```clojure
{:first-name "Dominik"
 :last-name "Magdaleński"}
```

`:first-name` and `:last-name` are *keywords*

#### Vectors

```clojure
[1 2 3]
```

```clojure
[1 {:a "Aa" :b "Bb"} 43.45 3/4]
```

#### Lists

```clojure
'(1 2 3)
```

```clojure
'(1 "two" {3 4})
```

#### Hash-Sets - collections of unique values

```clojure
#{"Dominik Magdaleński" 1 :a-key}
```

### Multi-arity functions

```clojure
(defn multi-arity
  ;; 3-arity arguments and body
  ([first-arg second-arg third-arg]
     (do-things first-arg second-arg third-arg))
  ;; 2-arity arguments and body
  ([first-arg second-arg]
     (do-things first-arg second-arg))
  ;; 1-arity arguments and body
  ([first-arg]
     (do-things first-arg)))
```

```clojure
(defn greeting
  ([name]
    (str "Hello, " name "!"))
  ([]
    (greeting "Stranger")))
```

```clojure
(greeting)
; => "Hello, Stranger!"
```

```clojure
(greeting "Dominik")
; => "Hello, Dominik!"
```

### `&` - the rest parameter

```clojure
(defn my-func
  [first-arg & rest-args]
  (...)
```
