# Oxford English Dictionary Word Parser 📚🔍

**Oxford English Dictionary Word Parser** is a Python-based tool designed to scrape and parse English word data from the Oxford English Dictionary (OED) website. This project provides a robust solution for extracting and managing word-related information, including definitions, snippets, and parts of speech. It’s particularly useful for linguists, language enthusiasts, and developers working with English language datasets.

## Table of Contents

1. [Features](#features)
2. [Data Outputs](#data-outputs)
3. [Installation](#installation)
4. [Usage](#usage)
5. [Contributing](#contributing)
6. [License](#license)
7. [Disclaimer](#disclaimer)

## Features 🚀

- **Advanced Data Extraction**: Efficiently scrape detailed word data including definitions, snippets, and parts of speech from OED search pages.
- **Customizable Request Handling**: Control request delays and retry mechanisms to manage server load and handle errors gracefully.
- **Flexible Pagination Control**: Specify the starting page and the number of pages to parse, with support for large-scale data extraction.
- **Multiple Output Formats**: Save parsed data in various formats including CSV, JSON, and plain text.
- **Database Integration**: Load parsed data directly into a MySQL database for easy management and querying.
- **Error Logging**: Detailed logging of errors and exceptions for troubleshooting and debugging.
- **Dynamic Data Loading**: Supports loading data from local files directly into the database using `LOAD DATA LOCAL INFILE`.
- **Environment Configuration**: Utilize a `.env` file for secure and flexible database configuration.
- **Minification Option**: Option to minify JSON output for more compact data storage.
- **Cross-Platform Compatibility**: Designed to work across different operating systems with minimal configuration.

## Data Outputs 📂

The following data files are available for download in the `data` folder:

- **`english-words.txt`**: Contains a list of just the words, separated by a new line.
- **`english-words.csv`**: Usable with the `load-data-mysql.py` script to load data into a MySQL database.
- **`english-words.json`**: Contains the word data in pretty (indented) JSON format.
- **`english-words.min.json`**: Contains the word data in minified JSON format.

These files were generated using the script and are available for download directly in the `data` folder on the repository.

## Installation 🛠️

To run the scripts, you need to have Python 3 and the required packages installed. Follow these steps:

1. **Clone the Repository:**

    ```bash
    git clone https://github.com/ronbodnar/oxford-english-dictionary-parser.git
    cd oxford-english-dictionary-parser
    ```

2. **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

3. **Set Up the Environment:**

    Ensure you have Python 3.6 or higher installed. You may also want to set up a virtual environment.

    Create a `.env` file in the root directory of the project with the following content:

    ~~~
    DB_HOST=your_database_host
    DB_PORT=your_database_port
    DB_USER=your_database_user
    DB_PASS=your_database_password
    DB_NAME=your_database_name
    ~~~

    Replace the placeholders with your actual database connection details.

## Usage 📝

### `oed-parser.py`

Run the script to parse data from OED and save it to a specified output file:

```bash
python src/oed-parser.py --output-file results.txt
```

**Arguments:**
- `--request-delay` (int, optional): Delay between requests in seconds (default is 1).
- `--error-delay` (int, optional): Delay between retrying after an error (default is 60).
- `--max-retries` (int, optional): Maximum number of retries when encountering an error (default: 1).
- `--max-pages` (int, optional): Maximum number of pages to process (default is infinity).
- `--starting-page` (int, optional): The page number to start parsing from (default is 1).
- `--output-file` (string, optional): The path of the output file to write to (default is output.txt).
- `--delimiter` (string, optional): The delimiter for the output file (default: `,`)

**Example:**

To start parsing a total of 50 pages, starting from page 1, with a delay of 1 second between requests, and save results to `parsed_data.txt`, use:

```bash
python src/oed-parser.py --request-delay 1 --max-pages 50 --starting-page 1 --output-file parsed_data.txt
```

### `convert-data.py`

Convert the parsed data into different formats:

```bash
python src/convert-data.py -i parsed_data.txt -o output.json -f json -m
```

**Arguments:**
- `-i, --input-file` (str, required): The full path including the file name for the input CSV file.
- `-o, --output-file` (str, required): The full path including the file name for the output file.
- `-f, --format` (str, required): The format of the output. Can be 'csv', 'txt', or 'json'.
- `-m, --minified` (flag, optional): Flag to indicate if the JSON output should be minified.

### `load-data-mysql.py`

Load parsed data from CSV into a MySQL database:

```bash
python src/load-data-mysql.py
```

**Notes:**
- Ensure your `.env` file is properly configured with the database credentials before running this script.

## Contributing 🤝

Contributions are welcome! If you have suggestions for improvements or new features, please follow these steps:

1. **Fork the Repository**
2. **Create a New Branch**: `git checkout -b feature/your-feature`
3. **Commit Your Changes**: `git commit -am 'Add new feature'`
4. **Push to the Branch**: `git push origin feature/your-feature`
5. **Create a Pull Request**

## License 📜

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Disclaimer ⚠️

This project is intended for educational purposes and personal use. The script is not affiliated with or endorsed by the Oxford English Dictionary (OED). Users are responsible for ensuring compliance with OED's terms of service and legal restrictions on data usage.