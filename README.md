<<<<<<< HEAD
# DevOps Challenge Demo Code:

This application will be used as a demo for DevOps Challenges.

You should fork/clone this repository to use as a basis for the challenge.

## Demo application

### Requirements

#### System

- GNU/Linux
- `python` >= 3.7
- `pip` >= 9.0
- `redis` >= 5.0

`>=` means any version of the package, above or equal to the specified version.

#### Application

- `redis-py`
- `tornado`

You can find them in the `requirements.txt` file and their required version number.
You can install them by using:

```bash
pip install -r requirements.txt
```

### :rocket: Starting the Application

The application uses several environment variables.
You can find them all and their default values in the `.env` file. They need to be avaiable at runtime. Here is an overview about the environment variables:

- `ENVIRONMENT` the environment in which the application is run. Likely `PROD` for production or `DEV` for development context.
- `HOST` the hostname on which the application is running. Locally it is `localhost`.
- `PORT` is the port on which the application is running.
- `REDIS_HOST` is the hostname on which redis is running. Locally it is `localhost`.
- `REDIS_PORT` is the port on which to communicate with redis. Normally it is `6379`.
- `REDIS_DB` which redis db should be used. Normally it is `0`.

Application can be found in `hello.py` file. You can start the application by using:

```bash
export $(cat .env | xargs) && python hello.py
```

Although you don't have to export the environment variables that way. :wink:

### Static files

- Static files are located in `static/` folder.
- Templates are located in `template/` folder.

### Executing Tests

Tests can be found in `tests/test.py` file.
You can run the tests by using:

```bash
python tests/test.py
```

## License

Copyright (c) 2019 by the Tradebyte Software GmbH.<br/>
`DevOps-Challenge` is free software, and may be redistributed under the terms specified in the [LICENSE] file.

[license]: /LICENSE

=======
# Objective 

![WhatsApp Image 2023-02-15 at 6 48 13 PM](https://user-images.githubusercontent.com/118529639/220353228-f1251401-e2e7-4792-96f6-0e54059887e7.jpeg)

## Steps:
1- Build the infrastructure on GCP
```
git clone https://github.com/Radwa-Hesham22/GCP-Project.git
terraform init 
terraform plan
terraform apply 
```
- Vpc created

![1](https://user-images.githubusercontent.com/118529639/220355607-09c28247-61e0-4f2e-926e-0dc7c3cb75bc.PNG)

-  2 Subnets created (managed and restricted )

![2](https://user-images.githubusercontent.com/118529639/220356132-ae6f6e8f-67da-43e0-a636-1e22c78e8ad5.PNG)

- Private vm created in managed subnet 

![5](https://user-images.githubusercontent.com/118529639/220356517-dd9863cf-6a09-425f-86ab-074785cb9550.PNG)

- Firewall rule that allows ssh to private vm

![3](https://user-images.githubusercontent.com/118529639/220356629-bb0f27cc-ec23-4cb9-a88a-a1d9de96a83f.PNG)

- Nat gateway in managed subnet

![4](https://user-images.githubusercontent.com/118529639/220356955-8093a727-8557-4a67-a8c5-1ac671135dad.PNG)

- Service account created

![9](https://user-images.githubusercontent.com/118529639/220357175-cf5471e0-9959-458e-a826-7332eff6763e.PNG)

- GKE cluster created in restricted subnet

![6](https://user-images.githubusercontent.com/118529639/220357523-26333147-4731-47c5-958a-f8cf7bf0fd77.PNG)

![7](https://user-images.githubusercontent.com/118529639/220358184-80f3845d-4fb9-4da1-af71-02aea6d7f462.PNG)

2- Build the docker image and push it to GCR

```
docker build -t python_app .
docker tag python_app gcr.io/quick-asset-377911/python_app
docker push gcr.io/quick-asset-377911/python_app
docker pull redis
docker tag redis gcr.io/quick-asset-377911/redis
```

![8](https://user-images.githubusercontent.com/118529639/220361051-dc1647fa-c22e-4680-8aba-f6e51ab45064.PNG)

3- ssh to the private vm 
```
gcloud compute ssh --zone "asia-east1-b" "private-vm"  --tunnel-through-iap --project "quick-asset-377911"
```
4- Credentials to control plane
```
gcloud container clusters get-credentials primary --zone asia-east1-b --project quick-asset-377911
```
5- Apply yaml files
```
vim loadbalancer.yaml
kubectl apply -f loadbalancer.yaml
vim deployment.yaml
kubectl apply -f deployment.yaml
```
6- Check it on your browser

![final](https://user-images.githubusercontent.com/118529639/220362636-a19f92fa-48e5-4fbc-a8a2-666b58853247.PNG)
>>>>>>> e43fd255e6c2eae30e81c149134f92cd8ce9783a
