### Retag image in ECR with the AWS CLI
Check it [here](https://docs.aws.amazon.com/AmazonECR/latest/userguide/retag-aws-cli.html)
Use the batch-get-image command to get the image manifest for the image to retag and write it to an environment variable. In this example, the manifest for an image with the tag, latest, in the repository, amazonlinux, is written to the environment variable, MANIFEST.
```
MANIFEST=$(aws ecr batch-get-image --repository-name amazonlinux --image-ids imageTag=latest --query images[].imageManifest --output text)
```
Use the --image-tag option of the put-image command to put the image manifest to Amazon ECR with a new tag. In this example, the image is tagged as 2017.03.

* Note

If the --image-tag option is not available in your version of the AWS CLI, upgrade to the latest version. For more information, see Installing the AWS Command Line Interface in the AWS Command Line Interface User Guide.

```
aws ecr put-image --repository-name amazonlinux --image-tag 2017.03 --image-manifest "$MANIFEST"
```
Verify that your new image tag is attached to your image. In the output below, the image has the tags latest and 2017.03.

```
aws ecr describe-images --repository-name amazonlinux
```
