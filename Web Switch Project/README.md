# Web Switch
<div align="center">
  <br>
  <a href="https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Faws.amazon.com%2Fmarketplace%2Fmanagement%2Fsignin%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Faws-mp-seller-management-portal&forceMobileApp=0&code_challenge=aob9N8uqf0Ig-0kp2wj_HVSqGtE6HKHFv23ub_2Cqaw&code_challenge_method=SHA-256">
  <img height="100em" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/512px-Amazon_Web_Services_Logo.png"></img>
</a>
</div>
<br>
<br>
Step by Step to buildling an AWS Archtecture to switch a relay from website.

## Let's put our hands-on in Amazon Web Server!

### Login in AWS Account

We will need to login in our AWS Account to make all this happen! So, <a href="https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Faws.amazon.com%2Fmarketplace%2Fmanagement%2Fsignin%3Fstate%3DhashArgs%2523%26isauthcode%3Dtrue&client_id=arn%3Aaws%3Aiam%3A%3A015428540659%3Auser%2Faws-mp-seller-management-portal&forceMobileApp=0&code_challenge=aob9N8uqf0Ig-0kp2wj_HVSqGtE6HKHFv23ub_2Cqaw&code_challenge_method=SHA-256">click here</a> to sign in.

#### Creating Lambda Functions
In console of AWS, type Lambda and click in button to open the space to create our Lambda Functions.
Now, we are starting our project! We will create two Lambda Functions. The first will be responsable to <b>Check</b> if our switch are <i>ON</i> or <i>OFF</i>.
So take a note of the both Lambda Functions Names, it will be important later.

### For the first Lambda
<ul>
    <li>In console, click in "Create Function" button.</li>
    <li>Select Author from scratch</li>
    <li>Type your first Lambda Function Name to check the Switch State (save this name)</li>
    <li>In Runtime, select Python 3.8</li>
    <li>if Architecture option appear for you, select "x86_64"</li>
    <li>Click in "Create Function"</li>
</ul>

Well done! Now we need to upload the .zip code downloaded
<ul>
    <li>
    Inside our first Lambda, click in Upload from>.zip File>upload</li>
    Select the .zip file, inside the Shadow Status Check folder</li>
    Click in Save</li>
</ul>

Now let's attach policy that will permite the communication between our Lambda and IoT Core (Service that we will configurate later)
<ul>
    <li> Still inside Lambda Function select: Configuration>Permission and click in Role Name link</li>
    <li>IAM will open so: Permission>Attach Policies</li>
    <li>Search for: AWSIoTDataAccess>select>Attach Policy</li>
</ul>

### For the second Lambda
<ul>
    <li>In console, search for Lambda>Create Lambda</li>
    <li>Select Author from scratch</li>
    <li>Type your second Lambda Function Name to update the Switch State (save this name)</li>
    <li>In Runtime, select Python 3.8</li>
    <li>if Architecture option appear for you, select "x86_64"</li>
    <li>Click in "Create Function"</li>
</ul>

Well done! Now we need to upload the .zip code downloaded
<ul>
    <li>Inside our second Lambda, click in Upload from>.zip File>upload</li>
    <li>Select the .zip file, inside the Shadow Status Update folder</li>
    <li>Click in Save</li>
</ul>

Now let's attach policy that will permite the communication between our Lambda and IoT Core (Service that we will configurate later)
<ul>
    <li>Still inside Lambda Function select: Configuration>Permission and click in Role Name link</li>
    <li>IAM will open so: Permission>Attach Policies</li>
    <li>Search for: AWSIoTDataAccess>select>Attach Policy</li>
</ul>

### Launching our stack

Click in button Below<br>
[![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite)

Select: <i>Template is ready>Upload a template file>select .yml file downloaded>next</i>
Now:
<ul>
  <li>Type any stack name</li>
  <li>Insert your first Lambda Function Created</li>
  <li>Insert your second Lambda Function Created</li>
  <li>Type your ThingName (Capital letters and special carachteres, are not allowed)</li>
  <li>Select "REGIONAL", in apiRegion</li>
  <li>Next</li>
  <li>Scroll the website to the end and press Next button</li>
  <li>Scroll the website to the end and select <i><b>I acknowledge that AWS CloudFormation might create IAM resources with custom names</b></i></li>
  <li>Create Stack</i>
</ul>
At this time, wait the stack name be with status: "CREATE_COMPLETE", to check this out, just press the reload button inside AWS
Congratulations!!

### Uploading WebSite
Before we Update the html to our bucket, we need to configure the URL to be invoked when requisited.<br>
Open <b><i>API Gateway>API_{ThingName}>Stage>Click in arrow to show options>Click in Get Method and copy the URL.</i></b><br>
<ul>
  <li>Open <b>iot_lamp.txt</b></li>
    <ul>
      <li>There are three lines inside that you need to paste the URL copied inside single quotes</li>
    </ul>
  <li> save as iot_lamp.html</li>
  <li>In AWS Console Type: S3 > Search by your thingname> upload> Select iot_lamp.html>upload</li>
</ul>

<i>Go to API Gateway>API_{ThingName}>Resource>shadow-state>GET>Integration Request>LambdaFunction>Edit(click in pencil)>Select your lambda check>OK</i> 
## Configuring ESP and AWS IoT Core
### Editing AWS IoT Shadow 
In this session, we will configure the AWS Shadow State (To check and update the shadow of our object) at AWS IoT Core to permite the connection and communication between AWS and our device
At first, let's search in AWS Console, IoT Core.
So with IoT Core Open: <b><i>Manage>Things>Select your ThingName created with Stack earlier</i></b>
Navigate in tabs at <b><i>Device Shadow</i></b>
Now:
<ul>
  <li><i>Create Shadow>Unnamed (classic) Shadow>Edit</i></li>
  <li>Copy the code below and replace all in the code area</li>
  <b>{ "state": { "desired": { "status": "off" }, "reported": { "status": "off" } } } </b>
  <li>Update</li>
</ul>

### Finally, let's generate our certificate and attach policy to our thing
Returning to our Thing open, click in: Certificates>Create Certificate<br>
Now:
<ul>
  <li>At Device Certificate: Active Certificate>Download (save the certificate)</li> 
  <li>At Public Key: Download (don't need to save)</li> 
  <li>At Private key: Download (save the certificate)</li> 
  <li>Done</li> 
  <li>Click in the certificate created>Policies>Attach Policies>Policy_{ThingName}</li>
</ul>


### Configuring ESP32

Finally, let's configure the device.
Open the folder "iot_switch_esp_code">iot_switch_esp_code.ino<br>
<b>At iot_switch_esp_code.ino file</b>
<ul>
  There are two lines that we will need to modificate as follow
  The first line, change the ThingName to created: #define AWS_IOT_PUBLISH_TOPIC   "$aws/things/<b><i>THINGNAME</i></b>/shadow/update"
  The second line, change the ThingName to created: #define AWS_IOT_SUBSCRIBE_TOPIC   "$aws/things/<b><i>THINGNAME</i></b>/shadow/update/delta"
</ul>
<b>At secrets.h file</b>
<ul>
  <li>Change the ThingName to created: #define THINGNAME <b><i>"THINGNAME"</i></b></li>
  <li>You’d have to replace the values of <WIFI NAME>, AWSEnDPOINT (your AWS IoT Host Endpoint), and <WIFI PASSWORD> depending on your setup</li>
    <ul>
      <li>To find your AWSENDPOINT: IoT Core>Settings(in the end of left Menu)>Endpoint</li>
    </ul>
</ul>

<ul>
  <b>Now let's replace the certificates that we downloaded earlier</b>
  <li>At AWS_CERT_CRT[], replace the certificate.perm</li>
  <li>At AWS_CERT_PRIVATE[], replace the certificate.perm</li>
</ul>
    
## Writing the Code to our Device
Plug your ESP32 in Desktop/Notebook
In the left upside, click in right arrow. Wait the written and when the console show "Connecting....___" Press the right button at ESP named: boot, until the code start flash. Wait 1 minute and well done!<br>
You also can see if connected if you open: IoT Core>Manage>Things>Select your thing>Activity>Connect your ESP in Desktop/PC<br>
Now you will se your ESP connecting to AWS :)
 
    
## Let's test
Open <b><i>API Gateway>API_{ThingName}>Stage>Click in link
Now, type your ThingName>Check>Press to Turn Off/On
