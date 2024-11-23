This is an theoretical investigation (and pilot development strategy) into the application of deep language models in creating psychotherapist assistant software sparked by my own doctor showing me one that was available to him now. This software recorded our session, displayed a transcript, and when prompted, stopped recording and generated a summary of our session. This summary was mostly correct, but muddled some details, and in one area the summary mistook a speaker. It seemed that this program was doing direct summarizing, maybe fine tuned for psychotherapy session transcripts, and might not even be doing speaker diarisation. I thought assuming that was true, there must be a better way that leverages not only speaker diarisation but the medium of psychotherapy itself and creating an intermediate diagnostic layer that points out medically important considerations (recognizing someone is depressed, manic, noting problematic relationships/behaviors, noting medication effectiveness with regard to patient's medical history, etc.) but also attends to token spans of the transcript pertaining to entity-tagged diagnostically important information (symptoms, medications, cognition, emotions, behaviors, social factors, etc.), attending to the full patient history, transcript (voice tone?), and retrieved entity-tagged articles from a medical corpus. Another attention layer would then filter the text area (and entity tokens within), from the top to the bottom of the transcript (theoretically mostly), that was relevant for each diagnostic "note" (structured/unstructured). After the medically relevant insights are generated, both the original transcript and medical notes pertaining to areas of the transcript would be used to generate a session summary, recommendations of information to add to patient history which the doctor can either accept/edit or reject, and actionable recommendations for the doctor. All of these would be editable by the doctor, and used to improve future suggestions. Although there is a blaring issue to my practical approach, I don't have the approvals, resources, licenses, lawyers, etc., to do official data collection or model training at the scale required to develop a good implementation of the proposed model, but what I can do now is work on the core transcript analysis, tagging, and information retrieval approach.\
I propose utilizing MentalBERT (trained on a general mental health corpus) to attend to the transcript and patient history, and entity tag words/sequences of words that pertain to psychologically relevant information (conditions, medications, behaviors, relationships, etc.), and use non-patient entities to retrieve diagnostically relevant documents. In the future, another language model would sit above this entity-tagged information, with retrieved documents, and produce the sequence of diagnostic notes pertaining to areas of the transcript. Then on top of both the entity-tagged transcript and diagnostic notes (possibly with "cited" relevant passages of documents instead of the entire document [cherry picking?]) a summarization model would produce the final session summary along with another model for proposed additions to patient history and therapist action items. Theoretically these last few tasks could be handled through API calls to GPT-4 (mainly the the 4o and 4o-mini models), although fine tuning a simpler model would be preferred (if I had the notoriously difficult to obtain data to train it on).

Papers: \
Detecting Depression and Anxiety on Social Media Using Selective Masking (2024, [link](https://repositum.tuwien.at/handle/20.500.12708/198293))\
Task-Specific Transformer-Based Language Models in Health Care: Scoping Review (2024, [link](https://medinform.jmir.org/2024/1/e49724/))\
Mental Illness Detection Using NLP (2024, [link](https://scholarworks.calstate.edu/downloads/ms35th72p))\
BioALBERT: A Simple and Effective Pre-trained Language Model for Biomedical Named Entity Recognition (2023, [link](https://ieeexplore.ieee.org/document/9533884))
