# AWS-CDN-Video-Streaming-Service
This project leverages the capabilities of Amazon S3, Amazon CloudFront, and React to build a scalable, efficient, and user-friendly video streaming service. 
The service allows users to viewa variety of streaming content through a web-based interface. 
**Amazon S3** is chosen for its durability, scalability, and ease of access. It's ideal for storing and retrieving any amount of data at any time, from anywhere on the web, making it perfect for a video streaming platform with potentially large, fluctuating traffic and vast amounts of data.
**Amazon CloudFront** is designed to optimize security, performance, and reliability, thanks to its worldwide network of data centers (edge locations). When a user requests content via the service, CloudFront retrieves data from the nearest edge location, ensuring the lowest latency and best possible performance. 
This is crucial for video streaming, which requires fast, uninterrupted data transfer. **React** is known for its efficiency, scalability, and flexibility, making it a popular choice for modern web applications. It allows for fast rendering and a dynamic user experience, essential for a platform where users interact with various content, navigate between different views, and control video playback.

## How they work together
Together, S3 ensures organized, scalable storage; CloudFront guarantees swift, reliable content delivery; and React provides a responsive, intuitive user interface. This synergy creates a streamlined video streaming service that prioritizes performance, scalability, and user engagement.


![CDn drawio](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/07105440-c759-4bf9-ba97-4933b3f75293)




## Creating the S3 Bucket
1. In the AWS console navigate to S3 click create bucket
2. Provide a name for your bucket and choose your region
3. Keep bucket ACLs disabled

<img width="827" alt="Screenshot 2023-10-10 at 8 39 51 PM" src="https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/85735eff-6fd8-4518-9f4a-8fb48e32f924"> 

4. Keep your bucket private by leaving the block all public access setting checked (we want users to securely access the bucket via CloudFront)
  
![Screenshot 2023-10-10 at 8 40 10 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/d797784e-77b7-4125-924d-ab695b9b42fb)

  
5. Enable bucket versioning and server-side encryption with Amazon S3-managed keys (SSE-S3)

 ![ ](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/52a91c7f-d849-44b7-93d9-cb482b95dcea)

6. Click create bucket

![Screenshot 2023-10-10 at 8 41 59 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/db01b66d-f890-452b-8f62-3a41e6237893)



## Create the CloudFront Distribution 
1. Navigate to the CloudFront service
2. Before making a CloudFront distribution, we must create an origin access control (OAC) setting under the security tab on the left hand side
3. Give the OAC a name like "videostreamingOAC" and leave the option sign in requests under settings enabled, create the OAC

![Screenshot 2023-10-10 at 8 44 18 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/196f429a-0f4f-443a-96ae-2dd63c0824a9)

4. Return to the distributions tab in CloudFront, click "create a distribution"
5. Choose the S3 bucket as your origin domain

![Screenshot 2023-10-10 at 8 44 37 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/f4d29b50-a7d6-4648-b2dd-6f32cfa6498a)

6. Select the origin access control setting under origin access, then select the OAC you created before (there will be warning to update the S3 bucket policy that will be done soon) 

![Screenshot 2023-10-10 at 8 45 11 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/db3f8690-f26f-4c4f-b44b-184d1ae01eaf)

7. Under Viewer check the Redirect HTTP to HTTPS to enable encryption in transit to secure viewer's connections secured
8. Click create distribution and wait for it to finish deploying in the meantime, update the bucket polict to get the OAC to work
9. Above will be a blue warning saying the S3 bucket policy needs to be updated, all you have to do is click copy policy and you will be redirected to S3
10. Under the S3 bucket policy paste the copied policy, then click save

![Screenshot 2023-10-10 at 8 47 38 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/126baf4b-f3db-4801-a0c0-7272a7ff8749)

## Upload your video to S3 
1. Once distribution status is enabled Return to your S3 bucket
2. Click objects, then upload your video either by dragging the file into the console or by clicking add files and selecting the video

![Screenshot 2023-10-10 at 8 52 03 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/3250ee90-c3fc-45fc-8980-00551dfcff49)


3. Once the file has been added make sure to click upload, it won't upload automatically you will see it loading once you do so

![Screenshot 2023-10-10 at 8 52 27 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/8e1fe6b4-2ba2-445b-8046-1cb7345bae0c)

## Test the video using S3 and CloudFront 
1. Copy the domain name or your CloudFront URL

![Screenshot 2023-10-10 at 9 04 37 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/823f42a8-6e17-41c1-845e-062483371d5c)

2. Paste it in a new tab and then return to S3
3. Go to the S3 bucket and copy the object key and then paste it after the cloudfront domain name (separate the domain name and object key with a "/")

![Screenshot 2023-10-10 at 9 03 13 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/a8724483-78ae-4677-8ef0-6872463a6e62)

4. Click enter and the video should appear in a new tab:

![Screenshot 2023-10-10 at 9 04 10 PM (2)](https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/77e7d369-85b4-4301-bbe3-788a15705bb8)

## Build the Frontend using VSCode and React 
1. Go to your terminal and use the npx command to create it

<img width="615" alt="Screenshot 2023-10-10 at 7 43 32 PM" src="https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/599d1202-ee5a-4e80-82e6-755f90592065">

2. The app should look like this after it has finished installing

<img width="1338" alt="Screenshot 2023-10-10 at 7 59 12 PM" src="https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/bf149cfe-6a39-44ea-8ae5-d4fd971b5457">

3. After the app has been created it is time to tailor it to your personal website: 


https://github.com/Shereefo/AWS-CDN-Video-Streaming-Service/assets/137960467/921ad2e3-b8b3-4860-9d66-eb80b2aacc63









