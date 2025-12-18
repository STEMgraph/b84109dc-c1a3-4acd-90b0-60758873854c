<!---
{
  "id": "b84109dc-c1a3-4acd-90b0-60758873854c",
  "depends_on": ["2c7334b3-b07d-48d6-a562-79072d8e166e"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-12-18",
  "keywords": ["JSON", "vim", "jq", "data format", "command-line", "structured data"],
  "license":"
Copyright 2025 Stephan Bökelmann

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
"
}
--->

# Introduction to the JSON Format Using `vim` and `jq`

> In this exercise you will learn the structure, rules, and features of the JSON data format. Furthermore we will explore how to edit JSON files using `vim`, and how to inspect and query them with the command-line tool `jq`.

## Introduction

JSON (JavaScript Object Notation) is a lightweight, human-readable data-interchange format widely used in APIs, configuration files, and data serialization. Its popularity comes from its simplicity and strict structure: data is either an object (a collection of key-value pairs) or an array (a list of values).

JSON supports several data types:

- **Objects**: Curly-braced key-value mappings (`{ "key": "value" }`)
- **Arrays**: Ordered lists (`[1, 2, 3]`)
- **Strings**: Double-quoted UTF-8 text
- **Numbers**: Integers and floats, including scientific notation
- **Booleans**: `true` and `false`
- **Null**: A special `null` literal

This exercise introduces you to all these features through hands-on editing and command-line inspection. You’ll write and read JSON by hand using `vim`, and use the CLI tool `jq` to format, filter, and transform JSON from the shell.

JSON is strict about syntax. Unlike YAML or XML, it enforces commas, brackets, and quoting rules. That makes it predictable but error-prone without proper tooling. `jq` is a powerful utility for parsing, validating, and manipulating JSON — similar to how `grep`, `awk`, or `sed` work with plain text.

### Further Readings and Other Sources

* [RFC 8259: The JSON Data Interchange Format](https://www.rfc-editor.org/rfc/rfc8259.html)
* `jq` Manual: [https://stedolan.github.io/jq/manual/](https://stedolan.github.io/jq/manual/)
* YouTube: “JQ Tutorial: Command Line JSON Processor” — [https://www.youtube.com/watch?v=1cPdY3XzVnU](https://www.youtube.com/watch?v=1cPdY3XzVnU)
* Book: *Data Wrangling with jq* by Brian J. Jones

---

## Tasks

---

### Task 0: Install `jq`

Install the `jq` tool using your package manager:

```bash
sudo apt update
sudo apt install jq
````

Verify it works:

```bash
jq --version
```

---

### Task 1: Create a JSON File by Hand

Use `vim` to create and edit a file called `profile.json`:

```bash
vim profile.json
```

Paste the following content:

```json
{
  "name": "Ada Lovelace",
  "born": 1815,
  "skills": ["mathematics", "programming", "poetry"],
  "is_active": false,
  "meta": {
    "verified": true,
    "score": 99.5,
    "tags": null
  }
}
```

This file demonstrates:

* **Strings** (`"Ada Lovelace"`)
* **Numbers** (`1815`)
* **Booleans** (`true`, `false`)
* **Arrays** (`["a", "b", "c"]`)
* **Nested objects**
* **Null values**

Save and exit `vim` (`:wq`).

---

### Task 2: Pretty-Print JSON with `jq`

Format your JSON neatly:

```bash
jq . profile.json
```

You should see the file reformatted with indentation and colors.

To overwrite the file with a pretty version:

```bash
jq . profile.json > pretty.json && mv pretty.json profile.json
```

---

### Task 3: Explore All JSON Features

Modify your `profile.json` to include more variety:

1. Add a floating point number
2. Use scientific notation: `1e6`
3. Include Unicode: `"symbol": "π"`
4. Nest arrays inside arrays
5. Mix types in an array: `[true, 42, "hello", null]`

Make sure it’s valid by running:

```bash
jq . profile.json
```

---

### Task 4: Query and Transform with `jq`

Try these commands:

```bash
jq '.name' profile.json
jq '.skills[1]' profile.json
jq '.meta.verified' profile.json
jq '.skills | length' profile.json
jq '.meta.tags // "No tags"' profile.json
```

These demonstrate:

* Field access
* Array indexing
* Dot-path navigation
* Length computation
* Null coalescing

---

## Questions

**1. What’s the difference between an object and an array in JSON?**

<details>
<summary>Click to reveal answer</summary>

An object maps named keys to values using `{}`; an array is an ordered list of values using `[]`.

</details>

**2. Why must JSON strings be enclosed in double quotes?**

<details>
<summary>Click to reveal answer</summary>

JSON strictly follows JavaScript's string rules, which require double quotes for valid string values.

</details>

**3. What does `null` mean in JSON?**

<details>
<summary>Click to reveal answer</summary>

It represents an intentional absence of value — similar to `None` in Python or `null` in C++ pointers.

</details>

**4. What happens if your JSON file contains a trailing comma?**

<details>
<summary>Click to reveal answer</summary>

It becomes invalid — JSON does not allow trailing commas unlike some other formats (like YAML).

</details>

**5. What does `jq '.meta.tags // "No tags"'` do?**

<details>
<summary>Click to reveal answer</summary>

If `.meta.tags` is `null` or missing, it outputs `"No tags"` instead. It’s a fallback/default operator.

</details>

---

## Advice

JSON may look simple, but real-world data can get deeply nested or messy. Learning to edit JSON in `vim` ensures you understand its syntax. Using `jq` is invaluable for inspecting and extracting information from JSON structures — especially in scripts or pipelines. Always validate your JSON after edits using `jq . file.json`. The more you explore, the more powerful and intuitive `jq` becomes. Stick to the strict format — no comments, no trailing commas, and always use double quotes.

---
