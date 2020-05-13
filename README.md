# POINTREC: A Test Collection for Point of Interest Recommendation

POINTREC is a test collection for point of interest (POI) recommendation, comprising of (i) a set of information needs, (ii) a dataset of POIs, and (iii) graded relevance assessments for information need and POI pairs. Additionally, we include recommendations by multiple variants of a simple baseline method.

### Information needs

The [infoneeds.json](infoneeds.json) file contains a set of 112 information needs, which were manually collected and enriched with metadata from Yahoo! Answers and Reddit.


### POI dataset

The [poi_dataset/](poi_dataset/) folder contains the following: TODO


### Relevance assessments

The [relevance/assessments.tsv](relevance/assessments.tsv) file contains the raw relevance assessments collected via crowdsourcing.  For each information need-POI pair (columns 1 and 2), column 3 contains a space-separated list of relevance ratings that were given by workers.  There are at least 3 ratings for each pair.

For each information need-POI pair, the relevance ratings are consolidated into a single ground truth label.  This consolidation is performed by the [relevance/create_qrels.py](relevance/create_qrels.py) script.  The resulting ground truth file, in TREC qrels format, is [relevance/qrels.trec](relevance/qrels.trec).


### Baselines

Recommendations are generated by three variants of a simple content-based recommender.  These can be found under [baselines/](baselines/) in TREC runfile format.  The table below shows their performance using graded (NDCG@5 and NDCG@10) and binary (MRR, MAP) metrics.  Specifically, we use the [trec_eval](https://github.com/usnistgov/trec_eval) tool for evaluation using the following settings.  (Note the use of the `-c` flag, as the baselines may not return any results for some of the information needs.)

For graded relevance:

```
trec_eval -c -m ndcg_cut relevance/qrels.trec baselines/baselineX.trec
```

For binary relevance (only the highest relevance level 3 is accepted as relevant):

```
trec_eval -c -l3 relevance/qrels.trec baselines/baselineX.trec
```

| Method | NDCG@5 | NDCG@10 | MRR | MAP |
| -- | -- | -- | -- | -- |
| Baseline 1 | 0.6389 | 0.5812 | 0.5812 | 0.3304 |
| Baseline 2 | 0.4109 | 0.3979 | 0.2814 | 0.0667 |
| Baseline 3 | 0.6784 | 0.6573 | 0.5535 | 0.2506 |
