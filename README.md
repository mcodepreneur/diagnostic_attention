WARNING: This was written before the current unit in my applied NLP course. This proposal might need to be overhauled to make more use of autoregressive language models. Also the implementation of neural retrieval is notably ambiguious, but would entail clarification and creation of a (custom) neural interaction.\
\
This is a theoretical investigation (and pilot development strategy) into the application of deep language models in creating psychotherapist assistant software sparked by my own doctor showing me one that was available to him now. This software recorded our session, displayed a transcript, and when prompted, stopped recording and generated a summary of our session. This summary was mostly correct, but muddled some details, and in one area the summary mistook a speaker. It seemed that this program was doing direct summarizing, maybe fine tuned for psychotherapy session transcripts, and might not even be doing speaker diarisation. I thought assuming that was true, there must be a better way that leverages not just speaker diarisation but the medium of psychotherapy itself, creating an intermediate diagnostic layer that points out medically important considerations (recognizing someone is depressed, manic, noting problematic relationships/behaviors, noting medication effectiveness with regard to patient's medical history, etc.) and attends to token spans of the transcript pertaining to entity-tagged diagnostically important information (symptoms, medications, cognition, emotions, behaviors, social factors, etc.), attending to the full patient history, transcript (multimodal? voice tone?), and retrieving entity-tagged articles from a diverse medical corpus containing not only articles about medications, conditions, etc. but also therapist training information with guidelines of action in aspects like dealing with emotional states, relationships, medication, etc.. Another layer would then attend to the text area (and entity tokens within), from the top to the bottom of the transcript (theoretically mostly), that was relevant for each diagnostic "note" (probably unstructured). After the medically relevant insights are generated, both the original transcript and medical notes pertaining to areas of the transcript would be used to generate a session summary, recommendations of information to add to patient history which the doctor can either accept or reject, and actionable recommendations for the doctor. All of these would be editable by the doctor (summary being regenerated for changes to diagnostic notes), and used to improve future suggestions. Although there is a blaring issue to my practical approach, I don't have the approvals, resources, licenses, lawyers, etc., to do official data collection or model training at the scale required to develop a good implementation of the proposed model, but what I can do now is work on the core transcript analysis, tagging, and information retrieval approach.\
\
I propose utilizing MentalBERT, trained on a general mental health corpus, and fine tuning utilizing selective masking as described [here](https://repositum.tuwien.at/handle/20.500.12708/198293), boosting BERTs ability to recognize clinically relevant indicators from complex context surrounding these concepts by masking words pertinent to mental health, to entity-tag words/sequences of words in the session transcript and patient history that pertain to psychologically relevant information (conditions, medications, behaviors, people/relationships, etc.), and use non-patient entities to retrieve diagnostically relevant documents.\
\
In the future, another language model would sit above this entity-tagged information, with retrieved documents, and produce the sequence of diagnostic notes pertaining to areas of the transcript. On top of both the entity-tagged transcript and diagnostic notes (possibly with "cited" relevant passages of documents instead of the entire document [cherry picking?]) a summarization model would produce the final session summary along with another model for proposed additions to patient history and therapist action items. These last few tasks could be handled through prompt engineering and API calls to GPT-4 (mainly the 4o-mini model), although fine tuning a simpler model would be preferred (if I had the notoriously difficult to obtain data to train on). Prompting models like these also allows us to incorperate clinitian edits of generations in prompt context. Using API calls to generative models would theoretically eliminate the need for expensive model development and training, but risk being lower quality (as well as difficult to HIPAA certify), possibly not good enough for a mature clinical software suite, but likely still better then boiler plate text summarization while significantly lowering the barrier to implement.

Papers: \
Detecting Depression and Anxiety on Social Media Using Selective Masking (2024, [TUWien](https://repositum.tuwien.at/handle/20.500.12708/198293))\
Task-Specific Transformer-Based Language Models in Health Care: Scoping Review (2024, [JMIR](https://medinform.jmir.org/2024/1/e49724/))\
Mental Illness Detection Using NLP (2024, [CSUN](https://scholarworks.calstate.edu/downloads/ms35th72p))
