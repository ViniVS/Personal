For the second Lambda

    In console, search for Lambda>Create Lambda
    Select Author from scratch
    Type your second Lambda Function Name to update the Switch State (save this name)
    In Runtime, select Python 3.8
    if Architecture option appear for you, select "x86_64"
    Click in "Create Function"

Well done! Now we need to upload the .zip code downloaded

    Inside our second Lambda, click in Upload from>.zip File>upload
    Select the .zip file, inside the Shadow Status Update folder
    Click in Save

Now let's attach policy that will permite the communication between our Lambda and IoT Core (Service that we will configurate later)

    Still inside Lambda Function select: Configuration>Permission and click in Role Name link
    IAM will open so: Permission>Attach Policies
    Search for: AWSIoTDataAccess>select>Attach Policy
