![alt text](https://increscotech.com/_next/static/images/logo-dark-692f2e4b1db92d8749d96ba04bcfb42d.svg)

# React Component Guidelines

- [Favor Functional Components](#favor-Functional-components)
- [Write Consistent Components](#write-consistent-components)
- [Name Components](#name-components)
- [Organize Helper Functions](#organize-helper-functions)
- [Don't Hardcode Markup](#dont-hardcode-markup)
- [Component Length](#component-length)
- [Use Error Boundaries](#use-error-boundaries)
- [Destructure Props](#destructure-props)
- [Number of Props](#number-of-props)
- [Pass Objects Instead of Primitives](#pass-objects-instead-of-primitives)
- [Conditional Rendering](#conditional-rendering)
- [Avoid Nested Ternary Operators](#avoid-nested-ternary-operators)
- [Move Lists in a Separate Component](#move-lists-in-a-separate-component)
- [Assign Default Props When Destructuring](#assign-default-props-when-destructuring)

#### Favor Functional Components

Favor functional components - they have a simpler syntax. No lifecycle methods, constructors or boilerplate. You can express the same logic with less characters without losing readability.

Unless you need an error boundary they should be your go-to approach. The mental model you need to keep in your head is a lot smaller.

```
// 👎 Class components are verbose
class Counter extends React.Component {
state = {
counter: 0,
}

constructor(props) {
super(props)
this.handleClick = this.handleClick.bind(this)
}

handleClick() {
this.setState({ counter: this.state.counter + 1 })
}

render() {
return (

<div>
<p>counter: {this.state.counter}</p>
<button onClick={this.handleClick}>Increment</button>
</div>
)
}
}

//
Functional components are easier to read and maintain
function Counter() {
const [counter, setCounter] = useState(0)

handleClick = () => setCounter(counter + 1)

return (

<div>
<p>counter: {counter}</p>
<button onClick={handleClick}>Increment</button>
</div>
)
}
```

#### Write Consistent Components

Stick to the same style for your components. Put helper functions in the same place, export the same way and follow the same naming patterns.

There isn’t a real benefit of one approach over the other

No matter if you’re exporting at the bottom of the file or directly in the definition of the component, pick one and stick to it.

#### Name Components

Always name your components. It helps when you’re reading an error stack trace and using the React Dev Tools.

It’s also easier to find where you are when developing if the component’s name is inside the file. Also your component name should start with Uppercase character

```
// 👎 Avoid this
export default () => <form>...</form>

// 👍 Name your functions
export default function Form() {
return <form>...</form>
}
```

#### Organize Helper Functions

Helper functions that don’t need to hold a closure over the components should be moved outside. The ideal place is before the component definition so the file can be readable from top to bottom.

That reduces the noise in the component and leaves inside only those that need to be there.

```
// 👎 Avoid nesting functions which don't need to hold a closure.
function Component({ date }) {
function parseDate(rawDate) {
...
}

return <div>Date is {parseDate(date)}</div>
}

// 👍 Place the helper functions before the component
function parseDate(date) {
...
}

function Component({ date }) {
return <div>Date is {parseDate(date)}</div>
}
```

You want to keep the least amount of helper functions inside the definition. Move as many as possible outside and pass the values from state as arguments.

Composing your logic out of pure functions that rely only on input makes it easier to track bugs and extend.

```
// 👎 Helper functions shouldn't read from the component's state
export default function Component() {
const [value, setValue] = useState('')

function isValid() {
// ...
}

return (
<>
<input
value={value}
onChange={e => setValue(e.target.value)}
onBlur={validateInput}
/>
<button
onClick={() => {
if (isValid) {
// ...
}
}} >
Submit
</button>
</>
)
}

// 👍 Extract them and pass only the values they need
function isValid(value) {
// ...
}

export default function Component() {
const [value, setValue] = useState('')

return (
<>
<input
value={value}
onChange={e => setValue(e.target.value)}
onBlur={validateInput}
/>
<button
onClick={() => {
if (isValid(value)) {
// ...
}
}} >
Submit
</button>
</>
)
}

```

#### Don't Hardcode Markup

Don’t hardcode markup for navigation, filters or lists. Use a configuration object and loop through the items instead.

This means you only have to change the markup and items in a single place.

```
// 👎 Hardcoded markup is harder to manage.
function Filters({ onFilterClick }) {
return (
<>

<p>Book Genres</p>
<ul>
<li>
<div onClick={() => onFilterClick('fiction')}>Fiction</div>
</li>
<li>
<div onClick={() => onFilterClick('classics')}>
Classics
</div>
</li>
<li>
<div onClick={() => onFilterClick('fantasy')}>Fantasy</div>
</li>
<li>
<div onClick={() => onFilterClick('romance')}>Romance</div>
</li>
</ul>
</>
)
}

// 👍 Use loops and configuration objects
const GENRES = [
{
identifier: 'fiction',
name: Fiction,
},
{
identifier: 'classics',
name: Classics,
},
{
identifier: 'fantasy',
name: Fantasy,
},
{
identifier: 'romance',
name: Romance,
},
]

function Filters({ onFilterClick }) {
return (
<>

<p>Book Genres</p>
<ul>
{GENRES.map(genre => (
<li>
<div onClick={() => onFilterClick(genre.identifier)}>
{genre.name}
</div>
</li>
))}
</ul>
</>
)
}
```

#### Component Length

A React component is just a function that gets props and returns markup. They adhere to the same software design principles.

If a function is doing too many things, extract some of the logic and call another function. It’s the same with components - if you have too much functionality, split it in smaller components and call them instead.

If a part of the markup is complex, requires loops and conditionals - extract it.

Rely on props and callbacks for communication and data. Lines of code are not an objective measure. Think about responsibilities and abstractions instead.

Write Comments in JSX
when something needs more clarity open a code block and give additional information. The markup is a part of the logic so when you feel that something needs more clarity - provide it.

```
function Component(props) {
return (
<>
{/_ If the user is subscribed we don't want to show them any ads _/}
{user.subscribed ? null : <SubscriptionPlans />}
</>
)
}
```

#### Use Error Boundaries

An error in one component shouldn’t bring down the entire UI. There are rare cases in which we want to take down the whole page or redirect if a critical error happens. Most of the times we’d be fine if we just hide a specific element from the screen.

In a function that deals with data you may have multiple try/catch statements. Put error boundaries to use not just on the top level. Wrap elements on the screen that can exist separately to avoid cascading failures.

```
function Component() {
return (
<Layout>
<ErrorBoundary>
<CardWidget />
</ErrorBoundary>

      <ErrorBoundary>
        <FiltersWidget />
      </ErrorBoundary>

      <div>
        <ErrorBoundary>
          <ProductList />
        </ErrorBoundary>
      </div>
    </Layout>

)
}
```

#### Destructure Props

Most React components are just functions. They get props and return markup. In a normal function you use the arguments it is passed directly, so it makes sense to apply the same principle here. No need to repeat props everywhere.

A reason not to destructure the props would be to distinguish what is external and what is internal state. But in a regular function there is no distinction between arguments and variables. Don’t create unnecessary patterns.

```
// 👎 Don't repeat props everywhere in your component
function Input(props) {
return <input value={props.value} onChange={props.onChange} />
}

// 👍 Destructure and use the values directly
function Component({ value, onChange }) {
const [state, setState] = useState('')

return <div>...</div>
}
```

#### Number of Props

The question of how many props should a component receive is a subjective one. The number of props that a component has is correlated to how much it’s doing. The more props you pass to it the more responsibilities it has.

A high number of props is a signal that a component is doing too much.

If I go above 5 props I consider whether this component should be split. In some cases, it may just need a lot of data. An input field, for example, may have a lot of props. In others it’s a sign that something needs to be extracted.

Note: The more props a component takes, the more reasons to rerender.

#### Pass Objects Instead of Primitives

One way to limit the amount of props is to pass an object instead of primitive values. Rather than passing down the user name, email and settings one by one you can group them together. This also reduces the changes that need to be done if the user gets an extra field for example.

Using TypeScript makes this even easier.

```
// 👎 Don't pass values on by one if they're related
<UserProfile
  bio={user.bio}
  name={user.name}
  email={user.email}
  subscription={user.subscription}
/>

// 👍 Use an object that holds all of them instead
<UserProfile user={user} />
```

#### Conditional Rendering

In some situations using short circuit operators for conditional rendering may backfire and you may end up with an unwanted 0 in your UI. To avoid this default to using ternary operators. The only caveat is that they’re more verbose.

The short-circuit operator reduces the amount of code which is always nice. Ternaries are more verbose but there is no chance to get it wrong. Plus, adding the alternative condition is less of a change.

```
// 👎 Try to avoid short-circuit operators
function Component() {
const count = 0

return <div>{count && <h1>Messages: {count}</h1>}</div>
}

// 👍 Use a ternary instead
function Component() {
const count = 0

return <div>{count ? <h1>Messages: {count}</h1> : null}</div>
}
```

#### Avoid Nested Ternary Operators

Ternary operators become hard to read after the first level. Even if they seem to save space at the time, it’s better to be explicit and obvious in your intentions.

```
// 👎 Nested ternaries are hard to read in JSX
isSubscribed ? (
<ArticleRecommendations />
) : isRegistered ? (
<SubscribeCallToAction />
) : (
<RegisterCallToAction />
)

// 👍 Place them inside a component on their own
function CallToActionWidget({ subscribed, registered }) {
if (subscribed) {
return <ArticleRecommendations />
}

if (registered) {
return <SubscribeCallToAction />
}

return <RegisterCallToAction />
}

function Component() {
return (
<CallToActionWidget
      subscribed={subscribed}
      registered={registered}
    />
)
}
```

#### Move Lists in a Separate Component

Looping through a list of items is a common occurrence, usually done with the map function. However, in a component that has a lot of markup, the extra indentation and the syntax of map don’t help with readability.

When you need to map over elements, extract them in their own listing component, even if the markup isn’t much. The parent component doesn’t need to know about the details, only that it’s displaying a list.

Only keep a loop in the markup if the component’s main responsibility is to display it. Try to keep a single mapping per component but if the markup is long or complicated, extract the list either way.

```
// 👎 Don't write loops together with the rest of the markup
function Component({ topic, page, articles, onNextPage }) {
return (

<div>
<h1>{topic}</h1>
{articles.map(article => (
<div>
<h3>{article.title}</h3>
<p>{article.teaser}</p>
<img src={article.image} />
</div>
))}
<div>You are on page {page}</div>
<button onClick={onNextPage}>Next</button>
</div>
)
}

// 👍 Extract the list in its own component
function Component({ topic, page, articles, onNextPage }) {
return (

<div>
<h1>{topic}</h1>
<ArticlesList articles={articles} />
<div>You are on page {page}</div>
<button onClick={onNextPage}>Next</button>
</div>
)
}
```

### Assign Default Props When Destructuring

One way to specify default prop values is to attach a defaultProps property to the component. This means that the component function and the values for its arguments are not going to sit together.

Prefer assigning default values directly when you’re destructuring the props. It makes it easier to read the code from top to bottom without jumping and keeps the definitions and values together.

```
// 👎 Don't define the default props outside of the function
function Component({ title, tags, subscribed }) {
return <div>...</div>
}

Component.defaultProps = {
title: '',
tags: [],
subscribed: false,
}

// 👍 Place them in the arguments list
function Component({ title = '', tags = [], subscribed = false }) {
return <div>...</div>
}
```

#### Avoid Nested Render Functions

When you need to extract markup from a component or logic, don’t put it in a function living in the same component. A component is just a function. Defining it this way is nesting inside its parent.

This means that it will have access to all the state and data of its parent. It makes the code more unreadable - what is this function doing in between all the components?

Move it in its own component, name it and rely on props instead of a closure.

```
// 👎 Don't write nested render functions
function Component() {
function renderHeader() {
return <header>...</header>
}
return <div>{renderHeader()}</div>
}

// 👍 Extract it in its own component
import Header from '@modules/common/components/Header'

function Component() {
return (

<div>
<Header />
</div>
)
}
```

### Acknowledgement/Credit:

https://alexkondov.com/tao-of-react/
