# DistillRecDial
Conversational Recommender Systems (CRSs) facilitate item discovery through multi-turn dialogues that elicit user preferences via natural language interaction. This field has gained significant attention following advancements in Natural Language Processing (NLP) enabled by Large Language Models (LLMs). However, current CRS research remains constrained by datasets with fundamental limitations. Human-generated datasets suffer from inconsistent dialogue quality, limited domain expertise, and insufficient scale for real-world application, while synthetic datasets created with proprietary LLMs ignore the diversity of real-world user behavior and present significant barriers to accessibility and reproducibility. The development of effective CRSs depends critically on addressing these deficiencies. To this end, we present **DistillRecDial**, a novel conversational recommendation dataset generated through a knowledge distillation pipeline that leverages smaller, more accessible open LLMs. Crucially, **DistillRecDial** simulates a range of user types with varying intentions, preference expression styles, and initiative levels, capturing behavioral diversity that is largely absent from prior work.  
Human evaluation demonstrates that our dataset significantly outperforms widely adopted CRS datasets in dialogue coherence and domain-specific expertise, indicating its potential to advance the development of more realistic and effective conversational recommender systems.

## Where can I find the DistillRecDial dataset?
> [!IMPORTANT]
DistillRecDial exceeds GitHub storage quota, for this reason it is only available through Hugging Face: https://huggingface.co/datasets/planeB/DistillRecDial
## DistillRecDial Generation Scripts
> [!TIP]
To support researchers wanting to extend or adapt our approach we release the scripts used to generate the DistillRecDial dataset.
### Setting Up the Environment
1. Create a virtual environment (Python 3.10.12 recommended):
   ```sh
   python -m venv env
   source env/bin/activate  # On Windows: `env\Scripts\activate`
   ```
2. Install dependencies:
   ```sh
   pip install -r requirements.txt
   ```
### Data Sources
The data sources needed to re-build DistillRecDial from scratch are:
* Amazon Reviews Dataset 2023: Movies and TV category (downloaded through the createDatasetToConversation_tmdb.py)
* Item features sourced from TMDB: available in the Hugging Face repository as tmdb_movies.json
* Visual captions from VLM: already included in tmdb_movies.json
### Main Scripts
- **`createDatasetToConversation_tmbdb.py`**  
  Handles the preprocessing of multiple data sources - Amazon Movies and TV, TMDB metadata, and visual captions from VLM - to populate prompt templates for dataset creation.
- **`knowledgeDistillationDataset.py`**  
  Formats the dialogues generated by the teacher model for supervised fine-tuning of the student model.
- **`exportConversationDataset.py`**  
  Post-processes the student-generated dialogues and splits the data into training, validation, and test sets to produce the final **DistillRecDial** dataset.
### Additional Scripts
- **`prompts.py`**  
  Defines the prompt templates used to simulate various user stereotypes during dialogue generation.
- **`ConvertToCrsLab.py`**  
  Converts the DistillRecDial dataset into the CRSLab-compatible format.
- **`EntityMentionDetector.py`**  
  Supports `ConvertToCrsLab.py` by performing Named Entity Recognition (NER) on dialogue content.
