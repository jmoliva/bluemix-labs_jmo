## Start a docker container on Bluemix

1. Download and install [docker for Mac or Windows] [docker_beta_url]

1. Download and install the [Containers Plug-in CF IC] [cf_ic_plugin_url]

1. Open Terminal

1. Login to the Private Registry

  ```
  cf ic login
  ```

1. Check that you’re connected

  ```
  cf ic images
  ```

1. Search the image nginx in docker hub
  ```
  docker search nginx
  ```

1. Retrieve the image nginx locally on your laptop
  ```
  docker pull nginx
  ```

1. Run the nginx image
  ```
  docker run -d -p 80:80 --name webserver nginx
  ```

1. Show the running server: [http://localhost:80](http://localhost:80)

1. Retrieve your namespace
  ```
  cf ic namespace
  ```
  
1. Tag image for Bluemix registry
  ```
  docker tag nginx:bluemix registry.eu-gb.bluemix.net/mace/nginx:bluemix
  ```
 
1. Push ​*nginx*​ image to Bluemix Public
  ```
  docker push registry.eu-gb.bluemix.net/mace/nginx:bluemix
  ```

1. Validate the presence of ​*nginx*​ image in Bluemix
  ```
  cf ic images
  ```

1. Create a volume (Optional)
  ```
  cf ic volume create NAME
  ```

1. Retrieve IP address
  ```
  bx ic ip list
  ```

1. Bind this IP address with your container
  ```
  bx ic ip bind IP_ADDRESS Demo1
  ```

1. Containers API is available in [Swagger Container API] [containers_api_url] 
  
  X-Auth-Token     = ```cf oauth-token```
  
  X-Auth-Project-Id= ```cf space <space-name> --guid```

Sample to retrieve a namespace:
curl -X GET -H "X-Auth-Project-Id: xxxx" -H "Accept: application/json" -H "X-Auth-Token: bearer xxxxx" "https://containers-api.eu-gb.bluemix.net/v3/registry/namespaces"
  
[containers_api_url]: http://ccsapi-doc.mybluemix.net
[docker_beta_url]: https://beta.docker.com/
[cf_ic_plugin_url]: https://new-console.ng.bluemix.net/docs/containers/container_cli_cfic.html