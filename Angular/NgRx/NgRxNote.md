# NgRx
## 1. Overall Flow of Application State
![image](https://user-images.githubusercontent.com/93693577/158955782-57f4f42c-ae55-47bb-9b2e-685aa47e2b65.png)
- **Store**: to read data out of the store and connect that data to component.
- **Component**: then just dispatch the action to let other module know what action has occured.
- **Reducer**: then response to those actions and tell NgRx how to update state.
- **Selector**: to query out of the store for component to consume, or to wrap a piece of needed state to consume.
- **Effects**: to handles calling side effects or api calls in response to some actions being dispatch.
<br/>
`Store` is an observable of `state` and an observer of `actions`.

## 2. 




![ngrx-which map should we use](https://user-images.githubusercontent.com/93693577/158955690-5aee78b5-5b00-4f56-a378-7dbf545909a6.png)
![ngrx-which map should we use 1](https://user-images.githubusercontent.com/93693577/158955698-d9c1da3d-2527-4a19-9e75-3aa82afc5db3.png)
