# SKItrace

![](./img/hero.jpg)

Nock tracing of `SKI` evaluation following the development of ~lagrev-nocfep (in press), “Representing the SKI Combinator Calculus in the Nock Instruction Set Architecture”, *Urbit Systems Technical Journal*.

The `S`, `K`, and `I` combinators are represented using the Nock ISA.  They require an expansion phase followed by an application phase.

Usage:

```sh
$ python3 nocktrace.py I 42    
========================================================================
(1)  *[42 [[I]]]   -- produces the VALUE of I
========================================================================
# *[42 [[I]]]   compile expansion
  *[42 [[I]]]
  *[42 1 I]   [[I]] = [1 I]
  *[42 1 0 1]   substitute S,K,I formulas

# evaluation
  *[42 1 0 1]
  [0 1]         Nock 1  *[a 1 b] = b

= [0 1]

========================================================================
(2)  applying that value to 42
========================================================================
# applying val(I) to 42   ( *[42 val(I)] )
  val(I) = [0 1]

# evaluation of *[42 [0 1]]
  *[42 0 1]
  /[1 42]     Nock 0  *[a 0 b] = /[b a]
  42          /[1 a] = a

= 42

------------------------------------------------------------------------
pinochle: val(I)            = [0 1]
pinochle: that value on 42      = 42
agreement: value OK, application OK
```
