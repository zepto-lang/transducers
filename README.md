# transducers

A minimal transducer library in and for zepto.
Obviously inspired by Clojure.

It's a stub and not really usable yet.

## Usage

This library contains the functions `transduce`, `compose`,
`map`, `cat`, `mapcat`, `filter`, `reduce`, `take` `into` and
`partition-by`.

````clojure
(load "transducers/transducers")

; Let's get all those functions directly
(define transducers:transduce (import "transducers:transduce"))
(define transducers:map (import "transducers:map"))
(define transducers:take (import "transducers:take"))
(define transducers:filter (import "transducers:filter"))
(define transducers:partition-by (import "transducers:partition-by"))
(define transducers:compose (import "transducers:compose"))
(define transducers:into (import "transducers:into"))
(define transducers:cat (import "transducers:cat"))
(define transducers:mapcat (import "transducers:mapcat"))

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

; into lets us add things to an existing collection
(transducers:into {} (transducers:map sub1) [2 3 4 5]) ; => {1 2 3 4}
```

There is a lot still to come.

## Caveats

Some of the transducers are not as generic as I would like them to be,
that is while one can specify special reduction functions to my version
of transduce (if the collection is unknown to me), you cannot do that with
all transducers; this is especially annoying with cat, which will only
work with standard collections and there is no way around that at the moment.

I hope I will be able to change that some other time.

<hr/>
Have fun!
