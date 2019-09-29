# Option Parser
Build: [![CircleCI](https://circleci.com/gh/AndreRenaud/option_parser.svg?style=svg)](https://circleci.com/gh/AndreRenaud/option_parser)

Option Parser is a minimal command line arguments parsing library designed
to provide minimal argument parsing without in a single function call.

It is designed for simple command line utilities (or in-built CLI-style
commands) with standard command line behaviour.

It supports both single-character short, and multi-character long style
arguments, ie: `-f filename` or `--file filename`

It also provides some utility functions for automatically breaking down a
single

## Example Usage
```c
int main(int argc, char *argv[]) {
	char *file = NULL;
	int64_t val = 5;
	struct option_entry entries[] = {
		{"file", 'f', "File to load", OPTION_FLAG_string, .string = &file},
		{"number", 'n', "Number", OPTION_FLAG_int, .integer = &val},
		{NULL, 0},
	};
	if (opt_parse(argc, argv, entries) < 0) {
		opt_parse_usage(eprintf, argv[0], entries);
		return -1;
	}
	if (opt_parse_is_present('f', entries)
		printf("file: %s\n", file);
	printf("number: %lld\n", val);
	return 0;
}
```
