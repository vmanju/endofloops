# End of Loops - Intro to functional programming
Presentation materials for Intro to functional programming by [@vmanju](https://twitter.com/vmanju) <br>
To be delivered at Lead Developer conference, Austin Nov 8, 2019 <br>
Slide deck TBD <br>

## Code Snippets
These are working code snippets you can copy paste in your favorite Javascript IDE and run them. Have fun!

### Example for a side effect

```
# Impure function

let total = 0;
const increment = () => {
    total += 1;
}
increment();
console.log(total);


# Pure function

const increment = (total) => {
    return total + 1;
}

console.log(increment(0))
```

### Lets make a breakfast taco using loops
```
const pantry = [
  { name: 'eggs', vegan: false},
  { name: 'cheese', vegan: false},
  { name: 'potatoes', vegan: true},
  { name: 'salsa', vegan: true},
  { name: 'avocado', vegan: true}
];

const isVegan = (ingredient) => ingredient.vegan;

const prepareIngredient = (ingredient) => {
    return `prepared ${ingredient['name']}`;
}

const prepareTaco = (taco, ingredient) => taco + `${ingredient} `;

let ingredients = [];
let taco = 'Your breakfast taco 🌮 served with ';

for (let i = 0; i < pantry.length; i++) {
  if (isVegan(pantry[i])) {
    ingredients.push(prepareIngredient(pantry[i].name));
  }
}

for (let ingredient of ingredients) {
  taco += prepareTaco(ingredient);
}

console.log(taco);

```
### Lets make a breakfast taco by replacing loops with higher order functions

```
const taco = pantry.filter(isVegan)
    .map(prepareIngredient)
    .reduce(prepareTaco, "Your breakfast taco 🌮 served with ");
console.log(taco);
```

### Lets make a breakfast taco by replacing loops with composing functions

```
const taco = prepareTaco(prepareIngredient(isVegan(pantry)));
console.log(taco);

// Using reduce to compose functions and enable "pipe" functionality
const pipe = (...functions) => input => functions.reduce(
    (acc, fn) => fn(acc),input
);

const taco = pipe(isVegan, prepareIngredient, prepareTaco);
console.log(taco(pantry));*/
```

## Resources

[Mary Cook's Intro to functional programming](https://maryrosecook.com/blog/post/a-practical-introduction-to-functional-programming)
[Professor Frisby's Mostly Adequate Guide to Functional Programming](https://mostly-adequate.gitbooks.io/)
[MDN's reference on Array reduce function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
[The Almighty Reducer by Sarah Drasner](https://css-tricks.com/understanding-the-almighty-reducer/)
[Eric Elliot's Composing Software using Reduce](https://medium.com/javascript-scene/reduce-composing-software-fe22f0c39a1d)
[Jessica Kerr's Functional principles for OO developers](https://www.infoq.com/presentations/fp-principles-oop/)

