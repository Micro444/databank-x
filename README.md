# <img src="logo.png" alt="Databank_X Logo" height="80"> Databank_X

**A minimalistic, extensible database and encryption toolkit for Python**  
_Developed by Micro444_

[![PyPI version](https://badge.fury.io/py/databank-x.svg)](https://badge.fury.io/py/databank-x)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![License: Custom](https://img.shields.io/badge/License-Custom-yellow.svg)](#license)

---

## Table of Contents

- [Overview](#overview)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Basic Functions (`basic`)](#basic-functions-basic)
- [JSON File Management (`saves`)](#json-file-management-saves)
- [Encryption & Security (`security`)](#encryption--security-security)
- [Logging System (`LogManager`)](#logging-system-logmanager)
- [Data Export (`convert`)](#data-export-convert)
- [Search Functionality (`search`)](#search-functionality-search)
- [Backup System (`backup`)](#backup-system-backup)
- [Examples](#examples)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [License](#license)

---

## Overview

**Databank_X** is a lightweight Python library for managing dictionary-based data with integrated functions for JSON serialization, file encryption using Fernet (symmetric encryption), comprehensive logging, data export capabilities, and backup functionality.

### Key Features

✨ **Simple Data Structure Management** - Dictionary-based data organization  
🔒 **Built-in Encryption** - Fernet-based file encryption with key management  
💾 **JSON Persistence** - Automatic data saving and loading  
📊 **Data Export** - Export to Excel and CSV formats  
🔍 **Search Functionality** - Find data across all directories  
📝 **Comprehensive Logging** - Optional logging system with file output  
🔄 **Backup System** - Automated data backup functionality  
🚀 **Minimal Dependencies** - Only `cryptography` and `pandas` as external dependencies  

Perfect for small projects, learning purposes, prototyping, or as a foundation for larger database solutions.

---

## Installation

### Via pip (Recommended)

```bash
pip install databank-x
```

### Dependencies

```bash
pip install cryptography>=3.0.0 pandas>=1.3.0
```

---

## Quick Start

```python
from databank_x import basic, saves, security, LogManager

# Initialize logging (optional)
LogManager.setup("app.log")

# Initialize data structure
basic.basic_List()

# Create new directory
basic.add_directory("users")

# Add data
basic.add_data("Alice", "users")
basic.add_data("Bob", "users")

# Display data
print(basic.show_List())
# Output: {'test1': [1, 'hi'], 'test2': ['his', 86], 'users': ['Alice', 'Bob']}

# Save as JSON
saves.save_json("my_data.json")

# Encrypt file
security.encrypt("my_data.json")
```

---

## Basic Functions (`basic`)

Jump to: [Logging](#logging-system-logmanager) | [Data Export](#data-export-convert) | [Search](#search-functionality-search)

### Function Overview

| Function | Description | Example |
|----------|-------------|---------|
| `basic_List()` | Initialize data structure | `basic.basic_List()` |
| `show_List()` | Show current data | `print(basic.show_List())` |
| `add_data(data, dir)` | Add data | `basic.add_data("value", "folder")` |
| `add_directory(name)` | Create directory | `basic.add_directory("new_folder")` |
| `remove_directory(name)` | Delete directory | `basic.remove_directory("folder")` |
| `remove_data(dir, index)` | Remove data by index | `basic.remove_data("folder", 0)` |
| `index_searche(dir, index)` | Search by index | `basic.index_searche("folder", 1)` |
| `string_data(string, dir)` | String to list | `basic.string_data("Hello", "chars")` |

### Detailed Descriptions

#### `basic.basic_List()`
Initializes the global data structure with sample data:
```python
basic.basic_List()
# Creates: {'test1': [1, 'hi'], 'test2': ['his', 86]}
```

#### `basic.add_data(datas, directory)`
Adds an entry to an existing directory:
```python
basic.add_directory("fruits")
basic.add_data("Apple", "fruits")
basic.add_data("Banana", "fruits")
# Result: {'fruits': ['Apple', 'Banana']}
```

#### `basic.string_data(datas, directory)`
Converts a string into a list of characters:
```python
basic.string_data("Hello", "letters")
# Result: {'letters': [['H', 'e', 'l', 'l', 'o']]}
```

---

## JSON File Management (`saves`)

### Functions

| Function | Description | Returns |
|----------|-------------|---------|
| `save_json(file)` | Save data as JSON | None |
| `see_json(file)` | Load JSON data | Dictionary |
| `overwrite_data_json(file)` | Overwrite current data | None |

### Usage

```python
# Save current data to file
saves.save_json("database.json")

# Load data from file (without overwriting current data)
loaded_data = saves.see_json("database.json")
print(loaded_data)

# Load and overwrite current data
saves.overwrite_data_json("database.json")
```

---

## Encryption & Security (`security`)

### Functions

| Function | Description | Key Storage |
|----------|-------------|-------------|
| `encrypt(files)` | Encrypt file | Saves key to `keys.txt` |
| `decrypt(filess, keys)` | Decrypt file | Reads key from specified file |

### Usage

```python
# Encrypt a file (generates and saves key automatically)
security.encrypt("sensitive_data.json")

# Decrypt the file using saved key
security.decrypt("sensitive_data.json", "keys.txt")
```

⚠️ **Security Note**: Keep your `keys.txt` file secure and separate from encrypted data!

---

## Logging System (`LogManager`)

### Functions

| Function | Description | Returns |
|----------|-------------|---------|
| `setup(file)` | Initialize logging | None |
| `see_log(file)` | Read log file | String |
| `log_message(message)` | Log custom message | None |

### Usage

```python
# Initialize logging system
LogManager.setup("application.log")

# Log custom messages
LogManager.log_message("Application started")

# View log contents
print(LogManager.see_log("application.log"))
```

When logging is enabled, all operations are automatically logged with timestamps and detailed information.

---

## Data Export (`convert`)

### Functions

| Function | Description | Output Format |
|----------|-------------|---------------|
| `convert_to_excel(file)` | Export to Excel | `.xlsx` |
| `convert_to_csv(file)` | Export to CSV | `.csv` |

### Usage

```python
# Export data to Excel
convert.convert_to_excel("data_export.xlsx")

# Export data to CSV
convert.convert_to_csv("data_export.csv")
```

The data is automatically formatted with directories as columns and their values as rows.

---

## Search Functionality (`search`)

### Functions

| Function | Description | Returns |
|----------|-------------|---------|
| `search_data(value)` | Find value in all directories | Tuple (key, list) or None |

### Usage

```python
# Search for a specific value across all directories
result = search.search_data("Alice")
if result:
    directory, data_list = result
    print(f"Found 'Alice' in directory '{directory}': {data_list}")
else:
    print("Value not found")
```

---

## Backup System (`backup`)

### Functions

| Function | Description | Output |
|----------|-------------|---------|
| `backup_data()` | Create data backup | `backup.json` |

### Usage

```python
# Create automatic backup
backup.backup_data()
# Creates backup.json with current data state
```

---

## Examples

### Complete Data Management Workflow

```python
from databank_x import basic, saves, security, LogManager, convert, search, backup

# 1. Initialize logging and setup data
LogManager.setup("company.log")
basic.basic_List()
basic.add_directory("employees")
basic.add_directory("projects")

# 2. Add some data
basic.add_data("John Doe", "employees")
basic.add_data("Jane Smith", "employees")
basic.add_data("Website Redesign", "projects")
basic.add_data("Mobile App", "projects")

# 3. Search for data
result = search.search_data("John Doe")
print(f"Search result: {result}")

# 4. Create backup
backup.backup_data()

# 5. Export to different formats
convert.convert_to_excel("company_data.xlsx")
convert.convert_to_csv("company_data.csv")

# 6. Save and encrypt
saves.save_json("company_data.json")
security.encrypt("company_data.json")

# 7. View logs
print("Application logs:")
print(LogManager.see_log("company.log"))
```

### Working with Logging

```python
# Enable detailed logging
LogManager.setup("detailed.log")

# All operations are now automatically logged
basic.basic_List()
basic.add_directory("test")
basic.add_data("sample", "test")

# Add custom log messages
LogManager.log_message("Custom operation completed")

# View complete log
logs = LogManager.see_log("detailed.log")
print(logs)
```

---

## API Reference

### Basic Module (`basic`)

All functions remain the same as in the previous version, with added logging support when enabled.

### LogManager Module (`LogManager`)

#### `LogManager.setup(file)`
Initializes the logging system with the specified log file.

**Parameters:**
- `file` (str) - Log filename

**Returns:** None

#### `LogManager.see_log(file)`
Reads and returns the contents of a log file.

**Parameters:**
- `file` (str) - Log filename to read

**Returns:** `str` - Log file contents or error message

#### `LogManager.log_message(message)`
Logs a custom message if logging is enabled.

**Parameters:**
- `message` (str) - Message to log

**Returns:** None

### Convert Module (`convert`)

#### `convert.convert_to_excel(excel_file)`
Exports current data to Excel format.

**Parameters:**
- `excel_file` (str) - Output Excel filename

**Returns:** None

#### `convert.convert_to_csv(csv_file)`
Exports current data to CSV format.

**Parameters:**
- `csv_file` (str) - Output CSV filename

**Returns:** None

### Search Module (`search`)

#### `search.search_data(value)`
Searches for a value across all directories.

**Parameters:**
- `value` (any) - Value to search for

**Returns:** `tuple` (directory_name, directory_contents) or `None`

### Backup Module (`backup`)

#### `backup.backup_data()`
Creates a backup of the current data structure.

**Returns:** None
**Creates:** `backup.json` file

---

## Contributing

We welcome contributions! Please feel free to submit a Pull Request.

### Development Setup

1. Fork the repository
2. Create a virtual environment
3. Install dependencies: `pip install -r requirements.txt`
4. Make your changes
5. Run tests
6. Submit a pull request

---

## Changelog

### Version 2.0.0
- Added comprehensive logging system (`LogManager`)
- Implemented data export functionality (Excel/CSV)
- Added search functionality across directories
- Integrated automatic backup system
- Enhanced error handling and logging throughout
- Improved code structure and documentation

### Version 1.0.0
- Initial release with basic data management
- JSON serialization support
- Fernet encryption integration

---

## License

This project is licensed under the MIT. See the license terms for more details. Also the code is written with AI to 10%
