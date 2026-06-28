### User Requirements Specification Document

##### DIBRIS – Università di Genova. Scuola Politecnica, Software Engineering Course 80154

**VERSION : 1.0**

**Authors**
Şermin Beyza Yurdakan
Mehmet Ali Kömürcü

**REVISION HISTORY**

| Version | Date       | Authors    | Notes                                                |
| ------- | ---------- | ---------- | ---------------------------------------------------- |
| 1.0     | 2026-06-28 | Şermin Beyza Yurdakan, Mehmet Ali Kömürcü | First version of the User Requirements Specification |

# Table of Contents

1. [Introduction](#p1)

   1. [Document Scope](#sp1.1)
   2. [Definitions and Acronyms](#sp1.2)
   3. [References](#sp1.3)
2. [System Description](#p2)

   1. [Context and Motivation](#sp2.1)
   2. [Project Objectives](#sp2.2)
3. [Requirements](#p3)

   1. [Stakeholders](#sp3.1)
   2. [Functional Requirements](#sp3.2)
   3. [Non-Functional Requirements](#sp3.3)

<a name="p1"></a>

## 1. Introduction

<a name="sp1.1"></a>

### 1.1 Document Scope

This document defines the first version of the user requirements for the **Italian Text Quality Analyzer**.

The system is a Google Docs add-on that analyzes Italian texts and provides feedback about readability, vocabulary, repetition, sentence complexity, paragraph-level issues, and target audience suitability.

The system is intended to support users during writing and revision. It is not intended to replace a human editor, teacher, or proofreader. The system does not provide full grammar correction; instead, it highlights possible problems and presents analysis results that the user can interpret.

<a name="sp1.2"></a>

### 1.2 Definitions and Acronyms

| Acronym / Term     | Definition                                                                       |
| ------------------ | -------------------------------------------------------------------------------- |
| URS                | User Requirements Specification                                                  |
| NLP                | Natural Language Processing                                                      |
| API                | Application Programming Interface                                                |
| Google Docs Add-on | A tool integrated into Google Docs                                               |
| Google Apps Script | Platform used to connect the Google Docs interface with the backend              |
| Backend            | The Python service that performs the text analysis                               |
| spaCy              | NLP library used to process Italian text                                         |
| FastAPI            | Python framework used to expose the analysis API                                 |
| Gulpease Index     | Italian readability index based on letters, words, and sentences                 |
| SCIX               | Syntactic Complexity Index                                                       |
| LDIX               | Lexical Diversity Index                                                          |
| Base Vocabulary    | Italian basic vocabulary used to evaluate whether words are common or accessible |
| Lemma              | Base form of a word                                                              |
| Target Audience    | Intended reader group selected by the user                                       |
| Named Entity       | A detected person, place, organization, or similar named item                    |
| Analyzed Document  | A generated Google Docs document containing highlights and analysis notes        |
| Report             | Exported PDF or DOCX file containing the analysis results                        |


<a name="p2"></a>

## 2. System Description

<a name="sp2.1"></a>

### 2.1 Context and Motivation

The project aims to help users evaluate Italian texts directly inside Google Docs.

Text quality cannot be represented by a single value. A text can have an acceptable readability score but still contain difficult sentences, repeated words, weak paragraph transitions, or vocabulary that is not suitable for the intended audience. For this reason, the system provides several complementary indicators instead of one final judgment.

The analyzer supports the user by showing where the text may be hard to read, lexically repetitive, syntactically complex, or unsuitable for selected reader profiles. The user remains responsible for deciding whether the highlighted parts should be changed.

<a name="sp2.2"></a>

### 2.2 Project Objectives

The main objective of the project is to create a Google Docs-based analyzer for Italian texts. The user should be able to open the analyzer from Google Docs, select one or more target audiences, run the analysis, and review the results in the sidebar.

The system calculates several metrics. The **Gulpease Index** is used to estimate the readability of the text for Italian readers. A higher Gulpease value generally indicates easier readability. However, the interpretation of the score depends on the selected target audience. For example, the same score may be acceptable for academic readers but difficult for elementary school readers.

The **Lexical Diversity Index** is used to estimate how varied the vocabulary is. This helps the user understand whether the text uses a limited or varied set of words. This value is not treated as a quality judgment by itself, because repetition can sometimes be intentional.

The **Syntactic Complexity Index** is used to identify texts or sentences that may be structurally complex. The system uses this metric to detect sentence structures that may require more reading effort. High syntactic complexity is not always an error, especially in literary or academic texts, so the result is presented as a warning signal rather than a correction.

The **Base Vocabulary analysis** is used to check how many words belong to a basic Italian vocabulary list. Words outside the Base Vocabulary are shown as possible misspellings or non-base vocabulary items. This does not mean that the word is certainly wrong; it may also be a technical, literary, rare, or domain-specific word.

The system also detects **lemma-based repetitions**. This means that different forms of the same word can be grouped together. For example, repeated forms of the same lemma can be shown as a repetition even if the exact word form changes.

The system provides **sentence-level** and **paragraph-level** feedback. Sentence-level feedback helps the user locate difficult sentences. Paragraph-level feedback helps the user understand local readability and possible structural issues.

The system also generates an **analyzed document**. In this document, the original text is reproduced with visual highlights and analysis notes. The system also exports a report in PDF or DOCX format.

<a name="p3"></a>

## 3. Requirements

| Priorità | Significato                                                     |
| -------- | --------------------------------------------------------------- |
| M        | **Mandatory:** required for the first working version           |
| D        | **Desiderable:** useful but not essential for the first version |
| O        | **Optional:** may be added				                         |
| E        | **Future Enhancement:** planned for a later version             |

<a name="sp3.1"></a>

### 3.1 Stakeholders

| Stakeholder       | Description                                                                                                      |
| ----------------- | ---------------------------------------------------------------------------------------------------------------- |
| Writer            | Uses the analyzer to revise Italian texts and identify possible readability or vocabulary issues.                |
| Student           | Uses the analyzer to check Italian texts during writing or revision.                                             |
| Teacher           | Uses the analyzer to evaluate whether a text is suitable for a specific reader group.                            |
| Editor            | Uses the analyzer to identify difficult sentences, paragraph-level issues, repetitions, and vocabulary problems. |
| Project team      | Designs, implements, tests, and documents the system.                                                            |

<a name="sp3.2"></a>

### 3.2 Functional Requirements

| ID    | Descrizione                                                                                                                                                                                     | Priorità |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| FR-1  | The system shall allow the user to open the text analyzer from Google Docs.                                                                                                                     | M        |
| FR-2  | The system shall provide a sidebar interface where the user can run the analysis and review the results.                                                                                        | M        |
| FR-3  | The system shall allow the user to select one or more target audiences before starting the analysis.                                                                                            | M        |
| FR-4  | The system shall analyze the text contained in the current Google Docs document.                                                                                                                | M        |
| FR-5  | The system shall calculate global text statistics, including number of words, unique words, sentences, and letters.                                                                             | M        |
| FR-6  | The system shall calculate the Gulpease Index for the whole document.                                                                                                                           | M        |
| FR-7  | The system shall calculate the Lexical Diversity Index for the whole document.                                                                                                                  | M        |
| FR-8  | The system shall calculate the Syntactic Complexity Index for the whole document.                                                                                                               | M        |
| FR-9  | The system shall provide an interpretation of the analysis according to each selected target audience.                                                                                          | M        |
| FR-10 | The system shall display the target audience analysis in a table.                                                                                                                               | M        |
| FR-11 | The system shall identify sentences that may be difficult because of low readability, excessive length, punctuation density, or high syntactic complexity.                                      | M        |
| FR-12 | The system shall display sentence-level warnings in the sidebar.                                                                                                                                | M        |
| FR-13 | The system shall allow the user to select a warning sentence in the original Google Docs document from the sidebar.                                                                             | D        |
| FR-14 | The system shall analyze the text at paragraph level.                                                                                                                                           | M        |
| FR-15 | The system shall identify paragraphs that may have readability, length, syntactic complexity, or cohesion-related issues.                                                                       | M        |
| FR-16 | The system shall display paragraph-level warnings in the sidebar.                                                                                                                               | M        |
| FR-17 | The system shall allow the user to select a warning paragraph in the original Google Docs document from the sidebar.                                                                            | D        |
| FR-18 | The system shall detect repeated lemmas in the text.                                                                                                                                            | M        |
| FR-19 | The system shall display repeated lemmas with their frequency and word forms.                                                                                                                   | M        |
| FR-20 | The system shall calculate Base Vocabulary coverage for the analyzed text.                                                                                                                      | M        |
| FR-21 | The system shall identify words that are outside the Base Vocabulary.                                                                                                                           | M        |
| FR-22 | The system shall present words outside the Base Vocabulary as non-base vocabulary items.        						                                                                          | M        |
| FR-23 | The system shall display possible misspellings or non-base vocabulary items with their frequency and word forms.                                                                                | M        |
| FR-24 | The system shall detect named entities in the text.                                                                                                                                             | D        |
| FR-25 | The system shall display detected named entities grouped by type.                                                                                                                               | D        |
| FR-26 | The system shall provide an analysis overview summarizing the main findings of the analysis.                                                                                                    | M        |
| FR-27 | The system shall generate a separate analyzed Google Docs document.                                                                                                                             | M        |
| FR-28 | The analyzed document shall include a legend explaining the meaning of the highlight colors.                                                                                                    | M        |
| FR-29 | The analyzed document shall highlight sentence-level warnings.                                                                                                                                  | M        |
| FR-30 | The analyzed document shall highlight repeated lemma forms.                                                                                                                                     | M        |
| FR-31 | The analyzed document shall highlight possible misspellings or non-base vocabulary items.                                                                                                       | M        |
| FR-32 | The analyzed document shall include global metrics, target audience analysis, analysis overview, Base Vocabulary analysis, paragraph-level information, lemma repetitions, and named entities.  | M        |
| FR-33 | The system shall export the analysis report as a PDF file.                                                                                                                                      | M        |
| FR-34 | The system shall export the analysis report as a DOCX file.                                                                                                                                     | M        |
| FR-35 | The exported report shall include global metrics, target audience analysis, sentence-level warnings, paragraph-level warnings, Base Vocabulary analysis, lemma repetitions, and named entities. | M        |
| FR-36 | The system may provide grammar correction in a future version.                                                                                                                                  | E        |
| FR-37 | The system may provide automatic text simplification suggestions in a future version.                                                                                                           | E        |

<a name="sp3.3"></a>

### 3.3 Non-Functional Requirements

| ID     | Descrizione                                                                                                                                     | Priorità |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| NFR-1  | The system shall be usable by non-technical users.                                                                                              | M        |
| NFR-2  | The sidebar shall organize results into clearly separated sections.                                                                             | M        |
| NFR-3  | The sidebar shall use pagination or scrollable areas when result lists or tables are long.                                                      | M        |
| NFR-4  | The system shall preserve the original Google Docs document when generating the analyzed document.                                              | M        |
| NFR-5  | The system shall clearly indicate that analysis results are warning signals and not absolute judgments.                                         | M        |
| NFR-6  | The system shall clearly indicate that a word outside the Base Vocabulary is not necessarily a spelling error.                                  | M        |
| NFR-7  | The system shall provide clear feedback when the document is empty.                                                                             | M        |
| NFR-8  | The system shall provide clear feedback when the backend service is unavailable or returns an error.                                            | M        |
| NFR-9  | The exported PDF and DOCX reports shall be readable as standalone documents.                                                                    | M        |
| NFR-10 | The analyzed document shall use consistent colors for the same type of warning or highlight.                                                    | M        |
| NFR-11 | The system shall use Italian-specific readability and vocabulary analysis.                                                                      | M        |
| NFR-12 | The system shall allow new target audience profiles to be added.													                               | O        |
| NFR-13 | The system should support improved performance for long documents in a future version.                                                          | E        |
| NFR-14 | The system should support more advanced NLP or grammar-related modules in a future version.                                                     | E        |
