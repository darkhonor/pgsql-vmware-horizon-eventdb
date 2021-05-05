# PostgreSQL Pod to support VMware Horizon Events DB

## Description

Starting with Horizon 2103, PostgreSQL is now a **supported** Database to host the Horizon Events Database.  These manifests will do the following:

+ Create several environment variables to configure the PostgreSQL instance and database
+ Create a Kubernetes Secret to store the database user password
+ Create an NFS Persistent Volume and associated Persistent Volume Claim
+ Create a Service to expose port 5432/tcp to the HomeLab network
+ Deploy a single pod instance of PostgreSQL

The deployment manifest uses the "Latest" tag for the Docker image, which at this time is 13.2.  No, the Base64-encoded string listed as the database user password is not the password I use (unless I am the most unluckiest person in the world to choose the wrong x letters to change to create a collision).  You will need to modify to use your own base64-encoded string or manually create on the master node by typing:

    kubectl create secret generic pgsql-horizon-secret --from-literal=password=<Your actual password here>

The order of applying the manifests only matters as long as `pgsql-deploy.yaml` is the last to be applied.