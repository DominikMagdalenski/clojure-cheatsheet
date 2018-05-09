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

### Built-in functions

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
