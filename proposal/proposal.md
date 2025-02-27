# CoNLL 2017 Shared Task Proposal: UD End-to-End parsing

[Call for proposals](http://www.conll.org/cfprop-sharedtask-2017)

For clarity, feasibility and encouragement of participants,
we propose only a small number of tracks and evaluation metrics
(even if there are many possibilities).


## Proposed Tracks


### Main Track

The main track is end-to-end parsing of UD corpora,
i.e., parsing from plain texts to dependency trees.

Most of the UD 1.4 corpora will be used as training/development/testing
data for this track (with some exceptions -- Japanese because of the license,
very small corpora and corpora which cannot be reliably detokenized).
Note that this means that in the track the testing data **will be known in
advance** and we have to trust the participants not to take advantage of it.

As majority of UD corpora do not contain the original plain text, we will
reconstruct it using unannotated raw texts.

Only systems working for **all the languages** will be accepted (we are
interested only in multi-lingual systems).

The participants will be allowed to use these data during training:

- UD 1.4 corpora with plain texts (either gold standard or automatically generated)
    - Automatically tokenized and POS-tagged variants will be provided
- Additional raw texts for the languages involved (probably as much as we can provide)
- Europarl Parallel corpus

No additional data can be used during training. (Note that we do *not* propose
an additional Open track which would allow utilization of additional data and/or
software.)

A participating system will be evaluated on every corpora using the evaluation
metric(s) below, and the final score of the system will be the arithmetic
mean of the corpora scores (an analogue of macro-accuracy).


### Parallel Data Track [if we have the required data]

Very similar to the Main track (same training data, additional resources
and evaluation), with the following differences:

- The testing data would be previously unreleased parallel corpora in a subset
  of languages from the Main track. During evaluation, the system will get all the
  data at the same time (to be able to exploit the fact that the testing data are
  parallel corpora).
- Small parallel corpora (either a small part of the corpora discussed above,
  or small part of Europarl, etc.) would be released as development data.

All systems submitted to the Main track would be evaluated in Parallel data
track, so that systems in the Main track are evaluated also on unknown test set,
in addition to known UD testing data.


### Surprise Language Track

Similar to the Main track (same training data, additional resources and
evaluation), with the following differences:

- The testing data will be in previously unreleased languages, unknown to the
  participants until the evaluation. No development data will be provided.


## Evaluation Metrics

We currently propose only one evaluation metrics -- LAS F1-score.
Notably, for a dependency edge to be considered correct:

- the dependent word and the head word must be both correct and tokenized
  correctly (in this respect, all technical roots are equivalent)
- the dependency relation must be correct

We currently do *not* propose to evaluate UAS (we already produce several
dozens of scores in the Main task for each system; and with UAS, we would have
two different orderings of participants in every track).

The evaluation starts by aligning the system-produces tokens to the
gold standard ones. This process is straightforward for
[CoNLL-U tokens](http://universaldependencies.org/format.html#words-and-tokens)
which can be identified by their range in the original plain text;
for [CoNLL-U words](http://universaldependencies.org/format.html#words-and-tokens)
being part of multiword-tokens, we use longest common subsequence to perform the
alignment. We completely ignore sentence breaks during tokenizer evaluation.

### Metric Focused on UD Content Word Dependencies [undecided]

If we come up with a good metric focused on UD content dependencies, we may
either replace the LAS by this metric (or use it in addition to LAS, but beware
or increased complexity).

### Language Variants [undecided]

For some languages, there are multiple corpora in the UD (3 corpora for Czech, English,
Latin; 2 corpora for 8 languages in UD 1.3).

It is yet undecided whether these corpora will be evaluated separately (whereby
contributing multiple times to the final score), or only one corpus for each language
would be kept, or the corpora for a given language will be somehow merged.


## Evaluation Process

We plan to use the [Tira platform](http://www.tira.io/) as suggested in the Call
for proposals.

Therefore, the participants will **submit the systems**, not parsed data,
allowing us _not_ to give the testing data beforehand (only after
the Shared Task is evaluated).
