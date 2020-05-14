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

### Action
``` typescript
//Auth types
export const enum AuthTypes {
    SIGNUP_START = '[Auth] Signup Start',
    SIGNUP_SUCCESS = '[Auth] Signup Success',
    SIGNUP_FAIL = '[Auth] Signup Fail',
}

//signup start
export class SignupStart implements Action {
    readonly type = AuthTypes.SIGNUP_START;
    constructor(public payload: User) { }
}

//signup success
export class SignupSuccess implements Action {
    readonly type = AuthTypes.SIGNUP_SUCCESS;
    constructor(public payload: string) {
        console.log(payload)
    }
}

//signup failure
export class SignupFail implements Action {
    readonly type = AuthTypes.SIGNUP_FAIL;
    constructor(public payload: string) {
        console.log(payload);
    }
}


//auth actions union type
export type AuthActions =
      LoginStart
    | LoginSuccess
    | LoginFail
}
```

### Reducer
```typescript
import { User } from '../auth.model';
import * as AuthActions from './auth.action';


export interface State{
    user:User;
    authenticated:boolean;
    token:string;
    emailAlreadyExistStatus:boolean;
    
}

const iState = {
    user:null,
    authenticated:false,
    token:null,
    emailAlreadyExistStatus:false
}

export function authReducer(state=iState,action:AuthActions.AuthActions){
    switch(action.type){
          case AuthActions.AuthTypes.SIGNUP_START:
            return{
               ...state,
               user:null,
               authenticated:false,
               toekn:null            
            }
     case AuthActions.AuthTypes.SIGNUP_FAIL:
         return {
             ...state,
             error:action.payload,
             authenticated:false,
             token:null,
         }     
            
      default:
          return state;      
    }
}

//selector
export const getUser = (state:State) => state.user;
export const getToken = (state:State) => state.token;
export const getAuthenticated = (state:State) => state.authenticated;
export const getEmailAlreadyExistStatus = (state:State) => state.emailAlreadyExistStatus;
```



