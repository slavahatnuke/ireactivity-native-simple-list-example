## iReactivity simple react native example
The main idea:

```javascript
import React, {Component} from 'react';
import {
    AppRegistry,
    Text,
    View,
    Button
} from 'react-native';

// iReactivity binding functions
import {Provider, connect} from 'ireactivity';

//
// export default class ireactivityNativeSimpleListExample extends Component {
//   render() {
//     return (
//       <View style={styles.container}>
//         <Text style={styles.welcome}>
//           Welcome to React Native!
//         </Text>
//         <Text style={styles.instructions}>
//           To get started, edit index.ios.js
//         </Text>
//         <Text style={styles.instructions}>
//           Press Cmd+R to reload,{'\n'}
//           Cmd+D or shake for dev menu
//         </Text>
//       </View>
//     );
//   }
// }
//
// const styles = StyleSheet.create({
//   container: {
//     flex: 1,
//     justifyContent: 'center',
//     alignItems: 'center',
//     backgroundColor: '#F5FCFF',
//   },
//   welcome: {
//     fontSize: 20,
//     textAlign: 'center',
//     margin: 10,
//   },
//   instructions: {
//     textAlign: 'center',
//     color: '#333333',
//     marginBottom: 5,
//   },
// });


const uid = () => Math.random().toString(35).slice(2, 8).toUpperCase();

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
    </View>

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

// const AppView = () => <View><Text>List</Text> <TodoPlus/> <Todos/></View>;

// const App = AppView;


// <View><Text>List</Text> <TodoPlus/> <Todos/></View>
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