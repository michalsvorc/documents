# RxJS Subjects

* [Guide](https://rxjs-dev.firebaseapp.com/guide/subject)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/subjects)

A Subject is like an Observable, but can multicast to many Observers. Subjects are like EventEmitters: they maintain a
registry of many listeners.

An RxJS Subject is a special type of Observable that allows values to be *multicasted* to many Observers. Subjects are
like EventEmitters: they maintain a registry of many listeners.

* Every Subject is an Observable: You can subscribe to it.
* Every Subject is an Observer: It is an object with the methods next(v), error(e), and complete().

Subjects are the only way of making any Observable execution be shared to multiple Observers.

A "multicasted Observable" passes notifications through a Subject which may have many subscribers, whereas a plain
"unicast Observable" only sends notifications to a single Observer.

There are 4 variants of subjects:

* Subject - No initial value or replay behavior.
* AsyncSubject - Emits latest value to observers upon completion.
* BehaviorSubject - Requires an initial value and emits its current value (last emitted item) to new subscribers.
* ReplaySubject - Emits specified number of last emitted values (a replay) to new subscribers.

## Subject

* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/subjects/subject)

A special type of Observable which shares a single execution path among observers.

## BehaviorSubject

* [Guide](https://rxjs-dev.firebaseapp.com/guide/subject#behaviorsubject)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/subjects/behaviorsubject)

Has a notion of "the current value". It stores the latest value emitted to its consumers, and whenever a new Observer
subscribes, it will immediately receive the "current value" from the BehaviorSubject. BehaviorSubjects are useful for
representing "values over time".

## ReplaySubject

* [Guide](https://rxjs-dev.firebaseapp.com/guide/subject#replaysubject)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/subjects/replaysubject)

A ReplaySubject is similar to a BehaviorSubject in that it can send old values to new subscribers, but it can also
record a part of the Observable execution.  A ReplaySubject records multiple values from the Observable execution and
replays them to new subscribers.

## AsyncSubject

* [Guide](https://rxjs-dev.firebaseapp.com/guide/subject#asyncsubject)
* [Learn RxJS](https://www.learnrxjs.io/learn-rxjs/subjects/asyncsubject)

The AsyncSubject is a variant where only the last value of the Observable execution is sent to its observers, and only
when the execution completes.  The AsyncSubject is similar to the
[last()](https://rxjs-dev.firebaseapp.com/api/operators/last) operator, in that it waits for the *subject.complete()*
notification in order to deliver a single value.


