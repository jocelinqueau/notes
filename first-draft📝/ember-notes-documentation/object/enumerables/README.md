# Enumerables

## Use of Observable Methods and Properties

In order for Ember to observe when you make a change to an enumerable, you need to use special methods that `MutableArray` provides. For example, if you add an element to an array using the standard JavaScript method `push()`, Ember will not be able to observe the change, but if you use the enumerable method `pushObject()`, the change will propagate throughout your application.

| Standard Method | Observable Equivalent |
| --- | --- |
| pop | popObject |
| push | pushObject |
| reverse | reverseObjects |
| shift | shiftObject |
| unshift | unshiftObject |

Additionally, to retrieve the first and last objects in an array in an observable fashion, you should use myArray.get('firstObject') and myArray.get('lastObject'), respectively.
