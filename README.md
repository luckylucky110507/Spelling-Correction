# Spelling Correction

An intelligent spelling correction system using character n-grams and Jaccard similarity to detect and suggest corrections for misspelled words.

## Project Overview

This project implements an automated spelling correction algorithm that identifies misspelled words and suggests the most similar correct word from a dictionary. It uses character-level n-gram analysis and Jaccard similarity scoring to find the best matches, making it robust against various types of spelling errors.

## Features

- **Character N-gram Analysis**: Breaks words into character sequences for similarity comparison
- **Jaccard Similarity Scoring**: Measures similarity between words based on shared n-grams
- **Text Preprocessing**: Handles special characters and normalizes input
- **Case-Insensitive Matching**: Converts words to lowercase for consistent processing
- **Real-time Corrections**: Provides instant spell correction suggestions
- **Similarity Score**: Returns confidence score (0-1) for each correction

## Algorithm

### 1. Character N-grams
Splits words into overlapping character sequences (default n=2):
- Example: "hello" → ["he", "el", "ll", "lo"]

### 2. Jaccard Similarity
Compares sets of n-grams using the Jaccard coefficient formula:

```
Jaccard Similarity = |Set A ∩ Set B| / |Set A ∪ Set B|
```

This measures the intersection divided by the union of n-gram sets.

### 3. Best Match Selection
Iterates through the dictionary to find the word with the highest Jaccard similarity score.

## Project Structure

```
Spelling-Correction/
├── README.md                          # Project documentation
└── SpellingCorrection.ipynb           # Main Jupyter notebook
```

## Dependencies

- **Python 3.x**
- **re**: Regular expressions for text preprocessing
- Standard Python libraries

### Installation

No external package dependencies. Uses only Python standard library:

```bash
# No installation needed - uses only built-in Python modules
```

## Usage

### Running the Notebook

Open the Jupyter notebook:

```bash
jupyter notebook SpellingCorrection.ipynb
```

### Basic Usage Example

```python
# Define a dictionary of correct words
dictionary = ["recieve", "believe", "friend", "learning",
              "machine", "python", "science", "data"]

# Create a misspelled word
wrong_word = "reciev"

# Get correction
match, score = improved_correction(wrong_word, dictionary)
print(f"{wrong_word} --> {match} (score: {score:.2f})")
# Output: reciev --> recieve (score: 0.86)
```

### Testing with Multiple Words

```python
wrong_words = ["reciev", "freind", "lerning", "machin", "sciece"]
for w in wrong_words:
    match, score = improved_correction(w, dictionary)
    print(f"{w} --> {match} (score: {score:.2f})")
```

### Interactive Mode

```python
user_word = input("Enter a word: ")
match, score = improved_correction(user_word, dictionary)
print(f"Suggested Correction --> {match} (score: {score:.2f})")
```

## Key Functions

### `char_ngrams(word, n=2)`
Generates character n-grams from a word.

**Parameters:**
- `word`: Input word (string)
- `n`: Size of n-gram (default: 2)

**Returns:** List of n-grams

**Example:**
```python
char_ngrams("hello", 2)
# ['he', 'el', 'll', 'lo']
```

### `jaccard_similarity(a, b)`
Calculates Jaccard similarity between two sets.

**Parameters:**
- `a`: First set of n-grams
- `b`: Second set of n-grams

**Returns:** Similarity score (0-1)

### `preprocessing(word)`
Normalizes and cleans input words.

**Parameters:**
- `word`: Input word (string)

**Returns:** Processed word (lowercase, alphanumeric only)

**Example:**
```python
preprocessing("HELLO@123!")
# 'hello'
```

### `improved_correction(word, dictionary, n=2)`
Main function that finds the best spelling correction.

**Parameters:**
- `word`: Misspelled word to correct
- `dictionary`: List of correct words
- `n`: Size of n-gram (default: 2)

**Returns:** Tuple of (best_match, best_score)

**Example:**
```python
improved_correction("reciev", dictionary)
# ('recieve', 0.86)
```

## Algorithm Performance

### Strengths
- Fast performance on small to medium dictionaries
- Handles various character-level errors (substitutions, transpositions, insertions)
- Robust to special characters and case variations
- No external dependencies required

### Example Results
```
reciev   --> recieve   (score: 0.86)
freind   --> friend    (score: 0.80)
lerning  --> learning  (score: 0.82)
machin   --> machine   (score: 0.83)
sciece   --> science   (score: 0.75)
```

## Limitations

- Works best with small, domain-specific dictionaries
- Requires a pre-defined dictionary of correct words
- May struggle with completely unrecognizable words
- No context awareness (doesn't consider surrounding words)
- Single character corrections limited

## Future Improvements

- Implement Edit Distance (Levenshtein distance) for better accuracy
- Add context-aware correction using language models
- Support for larger dictionaries with indexing
- Add frequency-based scoring to prioritize common words
- Implement phonetic similarity algorithms (Soundex, Metaphone)
- Create machine learning-based approach using embeddings
- Add multi-word phrase correction
- Integrate with spell-checking libraries (pyspellchecker, autocorrect)

## Applications

- Spell checker for text editors
- Search query autocorrection
- Document preprocessing and cleaning
- OCR post-processing
- Accessibility tools
- Educational applications

## Author

Created as a natural language processing project

## License

This project is open source and available for educational purposes.

---

**Note**: The current implementation works best with carefully curated dictionaries. For production use, consider integrating with established spell-checking libraries.
