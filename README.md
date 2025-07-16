# SmartBook-XLSX-Flashcard-ANKI-Converter
Converts your XLSX files exported from the Smartbook App into simply Anki-ready text files. Also removes duplicates, seperates by language and, if desired, quotes.
THis ReadMe will also have specific instructions about how to configure Anki.
![Python Version](https://img.shields.io/badge/python-3.7+-blue.svg)

***
This script is tailored specifically to the [Smartbook App]("https://smart-book.net/")! 
If the amount of columns in the output text file for Chinese or Japanese (it does not discriminate between the two) will automatically be different than it would be for language using the roman alphabet; both the anki cards and text files are slighlty different to accomodate the extra Pinyin column.

In the anki_instructions.md file are, who would have guessed it, [instructions for anki](anki_instructions.md); specifically about how to best configure Anki to have it jibe well with the output of this script and nice looking like this: ![Front Side](https://i.imgur.com/N7pJRRN.png) ![Back Side](https://i.imgur.com/rVdBqxO.png)


## Key Features

* **🗂️ Can sort by language automatically, in ~~most~~ some cases**: (Fallback method) Automatically attempts to detect whether a book is English (`en`), French (`fr`), and Chinese/Japanese (`zh`) by consulting several simple heuristics. Scores a books name, an info in the XLSX file, for how often they have letter combinations in them of which language; For example if a books title has a "The", it's plus 1 added to the text for English flashcards, and if it has something like " l'", it's assumed to be French.
* **⚙️ External Configuration**: Upon first launch, creates `config.json` file which allows one to manually assign languages to specific book names (or just keywords occuring in their name), overriding the automatic detection when needed.
*But all that language detection stuff is only relevant when the xlsx file contains flashcards in several languages and you want it sorted because that would be nice.*
* **🔪 Cutoff point**: You may choose some flashcard's word to have the script ignore all flashcards older (less recent and located later in the xlsx file).
* **🗑️ Rather Intelligent Deduplication**: (Optional) Applies a very specific kind of deduplication, where when there are several flashcards for the same word, it either the ones that doesn't have an example sentence, or, when both have the same one, it deletes the one with fewer characters in the translation/meaning-column. 
* **🤯 Quote & Idiom Separation**: If you manually set the "the part of speech" (it's usually something like "verb" or "word" by default), inside the Smartbook App, to something not otherwise used, you can thus demarcate, for you and the script, flashcards that are actually just containing excerpts/quotes of sentence you found marvellously written and wanted to save to remind yourself of it at some later date – that's might be a bit very much specific but I made it for myself in the first place, so deal with it😁.
* **🖥️ Interactive & User-Friendly**: Runs in the command line with clear prompts for the input file and other options.
* **⏱️ Timestamped Output**: Creates a new, timestamped output folder for each run, so you never overwrite previous exports. Neither does it override the xlsx file – it just reads it.

***

### 1. Prerequisites

Make sure you have **Python 3.7** or newer installed.

You will also need two Python libraries: `pandas` and `openpyxl`. You can install them using pip:

```bash
pip install pandas openpyxl
```

### 2. Setup

1.  **Download the Script**: Place the `flashcard_converter.py` script in a folder on your computer.
2.  **Add Your Flashcards**: Export your vocabulary from the SmartBook app as an `.xlsx` file and place it in the **same folder** as the script. By default, the script looks for a file named `smart-book-dictionary.xlsx`.

### 3. How to Use

1.  **Open a Terminal**: Navigate to the folder containing the script and your `.xlsx` file.
2.  **Run the Script**: Execute the script by typing:
    ```bash
    python flashcard_converter.py
    ```
3.  **Enter Filename (Optional)**: The script will prompt you for the name of your `.xlsx` file.
    * You can type the name of your file (e.g., `my_export.xlsx`) and press Enter.
    * Or, just press **Enter** to use the default filename (`smart-book-dictionary.xlsx`).
4.  **Handle Quotes (If any)**: If the script finds cards marked as `parenthesis`, it will ask if you want to separate them. Type `y` (yes) or `n` (no) and press Enter.
5.  **Done!**: The script will process your file and create a new folder named `flashcard_output_[timestamp]` containing your clean `.txt` files.

![output_example]([https://i.imgur.com/g8vU4k5.png](https://imgur.com/a/rCsAqxv))

## 🛠️ Configuration (Optional)

For most cases, the automatic language detection works well. However, if a book title is ambiguous, you can force a language using the `config.json` file.

If `config.json` does not exist, the script will create one for you the first time it runs. It will look like this:

```json
{
    "_comment_1_purpose": "This file lets you manually assign a language to flashcards from specific books. This is only needed if your spreadsheet contains flashcards from multiple languages and the script cannot automatically detect them.",
    "_comment_2_how_it_works": "Add book titles (or unique keywords from them) from the 'chapter' column of your XLSX file into the 'language_map' section below. The script will check if these keywords are present and assign the corresponding language code (e.g., 'en', 'fr', 'zh').",
    "_comment_3_example_template": {
        "三体": "zh",
        "On the Heights of Despair": "en",
        "La chute dans le temps": "fr"
    },
    "language_map": {
        "Your Book Title Here": "en",
        "Un Autre Titre": "fr"
    }
}
```
To add a rule, simply add an entry to the `language_map` with a unique keyword from the book's title and the desired language code (`en`, `fr`, or `zh`).


## Acknowledgements

The **SmartBook XLSX Flashcard Anki Converter** script itself is released under the [MIT License](https://opensource.org/licenses/MIT).

This project depends on third-party libraries:
* **pandas**: [BSD 3-Clause "New" or "Revised" License](https://opensource.org/licenses/BSD-3-Clause) [pandas Project Website](https://pandas.pydata.org/)
* **openpyxl**: [MIT License](https://opensource.org/licenses/MIT) [openpyxl Documentation](https://openpyxl.readthedocs.io/en/stable/)
