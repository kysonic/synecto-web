## Devops guide

Hey. Here i gonna describe all steps to spin up new server on GCP. This knowledge will be required when
we will start to develop big environment for app.synecto.io.

## Google cloud platform

### Ubuntu 16 04

1. Spin up environment

    - sudo apt-get install nginx

2. Install certbot4

    - https://certbot.eff.org/#ubuntuxenial-nginx
    - run sudo certbot --nginx


Deploy

gcloud auth login (login as Elena)
npm run build
export CLOUDSDK_CORE_PROJECT=tenacious-works-175319
gcloud compute scp ~/WebDevelopments/CDC/designmap-spa-v3/build/unbundled/* app-synecto:~/synecto --zone us-east1-c --recurse