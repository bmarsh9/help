## Flask

## Docker

##### Docker daemon in WSL
```
sudo dockerd &
```

## Git

##### Common
```
git pull
git checkout -b new-branch
git add . 
git commit -m "my changes"
git push origin new-branch
```

##### Undo commit
```
git commit -m "Something terribly misguided" # (0: Your Accident)
git reset HEAD~                              # (1)
[ edit files as necessary ]                    # (2)
git add .                                    # (3)
git commit -c ORIG_HEAD                      # (4)
```

## K8

## Terraform

##### Tfswitch
```
https://tfswitch.warrensbox.com/Install/
```

## VirtualEnv
```
python3 -m venv venv
source venv/bin/activate
```

## Gcloud

##### Cheat sheet
```
https://gist.github.com/bmarsh9/3a54ba90100d20529c9567b450af66ec
```
##### Common commands
```
gcloud auth application-default login

gcloud config list
gcloud auth list
gcloud config set project $MY_PROJECT_ID

gcloud projects list
gcloud organizations list

#switch project based on the name
gcloud config set project $(gcloud projects list --filter='name:wordpress-dev' --format='value(project_id)')
```

##### Tunneling
```
gcloud compute start-iap-tunnel test-vdi 3389 --local-host-port=localhost:5000 --zone us-west1-b
```

##### SSH
```
gcloud compute ssh --zone "us-west1-b" "sonarqube" --project "security-project-console"
```

##### Tunneling via SSH
```
gcloud compute ssh --zone "us-west1-b" "sonarqube" --project "security-project-console" -- -NL 8081:localhost:9000
```

## Cloud Naming
```
https://stepan.wtf/cloud-naming-convention/
```



