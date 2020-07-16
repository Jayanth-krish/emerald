---
title: Introduction
---
HipHop: Reactive Web programming
================================


Hiphop.js is a [Hop.js](http://hop-dev.inria.fr) DSL for
orchestrating web and IoT applications, which is inspired by Esterel.


```javascript
"use hiphop"
"use hopscript"

const hh = require( "hiphop" );

hiphop module prg( in A, in B, in R, out O ) {
   do {
      fork {
         await now( A );
      } par {
         await now( B );
      }
      emit O();
   } every( now( R ) )
}

const m = new hh.ReactiveMachine( prg, "ABRO" );
m.addEventListener( "O", e => console.log( "got: ", e ) );
m.react( { A: 1 }, { B: 2 }, { R: true }, { A: 3, B: 4 } );
```
