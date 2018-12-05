# Docassemble Cheat Sheet
## KEY CONCEPTS:
Fields (variables) store information. Fields can have multiple datatypes, such as numbers, dates, Booleans, or regular text.

Functions can transform fields. You can do basic operations on fields as well, such as x = a+b. capitalize(variable_name)

If: else: statements are the building block of logic.

## GETTING INFORMATION FROM THE USER
Two types of questions: basic question blocks, and the fields statement.
Basic questions only allow a few types of question structures. You can always use the fields statement instead of a basic question block.
A page that doesn't do anything (but you want to display to the user) uses a field statement. Clicking continue sets it to True.

## SYNTAX TO REMEMBER
### Logic in your interview
Code blocks use Python. Assignments: = Comparison: ==. Logic: if variable_name: 

### Formatting questions / Documents from scratch
Questions use Mako tags to insert fields.

Adding a variable: ${ variable_name}

Logic: %if variable: %endif

Control structures: %for x in my_list: %endfor

Documents from scratch work the same way as questions.

### Filling a Docx template
Uses Jinja2 syntax
Adding a variable: {{ variable_name }}

Logic: {% if variable_name %} {% endif %}

Special version that doesn't leave empty lines: {%p if variable_name %} {%p endif %}

## Groups
Lists have an order. This is the default kind of group you should use.

Each item in a dictionary has a label, which is helpful if you know the labels ahead of time and want to retrieve information later. They are unordered.

Sets are for storing items when you can't control when they are added but you don't want to repeat any items. You can also perform set operations (union, intersection, etc)
