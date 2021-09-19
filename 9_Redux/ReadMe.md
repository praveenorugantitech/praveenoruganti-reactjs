# Redux

Redux is a state management library for JavaScript apps.

The advantages of Redux are

- Centralizes application's state
- Makes data flow transparent and predictable

![screenshot of the app](https://raw.githubusercontent.com/praveenorugantitech/praveenoruganti-reactjs-course/master/9_Redux/images/1.PNG)

## Redux Architecture

![screenshot of the app](https://raw.githubusercontent.com/praveenorugantitech/praveenoruganti-reactjs-course/master/9_Redux/images/2.PNG)

We need to follow the below steps in building a redux app.

- Design the store
- Define the actions
- Create a reducer
- Setup the store


1. **Action**

Actions are plain JavaScript objects that have a type field.
Actions only tell what to do, but they don't tell how to do.

For example,

return {
    type: ADD_EMPLOYEE,
    payload: employee
}

**Action Creator**

Pure function which creates an action

For example,

const addEmployee = employee => {
    return {
        type: ADD_EMPLOYEE,
        payload: employee
    }
}

This is Reusable, Portable and Easy To Test.

2. **Reducer**

Reducers are the functions that take the current state and an action as arguments, and return a new state result.

For example,

const intialState = {
    employees: [],
}

const reducer = (state = intialState, action) => {
    switch (action.type) {
        case FETCH_EMPLOYEES:
            return {
                employees: action.payload,
            }
        case ADD_EMPLOYEE:
            return {
                ...state,
                employees: [...state.employees, action.payload],
            }
        case DELETE_EMPLOYEE:
            return {
                employees: [
                    ...state.employees.filter(employee => employee !== action.payload)
                ]
            }
        case UPDATE_EMPLOYEE:
            return {
                employees: [

                    ...state.employees.map(emp =>
                        emp.emailId === action.payload.emailId ?
                            { ...state.employees, ...action.payload } : emp)
                ]
            }


        default: return state
    }
}

3. **Store**

The Redux store brings together the state, actions and reducers that make up your app.

It's important to note that you will only have a single store in a Redux application.

Every Redux store has a single root reducer function.

For example,

const rootReducer = combineReducers({
    employee: employeeReducer
})

import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
const store = createStore(rootReducer, applyMiddleware(thunk))


## Redux Principles

1. Single source of Truth

The global state of your application is stored as an object inside a single store.

2. State is Read-Only

The only way to change the state is to dispatch an action.

3. Immutability, One-way data flow, Predictability of outcome

4. Changes are Made with Pure Reducer Functions



You can checkout my [Employee Registration App](https://github.com/praveenorugantitech/praveenoruganti-emp-reg-ui/tree/master/frontend) which is implemented based on redux.















