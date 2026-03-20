# weakset


24.4.1 The WeakSet Constructor

The WeakSet constructor:

    is %WeakSet%.
    is the initial value of the "WeakSet" property of the global object.
    creates and initializes a new WeakSet when called as a constructor.
    is not intended to be called as a function and will throw an exception when called in that manner.
    may be used as the value in an extends clause of a class definition. Subclass constructors that intend to inherit the specified WeakSet behaviour must include a super call to the WeakSet constructor to create and initialize the subclass instance with the internal state necessary to support the WeakSet.prototype built-in methods.

24.4.1.1 WeakSet ( [ iterable ] )

This function performs the following steps when called:

    1. If NewTarget is undefined, throw a TypeError exception.
    2. Let set be ? OrdinaryCreateFromConstructor(NewTarget, "%WeakSet.prototype%", « [[WeakSetData]] »).
    3. Set set.[[WeakSetData]] to a new empty List.
    4. If iterable is either undefined or null, return set.
    5. Let adder be ? Get(set, "add").
    6. If IsCallable(adder) is false, throw a TypeError exception.
    7. Let iteratorRecord be ? GetIterator(iterable, sync).
    8. Repeat,
           a. Let next be ? IteratorStepValue(iteratorRecord).
           b. If next is done, return set.
           c. Let status be Completion(Call(adder, set, « next »)).
           d. IfAbruptCloseIterator(status, iteratorRecord).

24.4.2 Properties of the WeakSet Constructor

The WeakSet constructor:

    has a [[Prototype]] internal slot whose value is %Function.prototype%.
    has the following properties:

24.4.2.1 WeakSet.prototype

The initial value of WeakSet.prototype is the WeakSet prototype object.

This property has the attributes { [[Writable]]: false, [[Enumerable]]: false, [[Configurable]]: false }.
24.4.3 Properties of the WeakSet Prototype Object

The WeakSet prototype object:

    is %WeakSet.prototype%.
    has a [[Prototype]] internal slot whose value is %Object.prototype%.
    is an ordinary object.
    does not have a [[WeakSetData]] internal slot.

24.4.3.1 WeakSet.prototype.add ( value )

This method performs the following steps when called:

    1. Let S be the this value.
    2. Perform ? RequireInternalSlot(S, [[WeakSetData]]).
    3. If CanBeHeldWeakly(value) is false, throw a TypeError exception.
    4. For each element e of S.[[WeakSetData]], do
           a. If e is not empty and SameValue(e, value) is true, then
                  i. Return S.
    5. Append value to S.[[WeakSetData]].
    6. Return S.

24.4.3.2 WeakSet.prototype.constructor

The initial value of WeakSet.prototype.constructor is %WeakSet%.
24.4.3.3 WeakSet.prototype.delete ( value )

This method performs the following steps when called:

    1. Let S be the this value.
    2. Perform ? RequireInternalSlot(S, [[WeakSetData]]).
    3. If CanBeHeldWeakly(value) is false, return false.
    4. For each element e of S.[[WeakSetData]], do
           a. If e is not empty and SameValue(e, value) is true, then
                  i. Replace the element of S.[[WeakSetData]] whose value is e with an element whose value is empty.
                  ii. Return true.
    5. Return false.

Note

The value empty is used as a specification device to indicate that an entry has been deleted. Actual implementations may take other actions such as physically removing the entry from internal data structures.
24.4.3.4 WeakSet.prototype.has ( value )

This method performs the following steps when called:

    1. Let S be the this value.
    2. Perform ? RequireInternalSlot(S, [[WeakSetData]]).
    3. If CanBeHeldWeakly(value) is false, return false.
    4. For each element e of S.[[WeakSetData]], do
           a. If e is not empty and SameValue(e, value) is true, return true.
    5. Return false.

24.4.3.5 WeakSet.prototype [ %Symbol.toStringTag% ]

The initial value of the %Symbol.toStringTag% property is the String value "WeakSet".

This property has the attributes { [[Writable]]: false, [[Enumerable]]: false, [[Configurable]]: true }.
24.4.4 Properties of WeakSet Instances

WeakSet instances are ordinary objects that inherit properties from the WeakSet prototype object. WeakSet instances also have a [[WeakSetData]] internal slot.
24.5 Abstract Operations for Keyed Collections
24.5.1 CanonicalizeKeyedCollectionKey ( key )

The abstract operation CanonicalizeKeyedCollectionKey takes argument key (an ECMAScript language value) and returns an ECMAScript language value. It performs the following steps when called:

    1. If key is -0𝔽, return +0𝔽.
    2. Return key.
