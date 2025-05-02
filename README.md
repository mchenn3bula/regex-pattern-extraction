# Regex Pattern Extraction 🔍

A Python-based tool for extracting structured information from unstructured text using regular expressions. The current implementation focuses on identifying dollar amounts and telephone numbers in English text.

## Project Overview 📋

This project demonstrates the power of regular expressions (regex) for information extraction from large text corpora. Using carefully crafted regex patterns, the system can identify and extract various formats of:

- Currency expressions (dollar amounts)
- Telephone numbers

The system is designed to be extensible and can be adapted to extract other types of structured information.

## Features ✨

### Dollar Amount Detection

The currency detection module can identify various formats of monetary expressions including:

- Symbol-based formats: `$10.50`, `$1,000,000`
- Word-based formats: `ten dollars`, `fifty cents`
- Mixed formats: `half a dollar`, `three thousand dollars`
- Currency with scale indicators: `$5 million`, `10 billion dollars`
- Fractional amounts: `$0.75`, `75 cents`
- International formats: `US$100`

### Telephone Number Detection

The telephone number extraction module identifies various phone number formats including:

- Standard US format: `(123) 456-7890`
- Hyphenated format: `123-456-7890`
- Dot-separated format: `123.456.7890`
- Space-separated format: `123 456 7890`
- Basic 10-digit format: `1234567890`

## Implementation Details 🔧

### Dollar Amount Regex Pattern

The dollar amount pattern uses a complex regex to capture many variations:

```python
dollar_regex = re.compile(r"""
    (\$\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?\s*(million|billion)?\b
    |\b\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?\s*(million|billion)?\s*dollars?\b
    |\b\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?\s*(spanish)?\s*cents?\b
    |\b\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?\s*dollars?\s+and\s+\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?\s*cents?\b
    |\bUS\$?\s*\d{1,3}(?:,\d{3})*(?:\.\d{1,2})?\s*(million|billion)?\b
    |\b(?:zero|one|two|three|four|five|six|seven|eight|nine|ten|eleven|twelve|thirteen|fourteen|fifteen|sixteen|seventeen|eighteen|nineteen|twenty|thirty|forty|fifty|sixty|seventy|eighty|ninety|hundred|thousand|million|billion)\s*(?:\s(?:zero|one|two|three|four|five|six|seven|eight|nine|ten|eleven|twelve|thirteen|fourteen|fifteen|sixteen|seventeen|eighteen|nineteen|twenty|thirty|forty|fifty|sixty|seventy|eighty|ninety|hundred|thousand|million|billion))*\s*(spanish)?\s*dollars?\b
    |\b(?:zero|one|two|three|four|five|six|seven|eight|nine|ten|eleven|twelve|thirteen|fourteen|fifteen|sixteen|seventeen|eighteen|nineteen|twenty|thirty|forty|fifty|sixty|seventy|eighty|ninety|hundred|thousand|million|billion)\s*(?:\s(?:zero|one|two|three|four|five|six|seven|eight|nine|ten|eleven|twelve|thirteen|fourteen|fifteen|sixteen|seventeen|eighteen|nineteen|twenty|thirty|forty|fifty|sixty|seventy|eighty|ninety|hundred|thousand|million|billion))*\s*cents?\b
    |\b(?:half\s+a\s+)?dollar\b
    )
""", re.IGNORECASE | re.VERBOSE)
```

### Telephone Number Regex Pattern

The telephone number pattern uses a more compact regex to capture common US phone number formats:

```python
phone_regex = re.compile(r"""
    (
    \(?\d{3}\)?[-.\s]?   # Area code (optional)
    \d{3}[-.\s]?        # First 3 digits
    \d{4}               # Last 4 digits
    )
""", re.VERBOSE)
```

## Data 📚

The system has been tested on the Open American National Corpus (OANC), a large collection of American English text from various sources.

## Usage 🚀

### Prerequisites

- Python 3.x

### Running the Code

1. Clone this repository:
```
git clone https://github.com/yourusername/regex-pattern-extraction.git
cd regex-pattern-extraction
```

2. Place your input text file in the project directory.

3. Run the dollar amount extraction:
```python
from dollar_extractor import find_dollar_amounts
find_dollar_amounts('input.txt', 'dollar_output.txt')
```

4. Run the telephone number extraction:
```python
from phone_extractor import find_telephone_numbers
find_telephone_numbers('input.txt', 'telephone_output.txt')
```

## Sample Results 📊

### Sample Dollar Amounts Extracted:
```
half a dollar
three Spanish dollars
30,000 dollars
$1.50
75 cents
$5,000
$1,000,000
fifty cents
ten dollars
```

### Sample Telephone Numbers Extracted:
```
(801) 596-1887
(757) 229-4631
541-754-4600
(303) 462-9000
(919) 541-1522
```

## Applications 🌟

This pattern extraction system can be useful for:

- Data mining and text analytics
- Information extraction from unstructured data
- Financial text analysis
- Document processing
- Customer data extraction

## Future Improvements 🔮

- Extend to support additional currencies (Euro, Pound, Yen, etc.)
- Add support for international phone number formats
- Improve robustness to unusual text formatting
- Develop additional extractors for dates, addresses, email addresses, etc.
- Add validation and normalization of extracted data

## License 📝

This project is licensed under the MIT License - see the LICENSE file for details.
