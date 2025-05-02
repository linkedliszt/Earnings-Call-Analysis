# Earnings-Call-Analysis

## Finetuning FinBERT
  - Goal: Finetuning FinBERT to identify confidence levels in management in earnings call transcripts
  - Created own dataset labelled using roBERTa, implemented Bayesian Optimization for hyperparameter tuning, used gradual unfreezing, achieved validation accuracy of 84\%

## MutliModal RAG
  - Goal: Develop a multimodal RAG that retrieves audio and textual earnings call data for sentiment/financial/insights analysis
  - Web-scraped earnings call transcripts using beautiful soup, used regex to extract Q\&A contents
  - Developed multi-modal RAG pipeline that retrieves and analyzes audio features (pitch, root mean squared (RMS) energy and composite intensity) and textual data from earnings call transcripts
  - Incorporated hybrid retrieval system BM25 + FAISS

## Finetuning Embdedding Model (for MuliModal RAG)
  - Goal: Fine-tuning textual embedding model to enhance retreival of MultiModal RAG
  - Web-scraped earnings call transcripts from even earlier years (held-out set) than the ones used for MultiModal RAG using beautiful soup, used regex to extract Q\&A contents
  - Curated query-positive pairs based on these scraped transcripts, by using using GPT-4 to generate a query for every chunk from those transcripts
  - Implemented random, BM25 and cross-encoder negative sampling to obtain hard negatives
  - Fine-tuned using MultipleNegativesRankingLoss which uses in-batch negatives, which greatly increases data usage efficiency
  - Boosted Recall@5 by 25%, Precision@5 by 14.2%, Mean Recriprocal Rank (MRR) by 11.1%
