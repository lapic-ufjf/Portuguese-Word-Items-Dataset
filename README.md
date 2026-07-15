# Portuguese-Word-Items-Dataset

This repository contains the qualitative evaluation data and LLM prompt
associated with the paper *Automatic Distractor Generation for Multiple-Choice
Items in Word Reading Assessments*.

The study compares a rule-based linguistic approach with an LLM-based approach
for generating distractor candidates in Brazilian Portuguese word-reading
items.

## Repository contents

```text
.
|-- README.md
|-- data/
|   |-- README.md
|   |-- answer_keys.csv
|   `-- qualitative_evaluations.csv
`-- prompts/
    |-- system_prompt.txt
    `-- user_prompt.txt
```

## Quantitative evaluation data

The quantitative evaluation measured the recovery of distractors from 140 unique answer keys associated with reference items. These items are not included in this repository because they are restricted assessment materials.

## Qualitative evaluation data

The qualitative evaluation comprises 35 answer keys selected by literacy
assessment specialists. For every answer key, GPT-5.2 and the rule-based
approach each produced four ranked lists of 20 candidates. The public table
therefore contains 5,600 candidate evaluations:

```text
35 answer keys x 2 approaches x 4 structural groups x 20 candidates = 5,600
```

Each candidate was blindly assessed according to its plausibility, pedagogical
adequacy, phonological and graphemic proximity to the answer key, and adherence
to the structural constraints of the item template.

## Answer-key profiles

The answer keys are organized into five profiles based on their number of
syllables and whether they are formed exclusively by canonical CV syllables.
The `answer_key_profile` column identifies the structural profile associated
with each answer key.

| Dataset profile | Description |
| --- | --- |
| `canonical_disyllabic` | Heard word with one or two syllables, exclusively in the canonical CV pattern, related to its written representation. |
| `canonical_trisyllabic` | Heard word with three syllables, exclusively in the canonical CV pattern, related to its written representation. |
| `canonical_polysyllabic` | Heard word with four or more syllables, exclusively in the canonical CV pattern, related to its written representation. |
| `noncanonical_disyllabic` | Heard word with one or two syllables in different syllabic patterns, related to its written representation. |
| `noncanonical_polysyllabic` | Heard word with four or more syllables in different syllabic patterns, related to its written representation. |

See [data/README.md](data/README.md) for a description of the CSV files and their columns.


## Prompt and model settings

The exact system and user messages used for LLM-based generation are available
in the [`prompts`](prompts) directory. The `{suporte}` placeholder in the user
message is replaced by the answer-key word for each request.

The following models and generation settings were used:

| Model | Provider | Model identifier | Temperature |
| --- | --- | --- | ---: |
| GPT-5.2 | OpenRouter | `openai/gpt-5.2` | 0 |
| Gemini 2.5 Pro | Google Generative AI (`google_genai`) | `gemini-2.5-pro` | 0 |
| Sabiá-4 | Maritaca AI (`ChatMaritalk`) | `sabia-4` | 0.001 |

> **Note:** The quantitative evaluation included GPT-5.2, Gemini 2.5 Pro, and
> Sabiá-4. As GPT-5.2 achieved the highest performance among the evaluated
> LLMs, it was selected for the subsequent qualitative evaluation.
>
>Sabiá-4 was run with a temperature of `0.001` because the
> `ChatMaritalk` version used in the experiments required a value greater than
> zero. This value was used as a near-zero setting.

## Citation

If you use these data in your research, please cite the following
work:

```bibtex
@inproceedings{automatic_distractor_generation_2026,
  author = {João Augusto Pilato and João Marcelo Amaral and Lucas Larcher and Lara Dias and João Vítor Nogueira and Rosângela Veiga and Begma Tavares and Jairo Francisco de Souza},
  title = {Automatic Distractor Generation for Multiple-Choice Items in Word Reading Assessments},
  booktitle = {Anais do XXXVII Simpósio Brasileiro de Informática na Educação},
  location = {Goiânia/GO},
  year = {2026},
  keywords = {},
  issn = {},
  pages = {},
  publisher = {SBC},
  address = {Porto Alegre, RS, Brasil},
}
```
