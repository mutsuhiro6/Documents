# RDD methods

## aggregate

```scala
def aggregate[U](zeroValue: U)(seqOp: (U, T) ⇒ U, combOp: (U, U) ⇒ U)
```

### zeroValue: U
This is the value Spark will start with for every partition. Why do you need this? Because of seqOp. seqOp takes an element of type U and an element of type T. Your RDD contains only elements of type T. So you need to give it at least 1 U to get started.

### seqOp: (U, T) ⇒ U

seqOp is what Spark will apply over all data of a partition. It will take your zeroValue (type U) and an element of your RDD (type T) and spit out a new element of type U. It can then use this element to combine it with another element of your partition. And so on. Until it ends with a single element of type U per partition.

Note that this is like the super version of Spark's reduce and fold ops:

- It is better than a reduce, because a reduce is basically applying a seqOp of (T, T) ⇒ T to all your elements. So a reduce is more limited, since all needs to be the same type.
- It is better than a fold (which imho is awkward anyway in Spark) for the same reasons.

But of course, at the end of all seqOps, you're now stuck with multiple elements of type U. So we need that combOp.

Note: the first argument in seqOp is the one that is the right type, so that is probably why they say:

> The functions op(t1, t2) is allowed to modify t1 and return it as its result value to avoid object allocation; however, it should not modify t2.

Because they can keep using it just fine.

### combOp: (U, U) ⇒ U

This is basically a reduce on all these U's you got from doing seqOp on your partitions.

That is basically what they mean with

> The first function (seqOp) can return a different result type, U, than the type of this RDD. Thus, we need one operation for merging a T into an U and one operation for merging two U"