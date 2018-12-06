# Docassemble Cheat Sheet
## Key Concepts

The `interview` asks questions. You can use the interview to generate a document from scratch, or to fill in a Docx or PDF `template`
file.

`Fields` (variables) store information. Fields can have multiple `datatypes`, such as numbers, dates, Booleans, or regular text.

`Functions` can transform fields. You can do basic operations on fields as well, such as `x = a+b` or `capitalize(variable_name)`

`If: else:` statements are the building block of logic.

Each `block` in your interview (i.e., each dialog screen shown the user) needs to separated with `---` on its own line.

Spacing and indentation is important.

## Getting Information From the User
Two types of questions: basic question blocks, and the `fields` statement.
Basic questions only allow a few types of question structures. You can always use the fields statement instead of a basic question block.

A page that doesn't do anything (but you want to display to the user) uses a field statement. Clicking continue sets it to True.

In the documentation, look at both **Setting Variables** and **Question Blocks** to learn how to set a field with a question.

## How Docassemble Asks Questions
Docassemble asks a question **if and only if** it is marked `mandatory: True` _or it is needed to fill-in any `fields`_ used in the
mandatory block (for example, any fields used in a document you generate or a final summary screen).

Docassemble will use the _last_ question that fills-in the field in your interview file. You can [override](https://docassemble.org/docs/logic.html#order) this on a question-by-question basis using [`if`](https://docassemble.org/docs/modifiers.html#if)

Good practice is to have only one mandatory block in your file. For longer interviews, use a `code` block to [control question order](https://docassemble.org/docs/logic.html#order).
It is only necessary to mention the variable in the code block for Docassemble to seek out its definition.

## Syntax to Remember
### Logic in your interview
Code blocks use Python. 
* Assignments: `=` 
* Comparison: `==`
* Logic: `if variable_name:`

### Formatting questions / Documents from scratch
Questions use `Mako` tags to insert fields.

Adding a variable: `${ variable_name}`

Logic: `%if variable:` on its own line and followed by  `%endif` on its own line.

Control structures: `%for x in my_list:` followed by `${x}` followed by `%endfor` on its own line.

Documents from scratch work the same way as questions.

### Filling a Docx template
Uses `Jinja2` syntax
Adding a variable: {% raw %}`{{ variable_name }}`{% endraw %}

Logic: `{% if variable_name %}` `{% endif %}`

Special version that doesn't leave empty lines: {% raw %}`{%p if variable_name %}` {% endraw %} on its own line followed by  {% raw %}`{%p endif %}`{% endraw %}

## Groups
Lists have an order. This is the default kind of group you should use.

Each item in a dictionary has a label, which is helpful if you know the labels ahead of time and want to retrieve information later. They are unordered.

Sets are for storing items when you can't control when they are added but you don't want to repeat any items. You can also perform set operations (union, intersection, etc)
