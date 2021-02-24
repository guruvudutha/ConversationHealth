# devops infra challenge solution

## Node JS API

1. Update the firebase database url in server.js file.
2. Create a service account for firebase and download the private key json file and place it inside app folder with name service_account.json.
3. Import firebase_import.json into the firebase realtime databse.

## Build and push docker image to GCR

```bash
$ gcloud auth login
$ gcloud auth configure-docker
$ cd app
$ docker build -t gcr.io/<PROJECT_ID>/node-rest-api:latest .
$ docker push gcr.io/<PROJECT_ID>/node-rest-api:latest
```

## Create gcp cloud run and deploy node js api into cloud run using terraform

1. Update project id in terraform/main.tf in provider block and also in the docker image name in google_cloud_run_service resource block.
2.
  ```bash
  $ cd terraform
  $ gcloud auth application-default login
  $ terraform init
  $ terraform apply
  ```
## Test

1. URL of the cloud run app can be obtained from terraform output.
2. To create employee

  ```bash
  $ curl -X POST \
  https://mywebapp-gu2ru4ehuq-uc.a.run.app/api/employees \
  -H 'content-type: application/json' \
  -d '{
  	"name": "emp2",
  	"age": 25,
  	"address": "US",
  	"phone": "+1 8388 765 432"
  }'
  ```

3. To list all employees

  ```bash
  $ curl -X GET \
  https://mywebapp-gu2ru4ehuq-uc.a.run.app/api/employees \
  -H 'content-type: application/json'
  ```

4. To view employee with uid

  ```bash
  $ curl -X GET \
  https://mywebapp-gu2ru4ehuq-uc.a.run.app/api/employees/-MUKsdeKh0xd5eK3FA77
  ```

5. To update employee with uid

  ```bash
  $ curl -X PUT \
  https://mywebapp-gu2ru4ehuq-uc.a.run.app/api/employees/-MUKsdeKh0xd5eK3FA77 \
  -H 'content-type: application/json' \
  -d '{
      "address": "US",
      "age": 26,
      "name": "emp2",
      "phone": "+1 8388 567 432"
  }'
  ```
6. To delete employee with uid

  ```bash
  $ curl -X DELETE \
  https://mywebapp-gu2ru4ehuq-uc.a.run.app/api/employees/-MUKsdeKh0xd5eK3FA77
  ```
