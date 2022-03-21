#RxJS Operators

#### from
convert into observable, print element one by one

#### map
transform values emitted from source observable

#### pipe
chain multiple RxJS operators

#### filter
emit values that pass the provided condition

#### merge
turn multiple observable into a single one

#### mapTo
when `map` emit to constant value: 
`map(() => '...')` to `mapTo('...')`

#### pluck 
elect property to emit

#### switchMap
switch to a new observable, maintains only one inner subscription at a time.

#### mergeMap
control multi inner subscriptions at a time immediately, 

#### concatMap
map values to inner observable, subscribe and emit in order, until the previous one complete

#### of
same as `from`, but print the while value at once

#### tap
transparently perform actions or side-effects, not transform the value, handle success and error.


![ngrx-which map should we use](https://user-images.githubusercontent.com/93693577/158955690-5aee78b5-5b00-4f56-a378-7dbf545909a6.png)
![ngrx-which map should we use 1](https://user-images.githubusercontent.com/93693577/158955698-d9c1da3d-2527-4a19-9e75-3aa82afc5db3.png)
