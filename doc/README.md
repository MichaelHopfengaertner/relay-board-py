# Documentation of relay board py
This is the actual documentation of the package.

After installing the `relay_board_py` package via `pip`, it can be used in different ways.

## Usage
1. Execute package directly as module:
```bash
python -m relay_board_py -s RB90FJ7SIHYU1F -c 1,7 -o 2 -r
```

2. Integrate into own python module:
```python
from relay_board_py.relay_board import RelayBoard

RelayBoard.main(['-s', 'RB90FJ7SIHYU1F', '-c', '1,7', '-o', '2', '-r'])
```

## Arguments
```bash
	-h, --help          show this help message and exit
	-s SERIAL_NUMBER    Serial-number in single operation mode
	-o OPEN             Specify relay ids to be opened "-o 1,2,3"
	-c CLOSE            Specify relay ids to be closed "-c 1,2,3"
	-f FILE             File path to json file containing the patterns
	-p PATTERN          Pattern to be used in provided json file
	-r                  Reset relay-board(s) first, before executing the operations
```

Relay boards can be controlled:
- by serial-number (arguments: -s, -o, -c)
- or by json pattern file (argumments: -f, -p)

## Pattern files
For more complex relay board control, json "pattern" files can be defined:
```json
{
	"aliases": {
		"A1": "RB90FJ7SIHYU1F",
		"A2": "RB9ZIRP7TWC305"
	},
	"patterns": {
		"P1": {
			"A1": {
				"open": [1],
				"close": [2]
			},
			"A2": {
				"open": [3],
				"close": [4]
			}
		},
		"P2": {
			"A1": {
				"open": [10],
				"close": [1, 2]
			}
		}
	}
}
```

The pattern file can be executed the following way:
```bash
python -m relay_board_py -f example_pattern.json -p P2 -r
```
