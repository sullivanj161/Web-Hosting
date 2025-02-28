1. Link to tutorial(s) used to setup or your bucket or assist with troubleshooting
I used the YouTube link that was provided in the Pilot announcement to create and use the bucket
to be able to access. https://www.youtube.com/watch?v=-l83oqcaTHg

When watching the video, the first thing I did was create my S3 bucket, this is used as a container 
for storange objects in the AWS server
I named my bucket s3-random-usable-bucket, then I went to the permissions to turn on the static settings 
then added my index.html file and my error 404.html file to store those specific files for use
Then I went to the permissions tab and made my S3 bucket public, which would grant access from outsiders to use the bucket
enabling the buckets public access

then we physically make the objects in our bucket publically available. 
Back into permissions, we enable ACL's which enforce object ownership, making the initial permissions of the
objects restored and publically available.
Then I clicked on my objects in the objects tab and clicked actions and clicked make objects public using ACL

2. Test your index.html by visiting the site URL. Document the URL
![image](https://github.com/user-attachments/assets/1938c133-3d93-4c8b-8b2f-22f1a332c8aa)
https://s3-random-usable-bucket.s3.us-east-1.amazonaws.com/index.html

3.Test the error page by requesting a file / resource that does not exist in your bucket. Document a URL that will resolve to your 404 page
![image](https://github.com/user-attachments/assets/73f0e973-790b-43a5-9067-8167d7c9da0f)
https://s3-random-usable-bucket.s3.us-east-1.amazonaws.com/404.html

4.Research and document the AWS recommended way to associate a Domain name with your S3 bucket
According to an AWS document that I had found, the methodology for using a domain for a static website is as follows
First step is to register a domains, it revolves around finding the domain we wish to use and going from there on how to set up the doman
Next step is to create an S3 bucket, which lets us store and retrieve data form anywhere on the itnernet
in the AWS console, choose create a bucket, enter the name and the name of your domain
You must chose the region that is closest
3. If you wanted to create a subdomain, just repeat step 2
4. setup your root domain bucket for website hosting 
Going to the buckets list, select properties, then you will want to scroll down to static website hositng and enable this
then Use this bucket to host a website, then enable 


(Optional) To provide your own custom error document for 4XX class errors, in Error document, enter the custom error document file name.

If you don't specify a custom error document and an error occurs, Amazon S3 returns a default HTML error document.

(Optional) If you want to specify advanced redirection rules, in Redirection rules, enter XML to describe the rules.
Then save the changes that were made 
Under Static website hosting, note the Endpoint.

The Endpoint is the Amazon S3 website endpoint for your bucket

5. (optional) do the same for the subdomain

6. Upload the index to create website content
First create the index.html file that is wished to be used.
In the buckets list, choose the name of the bucket that you want to enable static website hosting for
Now, in the Amazon console, choose the name of the bucket that you created in the procedure,
Then choose upload, add files, then select your file that you created
Follow other steps if need be to add other files

7. Edit S3 Block Public Access Settings
   For changing permissions for the S3 to allow public access to the added files to the S3 bucket
   First, go to the console
   then go to the name of the bucket that was configured as a static website
   Choose permissions
   Under block public acccess choose edit
   Then ensure if not already that block all public access is clear then saveThis will turn off the settings to create
   a public, static website,

   8. Attach a bucket policy
      Bucket policies will grant public read access to the objects in order for them to be accessible
      Choose your bucket that was created then go to permissions
      Under bucket policy click edit,
      Change the following lines
Copy the following bucket policy and paste it into a text editor. This policy grants everyone on the internet ("Principal":"*") permission to get the files ("Action":["s3:GetObject"]) in the S3 bucket that is associated with your domain name ("arn:aws:s3:::your-domain-name/*").

{
   "Version":"2012-10-17",
   "Statement":[{
      "Sid":"AddPerm",
      "Effect":"Allow",
      "Principal":"*",
      "Action":[
         "s3:GetObject"
      ],
      "Resource":[
         "arn:aws:s3:::your-domain-name/*"
      ]
    }]
}

Update the value for Resource to your-domain-name, for example example.com.

Choose Save changes.
9. Test domain end point
after these steps have been performed, according to the document, you should still have access to the public items
in the S3 storage bucket that are readily available for access.
Choose your bucket
go to propoerties then go to static website hosting and choose your bucket website 
10. Route DNS traffic for your domain to your website bucket
Open the route 53 console at https://console.aws.amazon.com/route53/
then go to hosted zones
choose your domain and then choose create record
    hoose Define simple record.
In Record name, accept the default value, which is the name of your hosted zone and your domain.
 In Record type, choose A ‐ Routes traffic to an IPv4 address and some AWS resources.
In Value/Route traffic to, choose Alias to S3 website endpoint.
Choose the Region.
 Choose the S3 bucket.
The bucket name should match the name that appears in the Name box. In the Choose S3 bucket list, the bucket name appears with the Amazon S3 website endpoint for the Region where the bucket was created, for example, s3-website-us-west-1.amazonaws.com (example.com).
Choose S3 bucket lists a bucket if one of the following is true:
 You configured the bucket as a static website.
The bucket name is the same as the name of the record that you're creating.
The current AWS account created the bucket.
If your bucket does not appear in the Choose S3 bucket list, enter the Amazon S3 website endpoint for the Region where the bucket was created, for example, s3-website-us-west-2.amazonaws.com. For a complete list of Amazon S3 website endpoints, see Amazon S3 Website endpoints. For more information about the alias target, see "values/route traffic to" section in Values specific for simple alias records.
For Evaluate target health, choose No.
Choose Define simple record.

11. Test the website by typing in your domain name and going to the website
https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started-s3.html

5. Research and document the AWS recommended way to enable HTTPS
   In terms of setting up an S3 bucket with HTTPS, it is wise to setup a HTTPS S3 bucket since we
   are transferring data over an HTTP connected protocl, which is unsecure in comparison to HTTPS.
   It could lead to data interception in transit which could create a data breach, man in the middle attacks
   or even eavesdropping attacks. Below is what is required to ensure HTTPS encryption on the S3 bucket
   The S3 bucket requires an access policy change
   denial of HTTP requests essentially only permitting HTTPS requests 
   
    effect sets if the statement will allow or deny access e.g. Allow;
    principal is the user or account that the statement applies to e.g. awesome-user;
    action is the resource actions (e.g. s3:GetObject) in scope of the statement;
    the resource is the list of AmazonResourceNames (ARNs) of the objects. It is a long string that begins with arn:aws:s3:::\* e.g. arn:aws:s3:::my-stack-my-chicken-wings-bucket423e3a42f3-432f3j2;
    the condition is a property that states when the policy applies: in our case we want to deny access when the aws:SecureTransport is false;
    you can tag your statement to group resources which share the same tag e.g. "food-bucket".
   According to a forum on https://dev.to/slsbytheodo/enable-https-only-on-your-s3-buckets-36eg

