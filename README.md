# Crowd Deliberation

-

This is the official repository of the Crowd Deliberation data set. There are three different files with relevant data:

* [**data.csv**](data.csv) which lists all 80 texts that were analyzed in the study: 40 from the Sarcasm data set, and 40 from the Relation data set.
* [**labels.csv**](labels.csv) which lists all labels collected from crowd workers for the 80 texts listed in data.csv.
* [**deliberations.csv**](deliberations.csv) which lists all group deliberations that were done on individual cases. Each group deliberation has 3 members who may or may not have been active in each of the Justify and Reconsider sessions.

### Columns in data.csv

-

* **DATASET**: the identifier of the data set that text belongs to; either "deliberation-sarcasm" or "deliberation-relation-person-place"
* **DATA\_ID**: the unique numeric ID of that text, used to match entries in labels.csv and deliberations.csv
* **TEXT**: the actual text content for that text
* **GROUND\_TRUTH\_LABEL**: the correct label for that text; only available for the first 25 cases of the "deliberation-relation-person-place" data set.

### Columns in labels.csv

-

* **DATA\_ID**: the numeric ID of the text that label was given for
* **DATASET**: the data set this text belongs to
* **ANNOTATOR\_ID**: the numeric ID of the crowd worker who provided that label
* **LABEL\_ID**: the unique numeric ID of that label, used to match entries in deliberations.csv
* **ORIGINAL\_LABEL**: the actual label provided; one of "sarcastic" / "not\_sarcastic" for the Sarcasm data set, and "relation\_expressed" / "not\_expressed" for the Relation Extraction data set
* **ORIGINAL\_CONFIDENCE**: the confidence for the label provided; one of 0 (Not Sure) / 0.5 (Sure) / 1 (Very Sure)
* **EVIDENCE**: A list of text snippets highlighted as evidence for the provided label in JSON format: [ { "start": 123, "end": 456, "quote": "The highlight text snippet.", "comment": "An optional comment from the annotator." }, { ... }, { ... } ]; annotators were required to highlight at least one text snippet, but they could highlight as many as they wanted.
* **QUESTION\_DO\_YOU\_THINK\_OTHER\_PEOPLE\_MIGHT\_CHOOSE\_A\_DIFFERENT\_ANSWER\_THAN\_YOU\_DID**: One of "I expect most people to agree with me." / "I expect only about half of the people to agree with me." / "I expect most people to disagree with me."
* **QUESTION\_WHY\_DO\_YOU\_THINK\_OTHER\_PEOPLE\_MIGHT\_CHOOSE\_A\_DIFFERENT\_ANSWER**: Annotators were shown a list of six possible reasons and an "Other: \_\_\_\_\_\_" field to provide a free-form text answer; they had to check at least one, but could check multiple of them if they had indicated they expected some disagreement from other people; this column contains the list of all answers checked, including a potential free-form answer in JSON format: [ "The text contains relevant details other people could easily miss.", "This is a case where a person's answer would depend heavily on their personal preferences and taste.", "Other: some other free-form answer." ]
* **QUESTION\_PLEASE\_ELABORATE\_ON\_YOUR\_ANSWER\_TO\_THE\_PREVIOUS\_QUESTION\_EXPLAINING\_WHY\_YOU\_THINK\_OTHER\_PEOPLE\_MIGHT\_CHOOSE\_A\_DIFFERENT\_ANSWER**: Free-form text answer
* **QUESTION\_IF\_THERE\_WERE\_OTHER\_PEOPLE\_WHO\_CHOSE\_A\_DIFFERENT\_ANSWER\_THAN\_YOU\_DID\_DO\_YOU\_THINK\_A\_GROUP\_DISCUSSION\_WOULD\_HELP\_TO\_RESOLVE\_THE\_CASE**: One of "Yes, a group discussion would help to resolve the case." / "No, a group discussion would not help to resolve the case."
* **DELIBERATION\_ID**: the numeric ID of the deliberation this label was discussed in if any. If this label was never part of any group discussion, this field is empty.

### Columns in deliberations.csv

-

* **DELIBERATION\_ID**: The unique numeric ID of that deliberation
* **DATA\_ID**: The numeric ID of the text discussed in that deliberatino 
* **WAS\_RESOLVED**: Whether this case was resolved; one of "True" / "False"
* **NUM\_DISSENTING\_OPINIONS\_DISCUSSED**: The number of dissenting opinions discussed in this deliberation; one of 0, 2, 3
* **NUM\_DISSENTING\_OPINIONS\_RECONSIDERED**: The number of dissenting opinions reconsidered in this deliberation; one of 0, 2, 3
* **NUM\_DISSENTING\_OPINIONS\_DISCUSSED\_AND\_RECONSIDERED**: The number of dissenting opinions discussed AND reconsidered in this deliberation; one of 0, 2, 3
* **NUM\_DISSENTING\_OPINIONS\_DISCUSSED\_RECONSIDERED\_AND\_CONCLUDED**: The number of dissenting opinions discussed, reconsidered AND concluded in this deliberation; one of 0, 2, 3
* **MESSAGES**: The chat history of messages exchanged in this deliberation in JSON format: [ { "user\_id": 123, "user\_pseudonym": "Happy Hippo", "content": "This is my message for the group." }, { ... }, { ... } ]

The following fields starting with **MEMBER\_** exist for all 3 members of the group discussion, starting with **MEMBER\_1\_**, **MEMBER\_2\_**, **MEMBER\_3\_** respectively:

* **MEMBER\_X\_USER\_ID**: The numeric ID of group member X
* **MEMBER\_X\_NAME**: The human-readable pseudonym assigned to group member X
* **MEMBER\_X\_LABEL\_ID**: The numeric ID of group member X's label discussed in this deliberation
* **MEMBER\_X\_ORIGINAL\_LABEL**: Group member X's original label; one of "sarcastic" / "not\_sarcastic" for the Sarcasm data set, and "relation\_expressed" / "not\_expressed" for the Relation Extraction data set
* **MEMBER\_X\_ORIGINAL\_CONFIDENCE**: Group member X's original confidence in her label; one of 0 (Not Sure) / 0.5 (Sure) / 1 (Very Sure)
* **MEMBER\_X\_DID\_DISCUSS**: Whether group member X came back for follow-up session 1 to discuss the case; one of "True" / "False"
* **MEMBER\_X\_DID\_RECONSIDER**: Whether group member X came back for follow-up session 2 to reconsider her position; one of "True" / "False"
* **MEMBER\_X\_RECONSIDERED\_LABEL**: Group member X's reconsidered label; one of "sarcastic" / "not\_sarcastic" for the Sarcasm data set, and "relation\_expressed" / "not\_expressed" for the Relation Extraction data set
* **MEMBER\_X\_RECONSIDERED\_CONFIDENCE**: Group member X's reconsidered confidence in her label; one of 0 (Not Sure) / 0.5 (Sure) / 1 (Very Sure)
* **MEMBER\_X\_QUESTION\_BASED\_ON\_YOUR\_DELIBERATION\_WHY\_DO\_YOU\_THINK\_THE\_OTHER\_PEOPLE\_IN\_THE\_GROUP\_CHOSE\_A\_DIFFERENT\_ANSWER**: Same format as in column QUESTION\_WHY\_DO\_YOU\_THINK\_OTHER\_PEOPLE\_MIGHT\_CHOOSE\_A\_DIFFERENT\_ANSWER for labels.csv to make both answers easily comparable.
* **MEMBER\_X\_QUESTION\_PLEASE\_ELABORATE\_ON\_YOUR\_ANSWER\_TO\_THE\_PREVIOUS\_QUESTION\_FOR\_EXAMPLE\_IF\_YOU\_CHANGED\_YOUR\_MIND\_ABOUT\_THE\_SOURCE\_OF\_DISAGREEMENT\_PLEASE\_EXPLAIN\_WHY**: Free-form text answer
* **MEMBER\_X\_DID\_CONCLUDE**: Whether group member X came back for follow-up session 3 to conclude the case and give their assessment on why the case could be/could not be resolved; one of "True" / "False"
* **MEMBER\_X\_QUESTION\_WHY\_DO\_YOU\_THINK\_THIS\_CASE\_COULD\_BE\_RESOLVED**: Free-form text answer
* **MEMBER\_X\_QUESTION\_WHY\_DO\_YOU\_THINK\_THIS\_CASE\_COULD\_NOT\_BE\_FULLY\_RESOLVED**: Free-form text answer
* **MEMBER\_X\_QUESTION\_DID\_SOMEBODY\_MAKE\_YOU\_DOUBT\_YOUR\_ORIGINAL\_ANSWER\_WHY\_OR\_WHY\_NOT**: A text string starting with "Yes" / "No" followed with an explanation.
* **MEMBER\_X\_QUESTION\_DID\_SOMEBODY\_MAKE\_YOU\_CHANGE\_YOUR\_ORIGINAL\_ANSWER\_WHY\_OR\_WHY\_NOT**: A text string starting with "Yes" / "No" followed with an explanation.
* **MEMBER\_X\_QUESTION\_DID\_YOU\_MANAGE\_TO\_CONVINCE\_SOMEONE\_TO\_CHANGE\_THEIR\_ANSWER\_OR\_CONFIDENCE\_LEVEL\_WHY\_DO\_YOU\_THINK\_YOU\_WERE\_ABLEUNABLE\_TO\_CONVINCE\_THEM**: A text string starting with "Yes" / "No" followed with an explanation.
* **MEMBER\_X\_QUESTION\_DESCRIBE\_HOW\_YOU\_FEEL\_ABOUT\_THE\_DELIBERATION\_PROCESS**: Free-form text answer
* **MEMBER\_X\_QUESTION\_DESCRIBE\_HOW\_YOU\_FEEL\_ABOUT\_THE\_DELIBERATION\_OUTCOME**: Free-form text answer