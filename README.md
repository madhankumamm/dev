# How to host a static website on Amazon S3 and set up a CI/CD pipeline with GitHub Actions


Step 1: Create an S3 Bucket
1.	Sign in to the AWS Management Console and open the Amazon S3 console at Amazon S3 Console.
2.	Create a Bucket:
  •	Click on "Create bucket".
  •	Enter a unique bucket name (e.g., my-static-website-bucket).
  •	Choose a region close to you.
  •	Leave the default settings and click "Create bucket".
Step 2: Enable Static Website Hosting
1.	Open the Bucket:
  •	Click on the bucket name you just created.
2.	Enable Static Website Hosting:
  •	Go to the "Properties" tab.
  •	Scroll down to "Static website hosting" and click "Edit".
  •	Select "Enable".
  •	For "Index document", enter index.html.
  •	Click "Save changes".
Step 3: Upload Your Website Files
1.	Create a Basic HTML File:
  •	Create a file named index.html with necessary content:
  •	name="viewport" content="width=device-width, initial-scale=1.0">
  •	In the S3 console, go to the "Objects" tab.
  •	Click "Upload" and then "Add files".
  •	Select the index.html file you created and click "Upload".


Step 4: Make Your Bucket Public
1.	Disable Block Public Access:
  •	Go to the "Permissions" tab.
  •	Click "Edit" under "Block public access (bucket settings)".
  •	Uncheck all the options to prevent blocking public access.
  •	Click "Save changes".
2.	Add a Bucket Policy:
  •	Go to the "Permissions" tab.
  •	Scroll down to "Bucket policy" and click "Edit".
  •	Add the following policy to make your bucket public:
  •	Click "Save changes".
Step 5: Set Up CI/CD Pipeline with GitHub Actions
	
1.	Create a GitHub Actions Workflow File:
  •	In your GitHub repository, create a directory named  .github/workflows.
  •	Inside this directory, create a file named deploy.yml.
2.	Add the Workflow Configuration:
Add the following content to the deploy.yml file:

                     name: Deploy to S3
                    o	    jobs:
                    o	  deploy:
                    o	    runs-on: ubuntu-latest
                    o	    steps:
                    o	    - name: Checkout code
                    o	      uses: actions/checkout@v2
                    o	    - name: Configure AWS credentials
                    o	      uses: aws-actions/configure-aws-credentials@v1
                    o	      with:
                    o	        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
                    o	        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
                    o	        aws-region: us-east-1
                    o	
                    o	    - name: Sync files to S3
                    o	      run: |
                    o	        aws s3 sync . s3://my-static-website-demo1 --exclude ".git/*" –delete


3.	Add Secrets to GitHub:
  •	Go to your GitHub repository.
  •	Navigate to "Settings" > "Secrets and variables" > "Actions".
  •	Click on "New repository secret" and add the following secrets:
  •	AWS_ACCESS_KEY_ID: Your AWS access key ID.
  •	AWS_SECRET_ACCESS_KEY: Your AWS secret access key.


4.	Push Changes to GitHub:
  •	Commit and push the deploy.yml file to your repository:
git add .github/workflows/deploy.yml git commit -m "Add GitHub Actions workflow for S3 deployment" git push origin develop


5.	 Access Your Website
1.	Get the Website URL:
  •	Go to the "Properties" tab.
  •	Scroll down to "Static website hosting".
  •	Use the "Bucket website endpoint" URL to access your static website.
Summary
This guide covers the steps to create an S3 bucket, enable static website hosting, upload your website files, make the bucket public, set up a CI/CD pipeline with GitHub Actions, and access your website.

