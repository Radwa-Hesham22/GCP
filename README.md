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
