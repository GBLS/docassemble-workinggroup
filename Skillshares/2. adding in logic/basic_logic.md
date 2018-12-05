# Docassemble Logic

Docassemble supports adding logic with all of the power of Python,
a fully-fledged programming language. When you are filling PDFs, creating documents
from scratch or using logic in an interview question, you will also make
use of very similar [`Mako`](https://docassemble.org/docs/markup.html#mako) tags, and when assembling a Docx template file,
you will use the very similar [`Jinja2`](https://docassemble.org/docs/documents.html#docx%20template%20file) tags to implement logic.

Most of the time the logic that you use will be pretty basic:
evaluating a True or False statement, and deciding what text to
hide or display in a document, or what follow-up questions to ask.

Here's an example of a few True or False statements translated into
Docassemble's language:
* `number1 > number2` evaluates to True if `number1` is larger than `number2`, and otherwise evaluates to False
* `saw_disclaimer` evaluates to True if we have a statement like `field: saw_disclaimer` on an interview
   screen with only a [`Continue`](https://docassemble.org/docs/questions.html#tocAnchor-1-5-3) button
* `claims.any_true()` evaluates to True if we have a checklist named `claims` and the user has selected at least one item in the [checklist](https://docassemble.org/docs/fields.html#fields%20checkboxes).
* `user_is_parent` evaluates to True if the user checked a [`datatype: yesno`](https://docassemble.org/docs/fields.html#fields%20yesno) field named `user_is_parent` in an interview

## Using True/False values in your Interview or Template

### The building block of logic: the if statement

The basic building block of logic is the `if` statement. The `if` statement is made up of
two parts: a logical test that evalutes to True or False, followed by something you
want the computer to _do_ if the test evaluates to True.

Here's an example of what this could look like in a Python `code` block:
```
if [logical test or Boolean value] :
    action
```
We just use the word `if` to tell the computer that what follows is going to be a test.
The `if` statement has to end with a `:`. In a `code` block the next line is indented to tell the computer
it is related to the `if` statement, and finally we run our action.

In an interview file, usually what you want to _do_ is just display some text, which can
include variables if you want. Here's an example of using logic that would work in a question
or document from scratch, using the `Mako` tag syntax.

```
% if [logical test or Boolean]:
Here's the optional text. It could have an optional ${variable} too.
% endif
```
There are a few minor differences in this `if` statement. Notice that we began the line with a `%` symbol.
This tells Docassemble/Mako that what follows is going to be an instruction instead of just normal text
that we want to display to the user. The second difference is that we did not need to indent the text that follows.
Finally, inside a `question` or document from scratch, we need to mark the end of the optional text with
the keyword `endif`.

There are some special shortcuts to be aware of. What happens if you have some text that you want to display
or action that you want to take that is different if the variable is False? You could simply reverse the test.
In Docassemble, the word `not` in front a test returns the opposite value. E.g., `if not [test]:`. The shortcut
is the keyword `else`.

```
if [logical test or Boolean]:
    action if True
else:
    action if False
```

Suppose that there are many possible values that you want to test. There is a special keyword `elif` that lets you
write a series of tests in a row. You can still use the final `else` as a default action that runs if the other
tests don't evaluate to True.

```
if value > 0 and value < 10:
    action 1
elif value >= 10 and value < 100
    action 2
else:
    default action
```

### Putting it into action


```yaml
---
question: Information about you
fields:
    - Your name: user_name
    - Your favorite number: user_number
      datatype: integer
---
code: |
    if user_number == 42:
        text = "You know the meaning of life, the universe and everything!"
    else:
        text = "You still have time to learn the meaning of life."
---
mandatory: True
question: Your download is ready.

attachment:
    - name: download
      filename: my_download
      content: |
        Hello, ${user_name}.

        Your favorite number is ${user_number}. ${text}

        % if user_number < 100:
        You don't like very large numbers!
        % elif user_number < 1000:
        Your favorite number is moderately big.
        % else:
        That's a big number!
        % endif
```

### Stretch goals

Here are some exercises you can try on your own.

* Create an interview that uses the basic [acknowledgement button](https://docassemble.org/docs/questions.html#tocAnchor-1-5-3) as an intro screen.
* Use [`datatype:yesno`](https://docassemble.org/docs/fields.html#fields%20yesno) together with a `fields` statement, and change the text displayed to the user depending on their answer.
* Create an interview that uses [checkboxes](https://docassemble.org/docs/fields.html#fields%20checkboxes) and display different text to the user
  depending on whether any items in the checklist where selected.