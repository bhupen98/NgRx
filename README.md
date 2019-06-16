### Key Concepts
* _Actions describe unique events that are dispatched from components and services._
* _State changes are handled by pure functions called reducers that take the current state and the latest action to compute a new state._
* _Selectors are pure functions used to select, derive and compose pieces of state._
* _State accessed with the Store, an observable of state and an observer of actions._

### Installation 
_**with npm**_<br>
```npm install --save @ngrx/store ``` <br>
_**with yarn**_<br>
```yarn add @ngrx/store ``` <br>
_**with ng add**_<br>
```ng add @ngrx/store```
### Let's take an example of ingredients
> ingredient.actions.ts
``` typescript
import { Action } from '@ngrx/store';
import { Ingredient } from '../../shared/ingredient.model';

export const ADD_INGREDIENT = 'ADD_INGREDIENT';

export class AddIngredient implements Action{
  readonly type = ADD_INGREDIENT; //action type
  payload:Ingredient //data
}
```

> ingredient.reducer.ts
``` typescript
import {Ingredient} from '../../shared/ingredient.model';
import * as ingredientActions from './ingredient.actions';
import { Action } from '@ngrx/store';

const iState = {
ingredients:[
   new Ingredient('Apple',1),
   new Ingredient('Bananas',2)
]
}

export function IngredientReducer(state=iState,action:ingredientActions.AddIngredient){
switch(action.type){
   case ingredientActions.ADD_INGREDIENT:
      return {
         ...state, //coping the old state
         ingredients:[...state.ingredients,action.payload]
      };
      default:
         return state
}
}
```
> app.model.ts
``` typescript
import {StoreModule} from '@ngrx/store';
imports:[
StoreModule.forRoot({ingredients:IngredientReducer})
]
```
