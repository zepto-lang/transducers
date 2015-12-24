# transducers

A minimal transducer library in and for zepto.
Obviously inspired by Clojure.

It's a stub and not really usable yet.

# Usage

This library contains the functions `transduce`, `compose`,
`map`, `filter`, `reduce`, `take` and `partition-by`.

````clojure
(load "transducers/transducers")

; Let's get all those functions directly
(define transducers:transduce (import "transducers:transduce"))
(define transducers:map (import "transducers:map"))
(define transducers:take (import "transducers:take"))
(define transducers:filter (import "transducers:filter"))
(define transducers:partition-by (import "transducers:partition-by"))
(define transducers:compose (import "transducers:compose"))

; map and transduce are like regular map and reduce
(transducers:transduce (transducers:map add1) + 0 [1 2 3]) ; => 9

; filter also works like it's regular counterpart
(transducers:transduce (transducers:filter (curry eq? 1)) += [] [1 2 3 1]) ; => (1 1)

; take will take a number of elements from the input
(transducers:transduce (transducers:take 1) + 0 [1 2 3]) ; => 1

; partition-by will create sublist of equal elements next to each other
(transducers:transduce (transducers:partition-by id) += [] [1 1 1 2 2 2 1]) ; => ((1 1 1) (2 2 2) (1))

; compose will let us chain transducers
(define comp 
  (transducers:compose
    (transducers:map add1)
    (transducers:filter (lambda (x) (not (eq? 4 x))))))
(transducers:transduce comp += [] [1 2 3]) ; (2 3)
```

There is a lot still to come.

<hr/>
Have fun!
