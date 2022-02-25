## 解决gcr.io无法下载的问题

```
#!/bin/base
# 这里修改为你docker仓库的根地址
YOUR_REG_NAME=ionio

images=(
   controller:v0.33.0
   kubeconfigwriter:v0.33.0
   git-init:v0.33.0
   entrypoint:v0.33.0
   nop:v0.33.0
   imagedigestexporter:v0.33.0
   pullrequest-init:v0.33.0
   workingdirinit:v0.33.0
   webhook:v0.33.0
)
for imageName in ${images[@]} ; do
    relName=gcr.io/tekton-releases/github.com/tektoncd/pipeline/cmd/$imageName
    docker pull $relName
    docker tag $relName $YOUR_REG_NAME/$imageName
    docker push $YOUR_REG_NAME/$imageName
done
docker pull gcr.io/google.com/cloudsdktool/cloud-sdk
docker tag  gcr.io/google.com/cloudsdktool/cloud-sdk $YOUR_REG_NAME/cloud-sdk
docker pull gcr.io/distroless/base
docker tag  gcr.io/distroless/base $YOUR_REG_NAME/base

docker push $YOUR_REG_NAME/cloud-sdk
docker push $YOUR_REG_NAME/base
```
