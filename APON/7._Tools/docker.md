Docker login
https://app.docker.com/ > Account settings > Personal Access Tokens > Read & Write
```
sudo docker login -u hexxedbitheadz
```
Password is the token value
```
sudo apt install docker.io docker-compose
```
Stop all the containers
```
sudo docker stop $(sudo docker ps -a -q)
```
Remove all the containers
```
sudo docker rm $(sudo docker ps -a -q)
```
Delete all images
```
sudo docker rmi $(sudo docker images -a)
```
#### Elasticsearch error
Elasticsearch requires the system setting `vm.max_map_count` to be set to a certain minimum value. You can fix this by setting it to `262144`.
```
echo "vm.max_map_count=262144" | sudo tee -a /etc/sysctl.conf
```