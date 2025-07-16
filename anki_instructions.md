### Anki Note Type Configuration Guide

This guide outlines the setup for two distinct Anki note types suitable for different linguistic contexts: one for Roman alphabet languages without phonetic transcriptions and another specifically for Hanzi/Kanji-based languages incorporating Pinyin.

---

#### 1. Standard Note Type (Roman Alphabet, no Pinyin)

This note type is designed for general vocabulary, where a word is presented, followed by a sentence and its meaning.

##### 1.1. Creating the Note Type

1.  Open Anki and navigate to `Tools` -> `Manage Note Types...`.
2.  Click `Add` to create a new note type.
3.  Select `Add: Basic (and reversed card)` and click `OK`.
4.  Provide a descriptive name, such as "Standard Vocabulary" or "Basic Word Card", and click `OK`.
5.  With your newly created note type selected, click `Fields...`.
6.  Configure the fields to match the structure depicted in the image below. Ensure you have the fields: `Word`, `Meaning`, and `Sentence`. You can use the `Add`, `Delete`, `Rename`, and `Reposition` buttons as needed.
    <div style="text-align: center;">
        <img src="https://github.com/user-attachments/assets/cc772b16-e788-4942-b4b0-5340053c16c2"; alt="Anki Fields for Standard Note Type" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
    </div>
    
7.  Click `Save` and then `Close`.

##### 1.2. Configuring the Card Template

1.  From the `Manage Note Types...` window, with "Standard Vocabulary" selected, click `Cards...`.
2.  Configure the Front Template, Back Template, and Styling sections as follows:

    **Front Template:**
    ```html
    <div id="word">{{Word}}</div>

    <div id="sentence-container">{{Sentence}}</div>

    <div id="word-to-highlight" style="display:none;">{{Word}}</div>

    <script>
      // Check if we are on the front side of the card before running
      if (document.getElementById("answer") === null) {
        var sentenceDiv = document.getElementById("sentence-container");
        var wordDiv = document.getElementById("word-to-highlight");
        
        if (sentenceDiv && wordDiv) {
          var sentence = sentenceDiv.innerHTML;
          var word = wordDiv.innerHTML;
          
          // This regular expression finds all instances of the word and replaces them
          var highlighted = sentence.replace(new RegExp(word, "g"), "<b>" + word + "</b>");
          
          sentenceDiv.innerHTML = highlighted;
        }
      }
    </script>
    ```

    **Back Template:**
    ```html
    {{FrontSide}}

    <hr>

    <div id="answer">
      <div class="translation">{{Meaning}}</div>
    </div>
    ```

    **Styling:**
    ```css
    /* --- General Card Styling --- */
    .card {
      font-family: 'Helvetica Neue', 'KaiTi', 'Microsoft YaHei', sans-serif;
      text-align: center;
      /* Softer background and text colors for easier reading */
      background-color: #fbfaf7; /* A very light, warm off-white */
      color: #3b3b3b;      /* A softer, dark gray for text */
    }

    /* --- Front Side --- */

    #word {
      font-size: 64px; /* Large and clear */
      font-weight: 600;
      margin-bottom: 20px;
      color: #1e1e1e; /* Near-black for high contrast */
    }

    /* The example sentence container */
    #sentence-container {
      font-size: 16px; /* Smallest font size for context */
      line-height: 1.45;
      color: #5d5d5d; /* Mid-gray to de-emphasize */
      padding: 0 20px; /* Adds space on the sides for long text */
      text-align: left; /* Aligns long sentences for better readability */
      word-wrap: break-word; /* Ensures very long words don't overflow */
    }

    /* The highlighted word within the sentence */
    b {
      color: #005a9c; /* A deeper, less saturated blue */
      font-weight: 600;
    }


    /* --- Back Side --- */

    /* The separator line */
    hr {
      border: 0;
      border-top: 1px solid #e8e8e8; /* A very light gray line */
      margin: 20px auto;
      width: 80%;
    }

    /* Container for the answers */
    #answer {
      display: flex;
      flex-direction: column;
      gap: 15px; /* Space between Pinyin and Translation */
    }

    /* Translation/Meaning styling */
    .translation {
      font-size: 28px;
      color: #3b3b3b;
    }
    ```
3.  Click `Close` to save your card template changes.

---

#### 2. Hanzi/Kanji Note Type (with Pinyin)

This note type is tailored for languages like Chinese or Japanese, providing fields for the character, its Pinyin/reading, a sentence, and the meaning.

##### 2.1. Creating the Note Type

1.  Open Anki and navigate to `Tools` -> `Manage Note Types...`.
2.  Click `Add` to create a new note type.
3.  Select `Add: Basic (and reversed card)` and click `OK`.
4.  Provide a descriptive name, such as "Chinese/Japanese Characters" or "Hanzi Card", and click `OK`.
5.  With your newly created note type selected, click `Fields...`.
6.  Configure the fields to match the structure depicted in the image below. Ensure you have the fields: `Word`, `Meaning`, `Pinyin`, and `Sentence`. You can use the `Add`, `Delete`, `Rename`, and `Reposition` buttons as needed.
    <div style="text-align: center;">
        <img src="https://github.com/user-attachments/assets/b07f094d-4bc3-4c21-9239-222eebdc7937" alt="Anki Fields for Hanzi/Kanji Note Type" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
    </div>
    
7.  Click `Save` and then `Close`.

##### 2.2. Configuring the Card Template

1.  From the `Manage Note Types...` window, with "Chinese/Japanese Characters" selected, click `Cards...`.
2.  Configure the Front Template, Back Template, and Styling sections as follows:

    **Front Template:**
    ```html
    <div id="word">{{Word}}</div>

    <div id="sentence-container">{{Sentence}}</div>

    <div id="word-to-highlight" style="display:none;">{{Word}}</div>

    <script>
      // Check if we are on the front side of the card before running
      if (document.getElementById("answer") === null) {
        var sentenceDiv = document.getElementById("sentence-container");
        var wordDiv = document.getElementById("word-to-highlight");
        
        if (sentenceDiv && wordDiv) {
          var sentence = sentenceDiv.innerHTML;
          var word = wordDiv.innerHTML;
          
          // This regular expression finds all instances of the word and replaces them
          var highlighted = sentence.replace(new RegExp(word, "g"), "<b>" + word + "</b>");
          
          sentenceDiv.innerHTML = highlighted;
        }
      }
    </script>
    ```

    **Back Template:**
    ```html
    {{FrontSide}}

    <hr>

    <div id="answer">
      <div class="pinyin">{{Pinyin}}</div>
      <div class="translation">{{Meaning}}</div>
    </div>
    ```

    **Styling:**
    ```css
    /* --- General Card Styling --- */
    .card {
      font-family: 'Helvetica Neue', 'KaiTi', 'Microsoft YaHei', sans-serif;
      text-align: center;
      /* Softer background and text colors for easier reading */
      background-color: #fbfaf7; /* A very light, warm off-white */
      color: #3b3b3b;      /* A softer, dark gray for text */
    }

    /* --- Front Side --- */

    /* The main Chinese word */
    #word {
      font-size: 64px; /* Large and clear */
      font-weight: 600;
      margin-bottom: 20px;
      color: #1e1e1e; /* Near-black for high contrast */
    }

    /* The example sentence container */
    #sentence-container {
      font-size: 16px; /* Smallest font size for context */
      line-height: 1.45;
      color: #5d5d5d; /* Mid-gray to de-emphasize */
      padding: 0 20px; /* Adds space on the sides for long text */
      text-align: left; /* Aligns long sentences for better readability */
      word-wrap: break-word; /* Ensures very long words don't overflow */
    }

    /* The highlighted word within the sentence */
    b {
      color: #005a9c; /* A deeper, less saturated blue */
      font-weight: 600;
    }


    /* --- Back Side --- */

    /* The separator line */
    hr {
      border: 0;
      border-top: 1px solid #e8e8e8; /* A very light gray line */
      margin: 20px auto;
      width: 80%;
    }

    /* Container for the answers */
    #answer {
      display: flex;
      flex-direction: column;
      gap: 15px; /* Space between Pinyin and Translation */
    }

    /* Pinyin styling */
    .pinyin {
      font-size: 30px;
      color: #b33939; /* A muted, earthy red */
    }

    /* Translation/Meaning styling */
    .translation {
      font-size: 28px;
      color: #3b3b3b;
    }
    ```
3.  Click `Close` to save your card template changes.

How it should look like:
    <div style="text-align: center;">
        <img src="https://github.com/user-attachments/assets/24caf46f-1c26-473c-9fe8-dd991660bbc7" alt="Anki Fields for Hanzi/Kanji Note Type" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">
    </div>


### Adding Audio to Your Cards (Optional)

To enhance your Anki cards with automated audio, we recommend utilizing the **HyperTTS** add-on. This add-on integrates various text-to-speech services, allowing you to generate and embed audio for your fields directly within Anki.

1.  **Install HyperTTS:**
    * Open Anki.
    * Go to `Tools` -> `Add-ons` -> `Browse & Install...`.
    * Enter the AnkiWeb add-on code for HyperTTS (you can find this on the [HyperTTS AnkiWeb page](https://ankiweb.net/shared/info/111623432)), then click `OK`.
    * Restart Anki to complete the installation.

2.  **Configure and Use HyperTTS:**
    * For a comprehensive guide on configuring HyperTTS with your preferred text-to-speech services (e.g., Google Translate, Azure, Amazon Polly) and integrating it into your note types, refer to the official HyperTTS documentation:
        * [HyperTTS Official Guide](https://hypertts.com/docs/latest/guide.html)

    HyperTTS will allow you to add audio to fields like `Word` and `Sentence` for both the "Standard Note Type" and the "Hanzi/Kanji Note Type," providing an auditory component to your learning.


### Importing Data from Your Script's Output TXT File

This section guides you through importing the `.txt` file generated by this repository's script into Anki. It ensures your data is correctly imported, with proper column handling, and assigned to the right deck and note type for your studies.

1.  **Find Your Script's Output TXT File:**
    After running the script from this repository, you'll have a `.txt` file (likely named something like `output.txt`). This file is already formatted with **tabs separating the fields**, making it ready for Anki's import process.

    * **How the script formats your TXT file:**
        * For Roman alphabet content (for the "Standard Note Type"), columns will typically be: `Word`, `Meaning`, `Sentence`.
        * For Hanzi/Kanji content (for the "Hanzi/Kanji Note Type"), columns usually are: `Word`, `Meaning`, `Pinyin`, `Sentence`.
    * There's no need to manually edit this `.txt` file; the script handles the tab separation for you.

2.  **Start the Import in Anki:**
    * Open Anki.
    * From the main Anki window, go to `File` -> `Import...`.
    * Locate and select the `.txt` file generated by the script, then click `Open`.

3.  **Set Up Import Options:**
    The "Import" dialog is where you tell Anki how to understand your file. Pay close attention here:

    * **Type:** Use the "Type" dropdown to select the **Note Type** that matches the data in your `.txt` file.
        * If the script's output is for general Roman alphabet words: Choose "Standard Vocabulary" (or whatever name you gave it).
        * If the script's output includes Pinyin/readings for Chinese/Japanese: Choose "Chinese/Japanese Characters" (or your chosen name).
    * **Deck:** Use the "Deck" dropdown to pick the **Deck** where you want your new notes to go. You can also create a new deck right from here.
    * **Fields separated by:** Make sure this option is set to **"Tabs"**. Anki usually detects this automatically, but it's good to confirm.
    * **Fields in your file:** This crucial section shows a preview of your script's data. For each numbered column in the preview, use the dropdown menu to select the correct Anki field that corresponds to the data in that column.
        * **For "Standard Note Type" output:** The first column usually maps to `Word`, the second to `Meaning`, and the third to `Sentence`.
        * **For "Hanzi/Kanji Note Type" output:** The first column maps to `Word`, the second to `Meaning`, the third to `Pinyin`, and the fourth to `Sentence`.

4.  **Finish the Import:**
    * Once all your fields are correctly matched, click `Import`.
    * Anki will show a quick summary of what was imported. Click `Close`.

Your notes, generated by the script and now perfectly formatted, will appear in your chosen Anki deck, ready for you to come make use of them someday;  "Someday sounds a lot like the thing people say when they actually mean 'never'"
