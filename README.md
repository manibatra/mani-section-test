# Deploy a Next.js App on Section Tutorial

![workflow status](https://github.com/section/nextjs-tutorial/actions/workflows/workflows.yaml/badge.svg)

This repo holds the sample code for usage with the tutorials hosted on Section.io's documentations.

Refer to [Tutorials/Next](https://www.section.io/docs/tutorials/frameworks/next) for detailed instructions on deploying.

```bash
# Build and push next.js image
USER=section
IMAGENAME=nextdemo
TAG=0.0.1
GITHUB_TOKEN=<INSERT_TOKEN> # https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

docker build . --tag ghcr.io/$USER/$IMAGENAME:$TAG
docker run -it --rm -p 1337:3000 ghcr.io/$USER/$IMAGENAME:$TAG

echo $GITHUB_TOKEN | docker login ghcr.io -u $GITHUB_USER --password-stdin
docker push ghcr.io/$USER/$IMAGENAME:$TAG

# Deploy k8s yamls
# - Change image name in k8s/webapp-deployment.yaml if using your own image instead
kubectl apply -f ./k8s/
```
