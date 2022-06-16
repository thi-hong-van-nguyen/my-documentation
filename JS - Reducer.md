# REDUX, REDUCER, ACTION CREATOR
## Action creator:
```
export const addDataToStore = (key, data) => {
    return {
        type: key,
        data: data,
    };
};
```

## Reducer
```
const initialState = {};

export const dataReducer = (state = initialState, action) => {
    const { type, data } = action;
    return {
        ...state,
        [type]: data,
    };
};

```
