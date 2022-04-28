# UP_Japanese-GSD


## Data Format
This data is in [conllup](https://universaldependencies.org/ext-format.html) format, which adds user defined columns to the original 10 columns from the CoNLL-U format (from UD). Our data consists of four columns: the original `ID` columns, plus three additional columns `UP:PRED`, `UP:ARGHEADS`, and `UP:ARGSPANS`.
- **ID** (column 1) is the token id consistent with corresponding UD sentence.
- **UP:PRED** (column 11) contains predicate sense label for this predicate. This sense provides roleset specific meanings for each of its arguments, as defined in EN propbank.
- **UP:ARGHEADS** (column 12) contains the argument heads for arguments of this predicate. Each argument is in the format `label:token_id`.  The arguments are separated by pipe `|` charactor.
- **UP:ARGSPANS** (column 13) contains the argument spans for arguments of this predicate. Each argument is in the format `label:start_token_id-end_token_id`.  The arguments are separated by pipe `|` charactor.


We provide a python script to combine such a UP file with its corresponding UD file to produce the desired 13 column `.conllup` file. The script is available in [tools](https://github.com/UniversalPropositions/tools) repository: `up2/merge_ud_up.py`. Follow the procedure:
- Download UD from https://lindat.mff.cuni.cz/repository/xmlui/handle/11234/1-4611 
- `git clone https://github.com/UniversalPropositions/Japanese-GSD.git`
- `git clone https://github.com/UniversalPropositions/tools.git`
- `cd tools`
    - Setup tools as per the instructions in [README.md](https://github.com/UniversalPropositions/tools#universal-propositions---tools).
- `python3 up2/merge_ud_up.py --input_ud=<ud_path_to_UD_Japanese-GSD>/ --input_up=<up_path_to_UP_Japanese-GSD>/ --output=<path_to_UD+UP_Japanese-GSD>/`

## Known data quality issues

### Parser quality
- Because of the underlying parser mistakes in identifying the correct lemma for certain verbs, and as we name the frame files based on the lemma in the target language, one might expect to see frame filenames that do not make sense in that particular language.
	
	
### Language peculiarities
- For the languages where subject/object can be omitted, one may expect to observe incorrect role label transfer. One potential reason for such issues is incorrect word alignment.
- `AUX` (be, have, do) in EN is likely to be misaligned with other tokens in other languages. In EN, these `AUX` are used to construct tenses (perfect perfective), polarity etc., but different languages represent tense and polarity differently.