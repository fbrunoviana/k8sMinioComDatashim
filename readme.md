# Configurando Um volume do Minio no Kubernetes com Datashim 

## Como nasceu
Bom tive a necessidade de criar um volume em um pod, um pouco incomum, esse volume tinha que ser montado em um bucket no minio. 

Depois de muita pesquisa, encontrei um projeto chamado [Datashim](https://datashim-io.github.io/datashim/)


## Descrição:
> Nossa estrutura apresenta o Dataset CRD, que é um ponteiro para fontes de dados S3 e NFS existentes.

![](https://datashim-io.github.io/datashim/pictures/dlf.png)

## Passo a Passo
1. Ir em access-keys no minio e criar uma nova credencial.
2. Criar o namespace `kubectl create ns dlf`
3. Instalar a ferramenta `kubectl apply -f https://raw.githubusercontent.com/datashim-io/datashim/master/release-tools/manifests/dlf.yaml`
4. Criar o dataset `kubectl create 001-dataset.yaml` 
5. Criar o pod `kubectl create 002-pod.yaml`

Obs: se atentar que o volume usado no pod, tem que ter o mesmo nome do `dataset` 

```yaml
  volumes:
  - name: "guelo-dataset"
    persistentVolumeClaim:
      claimName: "guelo-dataset"
```