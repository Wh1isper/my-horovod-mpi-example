# Horovod CPU-Only Case

This example shows how to run a cpu-only mpijob.

修改自 [https://github.com/kubeflow/mpi-operator/tree/master/examples/horovod](https://github.com/kubeflow/mpi-operator/tree/master/examples/horovod)

## How to Build Image

This example dockerfile is based on Horovod cpu only [dockerfile](https://raw.githubusercontent.com/horovod/horovod/master/Dockerfile.cpu), please build the image as follows:

```bash
docker build -t horovod:latest -f Dockerfile.cpu .
```

## Create Mpijob

The example mpijob is to run the horovod cpu-only example [tensorflow_mnist.py](https://raw.githubusercontent.com/horovod/horovod/master/examples/tensorflow_mnist.py).

```bash
kubectl create -f ./mytfminist.yaml
```

# 监控及结果
查看任务
```bash
kubectl get -o yaml mpijobs tensorflow-mnist
```

查看训练结果


```bash
PODNAME=$(kubectl get pods -l mpi_job_name=tensorflow-mnist,mpi_role_type=launcher -o name)
kubectl logs -f ${PODNAME}
```
