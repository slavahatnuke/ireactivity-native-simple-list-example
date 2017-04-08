## iReactivity simple react native example
The main idea:

```javascript
import React, {Component} from 'react';

// native
import {
    AppRegistry,
    Text,
    View,
    Button
} from 'react-native';

// iReactivity binding functions
import {Provider, connect} from 'ireactivity';

const uid = () => Math.random().toString(35).slice(2, 8).toUpperCase();

// store, it's just an object.
const store = {
    todos: [
        {title: 'Todo #1', id: uid()},
        {title: 'Todo #2', id: uid()}
    ]
};

const TodoView = ({todo, onRemove}) =>
    <View>
        <Text>{todo.title}</Text>

        <Button
            onPress={() => onRemove(todo)}
            title={`[x]`}
            color="#FF0000"
        />
    </View>;

const Todo = connect(TodoView, {
    onRemove: (store) => (todo) => {
        console.log('remove', todo.id);
        store.todos = store.todos.filter((aTodo) => todo !== aTodo)
    }
});

const TodosView = ({todos}) =>
    <View>
        {todos.map((todo) => <Todo key={'' + todo.id} todo={todo}/>)}
    </View>;

const Todos = connect(TodosView, {
    todos: (store) => store.todos
});

const TodoPlusView = ({onClick}) =>
<Button
    onPress={onClick}
    title="Add"
    color="#000000"
/>

const TodoPlus = connect(TodoPlusView, {
    onClick: (store) => () => {
        let id = uid();
        store.todos = [...store.todos, {title: `Todo #${id}`, id: id}]
    }
});

const App = () =>
    <View style={ {alignItems: 'center', margin: 20} }>
        <TodoPlus/>
        <Todos/>
    </View>;

const AppRunner = () => <Provider store={store}><App/></Provider>;
AppRegistry.registerComponent('ireactivityNativeSimpleListExample', () => AppRunner);
```

## How to start
- `npm install`
- `npm start`

## iReactivity
[https://www.npmjs.com/package/ireactivity](https://www.npmjs.com/package/ireactivity) - Simple React binding 