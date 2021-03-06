# Perform Foundational Data, ML, and AI Tasks in Google Cloud
Big data, machine learning, and artificial intelligence are today’s hot computing topics, but these fields are quite specialized and introductory material is hard to come by. Fortunately, Google Cloud provides user-friendly services in these areas and Qwiklabs has you covered with this introductory-level quest, so you can take your first steps with tools like Big Query, Cloud Speech API, and AI Platform. Complete this quest, including the challenge lab at the end, to receive an exclusive Google Cloud digital badge.


<div align="center"> 
  
   [![alt text](imagen/GSP323.png "GSP323.png")](https://google.qwiklabs.com/focuses/11044?parent=catalog)
</div>


[QUEST LINK](https://google.qwiklabs.com/quests/117)



If you are getting help from our channel, we request you to subscribe to [Eisen Picon](https://www.youtube.com/channel/UCXvWiFZ7h89FQx0nI-LfaGw), 
this is the only way to help us.

# Task 1: Ejecuta un job simple de Dataflow

```
gsutil cp gs://cloud-training/gsp323/lab.csv .

cat lab.csv

gsutil cp gs://cloud-training/gsp323/lab.schema .

cat lab.schema
```

# Task 4: AI
```
gcloud iam service-accounts create my-natlang-sa --display-name "my natural language service account"
```
---
```
gcloud iam service-accounts keys create ~/key.json --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com
```
---
```
export GOOGLE_APPLICATION_CREDENTIALS="/home/$USER/key.json"
```
--- 
```
gcloud auth activate-service-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com --key-file=$GOOGLE_APPLICATION_CREDENTIALS
```
## Utilice Cloud Natural Language API para analizar la oracion
```
gcloud ml language analyze-entities --content="Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat." > result.json
```
---
```
gcloud auth login 
```
### Copy the token from the link provided  

Cargue el archivo resultante a Cloud Storage con el siguiente comando: 

```
gsutil cp result.json gs://YOUR_PROJECT-marking/task4-cnl.result
```

## Utilice Google Cloud Speech API para analizar el archivo de audio

```

nano request.json
```

```json
{
  "config": {
      "encoding":"FLAC",
      "languageCode": "en-US"
  },
  "audio": {
      "uri":"gs://cloud-training/gsp323/task4.flac"
  }
}
```
---
```

curl -s -X POST -H "Content-Type: application/json" --data-binary @request.json \
"https://speech.googleapis.com/v1/speech:recognize?key=${API_KEY}" > result.json
```
---
```
gsutil cp result.json gs://YOUR_PROJECT-marking/task4-gcs.result
```
---

```
gcloud iam service-accounts create quickstart

gcloud iam service-accounts keys create key.json --iam-account quickstart@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com

gcloud auth activate-service-account --key-file key.json

export ACCESS_TOKEN=$(gcloud auth print-access-token)
```
---

### Utilice Google Video Intelligence y detecte todo el texto del video

```
nano request.json
```
---
```json
{
   "inputUri":"gs://spls/gsp154/video/train.mp4",
   "features": [
       "TEXT_DETECTION"
   ]
}
```

---

```
curl -s -H 'Content-Type: application/json' -H "Authorization: Bearer $ACCESS_TOKEN" 'https://videointelligence.googleapis.com/v1/videos:annotate' -d @request.json
```
---
```
curl -s -H 'Content-Type: application/json' -H "Authorization: Bearer $ACCESS_TOKEN" 'https://videointelligence.googleapis.com/v1/operations/OPERATION_FROM_PREVIOUS_REQUEST' > result1.json
```
---
```
gsutil cp result1.json gs://YOUR_PROJECT-marking/task4-gvi.result
```

## Congratulations! Done with the challenge lab

You completed the lab **Perform Foundational Data, ML, and AI**

<div align="center"> 
  
   [![alt text](imagen/Perform-Foundational-Data-ML-AI.png "Perform Foundational Data, ML, and AI")](https://google.qwiklabs.com/public_profiles/3a451349-23c9-4a64-8464-c164280214a0/badges/579348 )
</div>
