### Contents
Setting up REST API service on your local machine	1
API Specifications for “Generate Token” API	2
API Specifications for “View Account Details” API	2
API Specifications for “Update Account Details” API	2


Setting up REST API service on your local machine

In-case you wish to practice API scripting using these API’s then you can use below two methods.

Method 1
Step 1 - Download and install hoverfly (LINK)
https://hoverfly.io/

Step 2 – Move the downloaded hoverfly to C drive or any other folder of your choice. In my case I have moved it to this location - C:\hoverfly_bundle_windows_amd64

 

Step 3 – Copy simulation_800_1000_2000.json file to this hoverfly -C:\hoverfly_bundle_windows_amd64

simulation_800_1000_2000.json – You can double click and save this file to your local machine
 

I have also attached this file under resources section in the course. Pls refer to Section 5, lecture 17







Step 4 – Open command line (cmd) and navigate to below directory
C:\hoverfly_bundle_windows_amd64
 


Step 5 – Run below command
hoverctl start --listen-on-host 0.0.0.0 webserver --import simulation_800_1000_2000.json

Pls note : Before running above command from command line, you need to be in C:\hoverfly_bundle_windows_amd64 directory

If the hoverfly has started su successfully then you should see below
 


You can also verify from browser. Type this URL - http://localhost:8500/health
on your browser and you should see “I Am Healthy” message like below
 


Method 2 – For this you need docker installed on your local machine.

1.	Pull the docker image from docker hub and run it on your local machine.

Use below command to run this REST API service on your local machine
docker run -it -p 8888:8888 -p 8500:8500 d752892/rest-api-demo
or
winpty docker run -it -p 8888:8888 -p 8500:8500 d752892/rest-api-demo


$ winpty docker run -it -p 8888:8888 -p 8500:8500 d752892/rest-api-demo
Unable to find image 'd752892/rest-api-demo:latest' locally
latest: Pulling from d752892/rest-api-demo
Digest: sha256:de41ff5c8dfcb0653fa9408150bd5091bce48e5ce5c3accb44a60fc7c386703e
Status: Downloaded newer image for d752892/rest-api-demo:latest
INFO[2020-07-13T07:18:14Z] Default proxy port has been overwritten       port=8500
INFO[2020-07-13T07:18:14Z] Default admin port has been overwritten       port=8888
INFO[2020-07-13T07:18:14Z] Listen on specific interface                  host=0.0.0.0
INFO[2020-07-13T07:18:14Z] Using memory backend
INFO[2020-07-13T07:18:14Z] payloads imported                             failed=0 successful=4 total=4
INFO[2020-07-13T07:18:14Z] Webserver prepared...                         Destination=. Mode=simulate WebserverPort=8500
INFO[2020-07-13T07:18:14Z] current proxy configuration                   destination=. mode=simulate port=8500
INFO[2020-07-13T07:18:14Z] serving proxy
INFO[2020-07-13T07:18:14Z] Admin interface is starting...                AdminPort=8888




API Specifications for “Generate Token” API
Method: POST
Endpoint : http://localhost:8500/generate/token
Mandatory Headers:
Content-Type: application/json
 
Query parameters:
scope : accounts
client_id : username
client_secret: password 
grant_type: client_credentials



API Specifications for “View Account Details” API

Method: GET
Endpoint: http://localhost:8500/account/details/{AccountID}
Mandatory Headers:
Content-Type: application/json
Authorization: valid token


API Specifications for “Update Account Details” API

Method: POST
 
Endpoint :http://localhost:8500/update/account/details
Mandatory Headers:
Content-Type: application/json
Authorization: {token}
 
Request Body
{
	"AccountId": "111",
	"UpdatedBy": "Perf Test Coach",
	"Mobile": "1111111111"
}
 


