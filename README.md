### Key Concepts
* _Actions describe unique events that are dispatched from components and services._
* _State changes are handled by pure functions called reducers that take the current state and the latest action to compute a new state._
* _Selectors are pure functions used to select, derive and compose pieces of state._
* _State accessed with the Store, an observable of state and an observer of actions._

### Installation 
**with npm**<br>
```npm install --save @ngrx/store ``` <br>
**with yarn**<br>
```yarn add @ngrx/store ``` <br>
**with ng add**<br>
```ng add @ngrx/store```

## Setup
> counter.reducer.ts
``` typescript
import {Action} from '@ngrx/store';

iState={
   value:0
}

export function counterReducer(state=iState,action:Action){
  switch(action.type){
      case Increment:
         return {
         ...state, //implementing rule of thumb
         value:state.value+1
         };
      case Decrement:
         return {
         ...state,
         value:state.value-1
         }
      default:
         return state;
  }
}
```
_state changes with ngrx should always have to be immutable which means, must not edit the existing state._<br>
_Rule of thumbs always copy the old state and then override what you wanna change._
> counter.action.ts
``` typescript
import {Action} from '@ngrx/store'
export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';

export class IncrementActions implements Action{
readonly type = INCREMENT;
constructor(private payload:number){}
}

export class DecrementActions implements Action{
readonly type = DECREMENT;
constructor(private payload:number){}
}
```
_In your app.module.ts, import those reducers and use the StoreModule.forRoot(reducers) function to provide them to Angular's injector_
``` typescript
import { NgModule } from '@angular/core'
import { StoreModule } from '@ngrx/store';
import { counterReducer } from './counter';

@NgModule({
  imports: [
    BrowserModule,
    StoreModule.forRoot({ counter: counterReducer })
  ]
})
export class AppModule {}
```
_You can then inject the Store service into your components and services. Use store.select to select slice(s) of state:_
> counter.component.ts
``` typescript
export class CounterComponent implements OnInit{
constructor(){}
ngOnInit(){

}

}
```
