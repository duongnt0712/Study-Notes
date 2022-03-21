# NgRx
## 1. Overall Flow of Application State
![image](https://user-images.githubusercontent.com/93693577/158955782-57f4f42c-ae55-47bb-9b2e-685aa47e2b65.png)
- **Store**: to read data out of the store and connect that data to component.
- **Component**: then just dispatch the action to let other module know what action has occured.
- **Reducer**: then response to those actions and tell NgRx how to update state.
- **Selector**: to query out of the store for component to consume, or to wrap a piece of needed state to consume.
- **Effects**: to handles calling side effects or api calls in response to some actions being dispatch.
<br/>
> Store is an observable of `state` and an observer of `actions`.

![ngrx-store feature](https://user-images.githubusercontent.com/93693577/158959484-149322dc-0b71-4ea0-b22d-59a4050b9bfa.png)

> We should divide into `Store Feature Module` then import back to `Store Module`.

## 2. NgRx vs RxJs
- **RxJs:** handling complex asynchronous work like handling communication between client and server.
- **NgRx:** storing data in client and recalling them from all over the application.

## 3. Principle 
- **Single Source of Truth: **
	+ `State` stored in `Store`
	+ `Store` is an object tree
- `State` is **readonly**: `Store` dispatch `action` describing `state change`.
- Change are made with `Pure Functions`:
	+ return value is only dependent on input values
	+ no side effect

> `reducer`, `selectors`, and `RxJs operators` are `pure function`.

## 4. Architecture Deep Explaination
### Reducer
- Handling trasition from one state to next state.
- Determine which actions to handle based on the action's type
- Not change state, but make copy and change properties on new state
### Action
- Express unique events, especially the type of action
- Have optional payload (spread operators)
- Are dispatched by `Store` to ***run an effect*** or ***change state in reducer***
### State
- single, immutable data structure
- describe state changes
- accessed with `Store`

## 5. Component Store vs Store
- State need to persist: **using Store**
<br/>  State need to clean up: **using Component Store**
- Component Store is responsible for managing smaller, more local state.
<br/>  Global Store suited for managin global shared state.
> In case of larger apps, both Store and Component Store are applied.
- Global Store contains multiple `reducer`, each one hold a slice of state
<br/>  We can have many ComponentStores, but each one should store its own state.
- Global Store contains: `action`, `reducer`, `selector`, `effect` that is in all separate files
<br/>  Component Store contains `state`, `updaters`, `effects` in a single file, and having the additional selectors file.

![ngrx-compare store n component store](https://user-images.githubusercontent.com/93693577/159201881-3aa5ddb6-cf2b-47c7-b6fe-973608976e61.png)

### Component Store
- Initialize: 2 ways
	+ through constructor
	+ by calling setState and passing an object matches the state interface

- Read: using `select` method
- Write: 
	+ using `updater` method: analogous to **on()** in `Store reducer`
	+ `setState` method 
	+ `patchState` method
- Effect:
	+ using `effect` method, takes a callback with an Observable of values
