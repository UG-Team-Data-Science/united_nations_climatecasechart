# Data

All cases and included documents from [climatecasechart.com](https://climatecasechart.com/non-us-jurisdiction/), that

 - are Non-US jurisdiction
 - filed in a WHO53 country
   - or Arbitral Tribunal, European Committee on Social Rights, European Union, International Courts & Tribunals, World Trade Organization United Nations OECD
 - have an (estimated) filing year, estimated if not specified by earliest document filing date, and
 - that filing year is from 2011 up to and including 2024.

For these cases all documents are collected where available. Ten documents gave server errors and were also listed as 'Not Available', and hence were excluded. Ten more were not listed as unavailable, but had no download link associated to them and also has to be excluded. This left 899 documents. The vast majority of these were PDF, but some DOCX and PNG files were converted to PDF using respectively MSWORD and Eye of Gnome to support consistent processing.

# Method

**text extraction** All documents were organized by case and processed using [Surya](https://github.com/VikParuchuri/surya) to determine a reading order and ensure inclusion of scanned documents. Since PDF is a visual data format, some with digital text contained duplicated texts, e.g. to facilitate drop shadows. To avoid superfluous counting, the visualy intended text as found by OCR is used rather than the digital text. This introduced spelling errors, due to OCR misdetections causing false negatives on term searches. However, errors do not occur often and hence were disregarded.

**keyword matching** For all documents, the language was detected by [langdetect](https://github.com/Mimino666/langdetect), and all search terms are translated to those languages using Google Translate. To avoid matching partally on word, e.g. 'healthy' for the keyword 'health', all search terms and PDFs were tokenized using [nltk](https://www.nltk.org/)'s `TreebankWordTokenizer`, and keywords are matched on full tokens and language specifially.

**keyword evaluation** We iteratively judged the quality of keywords in their context, by manually evaluating the relavance of their use to climate health in a context window of their paragraph as determined by surya and one or more neighboring paragraps including at least 250 characters before and after. This means that areas with multiple matched are sometimes grouped into one such context.

**in-context learning** We experimented with using the `llama-3.1-8b-instruct-fp8` LLM-model to automatically determine the relevance of the matched keywords in these contexts, and to determine whether particular minorities like women, workers, children or elderly were mentioned in that regard, but haven't used this for the end result.


For details of the processing, we provide a [github](https://github.com/UG-Team-Data-Science/united_nations_climatecasechart/tree/main) and [intermediate results](https://huggingface.co/datasets/prhbrt/united_nations_climatecasechart/) as [pickle](https://docs.python.org/3/library/pickle.html)s and JSONs.
