# cloudformation-fun

This repository contains CloudFormation templates created for fun and to learn more about CloudFormation.

## Requirements

1. Create an S3 bucket that will contain all the `.yml` CloudFormation templates of this repository. You can then upload the templates by running:  

   ```bash
   aws s3 cp --recursive --exclude "*" --include "sns.yml" --include "codecommit.yml" . s3://YOURTEMPLATESBUCKET
   ```

   Make sure to replace `YOURTEMPLATESBUCKET` with the name of the bucket you just created.

2. Open the `parameters.json` file and replace the `CHANGEME` with the name of the bucket you just created.

3. OPTIONAL - Create an S3 bucket in which you will upload some ziped code that will be pushed to the CodeCommit repository created by this stack. You can do so by running this from within your code directory:  

   ```bash
   zip -r mycode.zip .
   aws s3 cp mycode.zip s3://YOURCODEBUCKET
   ```

   Make sure to replace `YOURCODEBUCKET` with the name of the bucket you just created.

4. If you did `step 3.`, then go ahead and populate `CodeCommitCodeBucket` with the bucket name and `CodeCommitCodeZipFile` with the zip file name into the `parameters.json` file.

## Deploy your stack

To deploy your stack, run the following command:

```bash
aws cloudformation create-stack --stack-name YOURSTACKNAME --template-body file://main.yml --parameters file://parameters.json
```

Make sure to replace `YOURSTACKNAME` with the name you choose for your stack. This name will be used through the nested stack to add prefixes.
