# Formula 1 SQL Practical Exercises

This repository is a hands-on SQL practice project built around Formula 1
results. It includes a SQLite database, the SQL dump used to create it, CSV
exports, and worked exercises covering queries from basic `SELECT` statements
through joins, aggregations, subqueries, and common table expressions (CTEs).

## Why use this project?

The dataset makes SQL practice concrete: query drivers, constructors, races,
standings, qualifying results, and pit stops while working with real-world
relational data. The exercises are useful for:

- Learning and revising core SQL syntax.
- Practising filtering, sorting, pagination, and calculated columns.
- Comparing aggregation and grouping techniques.
- Understanding joins across related Formula 1 tables.
- Building confidence with subqueries and CTEs.
- Experimenting with a self-contained database that requires no server.

## Repository contents

| Path | Description |
| --- | --- |
| [`f1_data.db`](f1_data.db) | Ready-to-query SQLite database. |
| [`f1_data.sql`](f1_data.sql) | SQLite dump for recreating the database. |
| [`F1DatabaseChallenge.txt`](F1DatabaseChallenge.txt) | SQL challenge prompts and example solutions. |
| [`vWxwKOYyT7yzDdIvbuxv_Module_3_and_4/Module_3_and_4.sql`](vWxwKOYyT7yzDdIvbuxv_Module_3_and_4/Module_3_and_4.sql) | Exercises for SQL modules 3 and 4. |
| `*.csv` | CSV exports for drivers, constructors, results, standings, qualifying, and pit stops. |
| [`SQL Essentials (SQL01) - ITonlinelearning Academy.pdf`](SQL%20Essentials%20%28SQL01%29%20-%20ITonlinelearning%20Academy.pdf) | Related course reference material. |

The database currently contains 859 drivers and 1,111 constructor records
representing 211 distinct constructor IDs, with race results covering seasons
2000–2024. Use the database itself as the source of truth if the data is
updated.

## Getting started

### Prerequisites

Install SQLite 3. No Python, Node.js, or database server is required.

### Open the supplied database

From the repository root, start the SQLite command-line shell:

```bash
sqlite3 f1_data.db
```

List the available tables and run a query:

```sql
.tables

SELECT GivenName, FamilyName, Nationality
FROM drivers
ORDER BY FamilyName, GivenName
LIMIT 10;
```

Exit with `.quit`.

### Recreate the database from the SQL dump

To create a fresh copy without changing the checked-in database:

```bash
sqlite3 /tmp/f1_practice.db < f1_data.sql
sqlite3 /tmp/f1_practice.db '.tables'
```

### Work through the exercises

Open [`F1DatabaseChallenge.txt`](F1DatabaseChallenge.txt) or
[`Module_3_and_4.sql`](vWxwKOYyT7yzDdIvbuxv_Module_3_and_4/Module_3_and_4.sql)
in a text editor. Run individual statements against `f1_data.db`, then modify
them to answer the prompts or test alternative approaches.

For example, find the five highest-scoring drivers in 2024:

```sql
SELECT DriverID,
       GivenName || ' ' || FamilyName AS Driver,
       SUM(Points) AS TotalPoints
FROM results
WHERE Season = 2024
GROUP BY DriverID, GivenName, FamilyName
ORDER BY TotalPoints DESC
LIMIT 5;
```

The examples use SQLite syntax. When using another SQL engine, adjust
engine-specific functions such as string concatenation and command-line
client commands as needed.

## Data model

The main tables are:

- `drivers` and `constructors`: identity and nationality information.
- `results`: driver finishing results, points, constructor, and race metadata.
- `driver_standings` and `constructor_standings`: season-round standings.
- `results_qualy`: qualifying results.
- `pitstops`: pit-stop timing and lap data.
- `results_history`: historical results data.

Inspect a table's columns in SQLite with:

```sql
.schema results
```

## Getting help

Start with the exercise prompts and the schema in [`f1_data.sql`](f1_data.sql).
For project questions or suspected data issues, open a
[GitHub issue](https://github.com/VoidLance/course-files-sql-practical-exercises-f1-challenge/issues).
For SQLite syntax and built-in functions, consult the
[SQLite documentation](https://www.sqlite.org/docs.html).

## Contributing

Contributions are welcome, especially corrected queries, clearer explanations,
data-quality fixes, and additional exercises. To contribute:

1. Fork the repository and create a focused branch.
2. Make the smallest change that addresses the problem.
3. Test SQL examples against a fresh database created from `f1_data.sql`.
4. Describe the change and validation performed in your pull request.

Please avoid committing generated database files or unrelated course material.
Use the existing exercise style and keep examples compatible with SQLite unless
the documentation clearly states otherwise.

## Maintainer

This project is maintained by the repository owner and its contributors.
Review the [commit history](https://github.com/VoidLance/course-files-sql-practical-exercises-f1-challenge/commits)
for current maintainer and contributor attribution. Use GitHub issues and pull
requests for support, corrections, and proposed improvements.

## License

No license file is currently included in this repository. Review the repository
owner's licensing terms before redistributing the contents.
