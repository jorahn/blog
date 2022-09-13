---
toc: false
layout: post
description: Pre-training and Fine-tuning Transformer Models on Chess Games
categories: [Language,Pretraining,Fine Tuning,BERT]
title: Transformer Chess Engine Pt. 1 
---
Position -> Policy Network -> Move -> Position -> Policy Network
2020 Shawn Presser GPT-2, 2021-22 3x GPT-2 Arxiv
PGN vs FEN, Data Sources & Preprocessing (pgn-extract)
Imitation Learning on Move selection (Winners and Losers)

Fine-tuning BERT-base-cased
Pre-training BERT-base from scratch and Fine-tuning
Pre-training DeBERTaV2-base from scratch and Fine-tuning

Effects of
- Hardware (3060 v T4 v P100 v V100) @ AMP, Batch Size, Speed
- Vocab size
- torch.adamw, bnb.adamw, apex.adamw_fused
- deepspeed & torchdynamo

Fine-tuning DeBERTaV2-base as a Value Network
Self-play RL
