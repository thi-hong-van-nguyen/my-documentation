## When change to new computer and can't push new repo to new repo on GitHub
### ERROR: 
```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

1. What you can do is open Git Bash, type in `ssh-keygen`, hit enter until it's done. 
  ``ssh-keygen -t ed25519 -C "thinguyen.webdev@gmail.com"``
2. Then type `cat ~/.ssh/id_rsa.pub` or `cat ~/.ssh/id_dsa.pub`. copy the whole string including your email
3. open GitHub -> setting -> SSH key -> generate new SSH -> paste the string into SSH key section and save
4. git add. commit and push

## SCROLL BAR

[Link](https://www.w3schools.com/howto/howto_css_hide_scrollbars.asp)
```
.example {
  overflow-y: scroll; /* Add the ability to scroll */
}

/* Hide scrollbar for Chrome, Safari and Opera */
.example::-webkit-scrollbar {
    display: none;
}

/* Hide scrollbar for IE, Edge and Firefox */
.example {
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}

<div class="example">Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling.. Some text to enable scrolling..  </div>

```

## MAX-WIDTH
- set the width of the parent `div` to
```
width: 100%;
overflow: hidden;
```
- set the second `div` to 
```
width: 80%; (what ever width desired)
max-width: 1220px;
margin: 0;
padding: 2% 0;
```

## SET HEIGHT TO 100VH:
```
body,
html {
  height: 100%;
  width: 100%;
  margin: 0
}

.parent-div {
  (min-)height: 100vh;
  overflow-x: hidden;
  overflow-y: hidden;
```

## EXPAND/ COLLAPSE ANIMATION
```
.tasks-container {
  width: 100%;
  margin: auto;
  max-height: 3000px;
  transition: max-height 0.5s ease-in;
  overflow: hidden;
}

.hidden {
  max-height: 330px;
  transition: max-height 0.3s ease-out;
}
```

## PROMISE, ASYNC AWAIT
- Promise basic:
```
const codeBlocker = () => {
    return new Promise((resolve, reject)=> {
        let i = 0;
        while(i< 1000000){i++};
        resolve("billion loops done")
    })
}

console.log("console log 1")
codeBlocker().then(log)
console.log("console log 2")
```
result:
console log 1 => `Elapse: 0ms`
console log 2  => `Elapse: 730ms` => The rum time is deplayed because the while loop blocks the main thread
billions loops done  => `Elapse: 731ms`

### Solution:
- put the while loops inside of the Promises call back, that way other operations won't be block by the loops
- Do this instead:
```
const codeBlocker = () => {
    return Promise.resolve().then(v => {
        let i = 0;
        while(i< 1000000){i++};
        return "billion loops done"
    })
}
```

- We can either use `async` keyword (`async function Func(){}`), or `return Promise.resolve()`

### async await:
```
const makeSmoothie = async () => {
    const a = await getFruit("pineapple");
    const b = await getFruit("strawberry");

    return [a, b]
}
```
- Above code will make b wait for a which double waiting time, so in order to make them run concurrently, we can use `Promise.all`:
```
const makeSmoothie = async () => {
    try{
        const a = getFruit("pineapple");
        const b = getFruit("strawberry");
        const smothie = await Promise.all([a, b]);
        return smothie
    } catch (err) {
        console.log(err);
        return "error message"
    }
}

makeSmoothie().then().catch(err => console.log({err}))
```

### async await and foor loops, map
- If we code something like `list.map(item => await...)`, it won't work. We need to use for loop instead
```
const smoothie = async () => {
    for await (const fruit of smothie) {
        console.log(fruit)
    }
}
```
- We can also use async await for if statement:
```

const fruitInspection = async () => {
    if (await getFruit('peach') === "peach"){
        console.log("it is a peach")
    }
}
```



## USEFORM, YUP VALIDATION
`useForm.js`
```
import { useState, useEffect } from "react";
import * as yup from "yup";

export const useForm = (initialValues, initialErrors, schema) => {
  const [formValues, setFormValues] = useState(initialValues);
  const [errors, setErrors] = useState(initialErrors);
  const [isDisabled, setIsDisabled] = useState(false);

  const validation = (name, value) => {
    yup
      .reach(schema, name)
      .validate(value)
      .then(() => setErrors({ ...errors, [name]: "" }))
      .catch((err) => setErrors({ ...errors, [name]: err.errors[0] }));
  };

  useEffect(() => {
    schema.isValid(formValues).then((valid) => setIsDisabled(!valid));
  }, [formValues]);

  const handleChange = (e) => {
    const { name, value, checked, type } = e.target;
    const valueToUse = type === "checkbox" ? checked : value;
    validation(name, valueToUse);
    setFormValues({ ...formValues, [name]: valueToUse });
  };

  return [formValues, errors, handleChange, isDisabled];
};
```

`Schema.js`
```
import * as yup from "yup";

const loginSchema = yup.object().shape({
  username: yup.string().trim().required("Username is required"),
  password: yup.string().trim().required("Password is required field"),
});

export default loginSchema;
```

`Login.js`
```
const [formValues, errors, handleChange, isDisabled] = useForm(initialValues, initialErrors, schema)
```

## REDUX, REDUCER, ACTIONS
- import {compose} from 'redux';
- Instead of writing function nested in another function, we could write `compose(func1, func2, func3)` with func3 is the one nested deepest, and func1 is the outside function

- Subscribe the changes of the state:
```
const subscriber = () => console.log("SUBSCRIBER", store.getState())
store.subscribe(subscriber)
```
===> same with redux logger

