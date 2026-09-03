# QuizGame

QuizGame is a command-line quiz application written in Go. It loads questions and answers from a CSV file, presents each question, and reports the number of correct answers before the time limit expires.

## Requirements

- Go 1.27 or newer
- A terminal that can accept standard input

## Run the quiz

From the repository root, start the quiz with the included question set:

```sh
go run .
```

The default time limit is 30 seconds. Enter one answer per question and press Enter. The quiz ends when all questions are answered or the time limit expires.

## Options

| Option | Default | Description |
| --- | --- | --- |
| `-csv` | `problems.csv` | Path to the question file |
| `-limit` | `30` | Time limit in seconds |

Examples:

```sh
go run . -limit 60
go run . -csv custom-problems.csv -limit 20
```

To see the available flags:

```sh
go run . -h
```

## Question file format

The CSV file must contain one question per row with exactly two fields:

```csv
question,answer
5+5,10
Capital of France,Paris
```

The first field is displayed as the question. The second field is the expected answer, with surrounding whitespace ignored. Answers are compared as entered, so capitalization and spelling must match unless the input and expected answer are identical.

Questions should not include a header row. The included `problems.csv` demonstrates the expected format.

## Project structure

```text
.
├── main.go       # CLI entry point and quiz logic
├── problems.csv  # Sample questions and answers
├── go.mod        # Go module definition
└── README.md     # Project documentation
```

## Development

Format the Go source and run the test command from the repository root:

```sh
gofmt -w main.go
go test ./...
```

The application currently has no automated tests. When adding tests, keep quiz data in test fixtures rather than changing the sample question set unless the change is intentional.

## Current behavior and limitations

- The timer starts after the question file is loaded.
- Each question is shown once, in CSV order.
- A question that is unanswered when time expires is not counted as correct.
- Invalid or unreadable CSV files cause the program to exit with an error.
- Empty rows or rows with fewer than two fields are not supported.
