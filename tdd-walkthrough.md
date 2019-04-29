# What I learned on hackday!

So, hackday came around and I felt a bit lost on my solo build from the day: what was happening? What was my function _doing_?
I decided to spend the day looking under the hood of my JavaScript files, in search of that elusive gem, "comprehension".

What follows is my findings: the good, the bad, the entirely underwhelming, and everything in-between!

**FIRST, we have our MAIN JavaScript File, which tells the HTML main page to run our SCRIPT**

### Our SCRIPT:

**1. CREATES two variables:**
   1. buttons (a nodelist (which is LIKE an array, but you can't use array methods on it) of CLASS elements (in here called '.color'))
   2. snake (a single element from the HTML, in this case a _section_ with the id="snake")

```javascript
const buttons = document.querySelectorAll('.color');
const snake = document.getElementById('snake');
```
___

**2. RUNS a _for loop_ that does 6 discrete things _each time the loop runs_:**
   1. **_Creates_** a variable that is used like a counter (let i), and its value is 0.

   2. **_Compares_** the counter (i) to the _length_ of our nodelist. 

   3. **_Increments_** the counter (i) by 1, _for each time_ the loop runs (i++). 

   4. **_Defines_** a _new variable_ called _button_, and its _value_ is the _**index number**_ (i, which starts at 0)
    of our nodelist.

   5. **_Calls_** the addEventListener _method_ on the button _element_ ('wiring' it up), which...

   6. **_Calls_** the addPart function _every time_ the event ('click') occurs. 


```javascript
for(let i = 0; i < buttons.length; i++) {
    const button = buttons[i];

    button.addEventListener('click', () => {
        addPart(snake, button.value);
    });
}
```
(we show how we CREATE the addPart function in the section below) 

### Our addPart FUNCTION:
**1. Has 2 _parameters_:**
   1. The _first_ one (parentInnerHTML) is the _**value**_ (the 'inner' text) of the _element_ container that we would like **to append a child element _to_**.

2. The _second_ one (colorName) is the _content_ that will be _given_ to our _**DOM element's class attribute**_. 

 _**Creates** a variable_ (span) that stores the _result_ ('span') of **calling** the document.createElement _method_.

 _**Calls**_ the .add _method_ on the .classList _property_... _**onto the variable**_ (span).

_**Calls**_ the .appendChild _method_ on the _value_ (_**inner text**_) of the parentInnerHTML _parameter_, and passes it the previously-created (span) _element_.

```javascript        
function addPart(parentInnerHTML, colorName) {
const span = document.createElement('span');
span.classList.add('part');
span.classList.add(colorName);

parentInnerHTML.appendChild(span);

}
```
___

### Our TDD test explained, in order of appearance:

_**Call**_ the test() _function_, (which is a built-in meaning we didn't write or create it, and it comes with the file we define at the top, (const test = QUnit.test), which takes 2 _arguments_:
   1. A _string_ ('appends part to parent element') to display when you run your test, so you know _what_ your test is _for_.

   2. A _function_ that takes an argument (assert)-- _**which I had to google**_: 
>_an assertion is a statement that a **predicate** 
(Boolean-valued function, i.e. a true–false expression) is always true at that point in code execution._

**Inside the function, we _arrange_ 3 discrete things:**

1. _**Create**_ a _variable_ (colorName) and give it a _value_ that is a _string_ ('yellow').

2. _**Create**_ a _variable_ (parentElement) and its _value_ is the _**result**_ of _calling_ (createElement) on our _DOM object_ and _passing_ it the ('div') _element_ (in other words, **the _element_ we want to be _created_**). 

3. _**Create**_ a _variable_ and give it a _value_ that is a _string_ (`'<span class="part yellow"></span>'`).

 **We _act_ by _calling_** our addPart _function_ defined earlier, giving it 2 _arguments_: our parentElement _variable_, and our colorName _variable_.
 
Then we _**assign**_ the _inner HTML_ of our _variable_ parentElement to a _**new** variable_ called parentInnerHTML.

Lastly, we use QUnit's built-in _assert_ method which has its own method, _equal_, which checks (or "asserts") that the two parameters (_parentInnerHTML_ and _expected_) are the same.

```javascript
test('appends part to parent element', function(assert) {
//Arrange
const colorName = 'yellow';
const parentElement = document.createElement('div');
const expected = '<span class="part yellow"></span>';

//Act 
// call the function you're testing and set the result
addPart(parentElement, colorName);

//Assert
const parentInnerHTML = parentElement.innerHTML;
assert.equal(parentInnerHTML, expected);
});
```


## Thank you for coming to my head talk, where I try to figure out what's going on... using only my mind!
___
___
___
___
___
___
___
