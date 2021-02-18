# novelWriter Internationalisation

The `i18n` folder contains the internationalisation files for novelWriter.
There are two types of files. The `nw_XX.qm` files are for localisation of the
main GUI, and the `project_XX.json` files are JSON files with translation maps
for the novelWriter projects.

## GUI Localisation

The `.qm` files are not generated by default. They can be built with:
```bash
python3 setup.py qtlrelease
```

To add a new translation file, please add a new entry in the `novelWriter.pro`
file under the `TRANSLATIONS` variable. Please use the underscore syntax for
file names as the importer expects this format.

After adding the entry in the `.pro` file, run:
```bash
python3 setup.py qtlupdate
```

This will build a new `nw_XX.ts` file for the language you just added. The file
can then be edited with the Qt 5 Linguist application. Please select "English"
and "United Kingdom" as the source langauge when prompted.

When you're done editing, you can build the `nw_XX.qm` file and test it in
novelWriter.

**Note:** This requires that you have the tools Qt 5 Linguist and `pylupdate5`
installed on your system.

## Project Localisation

Projects can have a different language setting than the GUI itself. The files
with format `project_XX.json` are simple translation maps for text that goes
into the exported documents.

The files are loaded based on the main GUI spell check language or the
project's spell check language. The project's spell check language takes
precedence over the GUI spell check language.

Since these are used mainly as replacement lookups, they are maintained as
plain JSON files. The main usage is to generate chapter headers as number
words.

There is no trick to using these files. Just copy the `project_en.json` file,
rename it, and edit it. Please use the underscore as separator if a language
needs to be localised to a specific country under a language. The importer will
for instance look for `en_GB` or `en_US` first, then use `en` if either is not
found. If there are no matching files, the project falls back to using English.