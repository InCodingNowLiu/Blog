title: rasa config
author: incodingnowliu
date: 2018-06-02 20:06:28
tags:
---
# rasa config

```bash
python -m rasa_nlu.server -c sample_configs/config_spacy.json
```

```bash
python -m rasa_nlu.server -c sample_configs/config_ava_20171201.json &
```

```bash
curl -X POST localhost:5000/parse -d '{"q":"I am looking for Mexican food"}' | python -m json.tool
```

```bash
nohup python -m rasa_nlu.server -c sample_configs/config_ava_20171206.json
```