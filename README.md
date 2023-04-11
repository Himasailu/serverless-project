# cloud serverless-project
# Developing integrated project using AWS Rekognition 
1. Labels Detection
2. Faces Detection
  3. Faces Comparison
4. Faces Indexing
5. Faces Search
# creating IAM ROLE
![image](https://user-images.githubusercontent.com/96177041/231196136-460350b8-92ed-4e28-9571-6c6dce507c9a.png)
# In the use case section select Lambda function.
![image](https://user-images.githubusercontent.com/96177041/231196654-6205206f-fb42-4729-ad49-963d8e144d94.png)
# Give Role Name.Attach policy permissions
![image](https://user-images.githubusercontent.com/96177041/231196836-41bbd09d-c965-4a95-8511-c661a5e79b5f.png)
![image](https://user-images.githubusercontent.com/96177041/231196882-54fa8df0-cb38-46be-93af-b770813d4500.png)
# Role Successfully created
![image](https://user-images.githubusercontent.com/96177041/231196984-175a777e-ffa3-4b27-bed7-25999748e038.png)
# Creating Bucket.
![image](https://user-images.githubusercontent.com/96177041/231197103-53eab597-91c9-4aef-b7fc-ec9fa45bc57f.png)
Give unique Bucket name
![image](https://user-images.githubusercontent.com/96177041/231197238-4ad55f86-c069-45b3-83f0-979257792f19.png)
# Bucket created successfully
![image](https://user-images.githubusercontent.com/96177041/231197355-e34629e6-125d-465f-83f4-7f6a021c84f6.png)
#upload object into bucket.
![image](https://user-images.githubusercontent.com/96177041/231197455-76177d54-05a7-4ed4-b218-4879ac47e58a.png)
![image](https://user-images.githubusercontent.com/96177041/231197481-30b11863-4717-4124-8f5a-ff212b877bbe.png)
object uploaded successfully.
![image](https://user-images.githubusercontent.com/96177041/231197577-7fd1c835-df22-433a-a881-383bf764e970.png)
# create Lambda Function
![image](https://user-images.githubusercontent.com/96177041/231197668-0bf92365-d0ac-4772-b484-ad530e78458c.png)
select language of code,select existing role and role which we have created in IAM.
![image](https://user-images.githubusercontent.com/96177041/231197890-e3572898-eb04-4887-9f80-736e9913580d.png)
![image](https://user-images.githubusercontent.com/96177041/231197949-41f622c1-9498-4f58-8db2-bd07a3cec63e.png)
import boto3
def lambda_handler(event, context):

    client = boto3.client("rekognition")
    s3 = boto3.client("s3")

    # reading file from s3 bucket and passing it as bytes
    fileObj = s3.get_object(Bucket="bucket-name", Key="obj_scene.jpeg")
    file_content = fileObj["Body"].read()

    # passing bytes data
    response = client.detect_labels(
        Image={"Bytes": file_content}, MaxLabels=3, MinConfidence=70
    )

    # passing s3 bucket object file reference
    response = client.detect_labels(
        Image={"S3Object": {"Bucket": "bucket-name", "Name": "filename"}},
        MaxLabels=3,
        MinConfidence=70,
    )

    print(response)
![image](https://user-images.githubusercontent.com/96177041/231198155-8ee83c21-2fc7-4f2e-8397-bc299e6f9120.png)
# Deploy and Test the code
![image](https://user-images.githubusercontent.com/96177041/231198264-c1078387-fddb-4b8e-b03f-2b221c2e62d2.png)
# Image is successfully rekognised.

