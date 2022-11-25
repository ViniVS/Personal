# For the first Lambda

    In console, click in "Create Function" button.
    Select Author from scratch
    Type your first Lambda Function Name to check the Switch State (save this name)
    In Runtime, select Python 3.8
    if Architecture option appear for you, select "x86_64"
    Click in "Create Function"

Well done! Now we need to upload the .zip code downloaded

    Inside our first Lambda, click in Upload from>.zip File>upload
    Select the .zip file, inside the Shadow Status Check folder
    Click in Save

Now let's attach policy that will permite the communication between our Lambda and IoT Core (Service that we will configurate later)

    Still inside Lambda Function select: Configuration>Permission and click in Role Name link
    IAM will open so: Permission>Attach Policies
    Search for: AWSIoTDataAccess>select>Attach Policy
