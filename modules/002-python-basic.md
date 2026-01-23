# Python basic

* Module: [LPC-002](002-python-basic.md)
* Date: 2026-01-23
* Environment: macOS Sequoia / Python 3.12.0

## 📝 Introduction

Learn to write Robust Code that ensures service sustainability and maintainability.

## 🎯 Objectives

* Master Python's core data types and structures for production.
* Define effective functions and handle parameters efficiently.
* Understand the role of Type Hinting and static analysis.
* Implement proper Exception Handling to build resilient services.

## 💡 Motivation

* **Self-Documenting**: Type annotations serve as the most accurate documentation.
* **Reliability**: `try-except` blocks protect services from external failures (e.g., network instability).
* **Efficiency**: Choosing the right data structure is the first step toward optimizing data pipelines.

## 📖 Concepts

### Core Data Structures

Select the optimal data structure based on the nature of your data.

| **Structure**  | **Characteristics**    | **Use Case**                           |
| -------------- | ---------------------- | -------------------------------------- |
| **List** `[]`  | Ordered, Mutable       | mage paths, sequence data              |
| **Dict** `{}`  | Key-Value, Fast Lookup | API responses (JSON), Model configs    |
| **Tuple** `()` | Immutable              | Coordinates, Resolution `(1080, 1920)` |
| **Set** `{}`   | Unique, Set Algebra    | Label management, Deduplication        |

### Functions & Type Hinting

A function is not just a block of code; it is a process of defining `Inputs` and `Outputs`.

- **Type Hinting**: Enhances readability and stability by specifying `variable: type`
- **Static Analysis**: Detects type mismatches before runtime using tools like `mypy`.

| **Concept**       | **Description**                            | **Example**            |
| ----------------- | ------------------------------------------ | ---------------------- |
| **Parameters**    | Functional inputs (Type hints recommended) | `def save(name: str):` |
| **Return Type**   | Specifies the type of the output           | `-> bool:`             |
| **Default Value** | Fallback value if argument is missing      | `limit: int = 10`      |
| **Flexible Args** | Handling variable number of arguments      | `*args`, `**kwargs`    |

#### Example

```python
def function_name(param1: type, param2: type = default) -> return_type:
	...
	return result
```

>[!TIP] Why Use Type Hinting? While Python is dynamically typed,
> explicit hints enable IDE autocompletion and prevent runtime errors during
> collaboration. It makes your code "readable" for both humans and machines.

## Error Handling

Services must remain operational even during unexpected events like network failures or memory issues.

```python
try:
    # 1. Main logic execution
except FileNotFoundError as e:
    # 2. Error handling (Fallback)
else:
	# 3. Post-processing after successful try
finally:
    # 4. Cleanup/Logging (Always executes)
```

## 💻 Hands-on Implementation

### Case1. Data Structure & Type Hinting

#### Scenario:

> 1. Extract unique names from user data (`list[dict]`) and return them as a sorted list.
> 2. Define clear inputs and outputs using type hints.

#### Execution:

```python
def get_unique_names(users: list[dict[str, str]]) -> list[str]:
    # Use Set for efficient deduplication
    unique_names: set[str] = { user["name"] for user in users }
    return sorted(list(unique_names))

# Test data
raw_data = [
    { "name": "Alice" },
    { "name": "Bob" },
    { "name": "Alice" }
]
result = get_unique_names(raw_data)

# Expected Output: ['Alice', 'Bob']
print(result)
```

### Case2. Error Handling (Stability)

#### Scenario:

> 1. Capture `KeyError` when accessing a dictionary to prevent crashes.
> 2. Utilize the `finally` block for consistent logging.

#### Execution:

```python
def find_score(data: dict[str, int], name: str) -> int:
    try:
        # Jump to 'except' immediately if key is missing
        score = data[name]
        return score
    except KeyError:
        # Fallback to default value instead of crashing
        print(f"⚠️ Data for '{name}' not found. Returning default (0).")
        return 0
    finally:
        # Always executes for cleanup or logging
        print("--- Lookup Completed ---")

scores = { "student1": 100, "student2": 90 }


print(find_score(scores, 'student1'))
print(find_score(scores, 'Python'))
```


## 🔗 Reference & Resources

- [Data structure](https://docs.python.org/3/tutorial/datastructures.html)
- [Error handling](https://docs.python.org/3/tutorial/errors.html)
