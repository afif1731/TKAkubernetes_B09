# TKAkubernetes_B09
## B (Install)
### Instalasi Kubectl
1. Download kubectl terbaru
```
curl.exe -LO "https://dl.k8s.io/release/v1.28.3/bin/windows/amd64/kubectl.exe"
```
2. Validasi biner. Download file checksum kubectl:
```
curl.exe -LO "https://dl.k8s.io/v1.28.3/bin/windows/amd64/kubectl.exe.sha256"
```
3. Validasi biner kubectl terhadap file checksum. Gunakan Command Prompt untuk membandingkan output CertUtil's secara manual dengan file checksum yang diunduh:
```
CertUtil -hashfile kubectl.exe SHA256
type kubectl.exe.sha256
```
Gunakan PowerShell untuk mengotomatiskan verifikasi menggunakan operator -eq untuk mendapatkan hasil True atau False
```
$(Get-FileHash -Algorithm SHA256 .\kubectl.exe).Hash -eq $(Get-Content .\kubectl.exe.sha256)
```

Tes untuk memastikan versi yang diinstall up to date:
```
kubectl version --client
```
### Instalasi Minikube
download dan jalankan installer untuk versi terbaru. Jika ingin menggunakan PowerShell, inputkan command:
```
New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
```
Tambahkan minikube.exe bianry ke PATH. Pastikan PowerShell berhalan sebagai Administrator:
```
New-Item -Path 'c:F\' -Name 'minikube' -ItemType Directory -Force
Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
```
Setelah installasi minikube sudah dilakukan, mulai kluster Kubernetes dengan command berikut:
```
cd C:\minikube
```
```
.\minikube start
```
Kalau sudah selesai install, masuk ke directory tempat kubectl sebelumnya (cd [directoryPathmu terserah di mana])
```
kubectl cluster-info
```
Outputnya nanti sekitaran
```
Kubernetes master is running at https://192.168.99.100:8443

kubernetes-dashboard is running at https://192.168.99.100:8443/api/v1/...

KubeDNS is running at https://192.168.99.100:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

## C (Pod)
buat file yaml via:
```
notepad WILSOOOONNNN_B09.yaml
```
masukkan ini:
```
apiVersion: v1
kind: Pod
metadata:
  name: wilsoooonnnn-b09
spec:
  containers:
  - name: nginx-container
    image: nginx
```
jalankan ini
```
kubectl apply -f WILSOOOONNNN_B09.yaml
```

Periksa lewat siini
```
kubectl get pods
```
Lihat logs pods via:
```
kubectl logs wilsoooonnnn-b09
```
expose pod
```
kubectl port-forward wilsoooonnnn-b09 8888:8080
```
buka terminal baru buat cek
```
curl localhost:8888
```

Hapus Pod menggunakan
```
kubectl delete pod wilsoooonnnn-b09
```
## C2 (Deploy)
jalankan command
```
kubectl create deployment biiiillllllll-b09 --image=knrt10/kubia --port=8080
```
expose
```
kubectl expose deploy biiiillllllll-b09 --type=LoadBalancer --name biiiillllllll-http
```
cek via:
```
kubectl get svc
```

hapus deploy
```
kubectl delete deploy biiiillll-b09
```

## D (Label)
edit file WILSOOOONNNN.yaml lama
```
notepad WILSOOOONNNN_B09.yaml
```
isinya masukkan ini
```
apiVersion: v1
kind: Pod
metadata:
  name: wilsoooonnnn-b09
  labels:
    creation_method: manual
    env: prod
    hotel: trivago
spec:
  containers:
  - image: knrt10/kubia
    name: kubia
    ports:
    - containerPort: 8080
      protocol: TCP
```
Create pods lewat ini
```
kubectl create -f WILSOOOONNNN_B09.yaml
```
lihat labels
```
kubectl get po --show-labels
```
lihat labels lagi
```
kubectl get po -L hotel
```
Tambahkan label baru
```
kubectl label po wilsoooonnnn-b09 nasi: kucing
```
overwrite label
```
kubectl label po wilsoooonnnn-b09 env=debug --overwrite
```

Menjadwalkan pod ke Nodes tertentu, buat file ADAAAAAMMMM_B09.yaml
```
notepad ADAAAAAMMMM_B09.yaml
```
isi ADAAAAAMMMM_B09.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: adaaaaammmm-b09
spec:
  nodeSelector:
    gpu: "true"
  containers:
  - image: luksa/kubia
    name: kubia
```
Jalanin dulu
```
kubectl create -f ADAAAAAMMMM_B09.yaml
```
cek via ini
```
kubectl get node -L gpu
```

## E (Annotation)
periksa pod sebelumnya
```
kubectl describe po adaaaaammmm-b09
```
tambahkan anotasi baru
```
kubectl annotate pod adaaaaammmm-b09 knrt10.github.io/someannotation="skibidi toilet"
```
periksa lagi
```
kubectl describe po adaaaaammmm-b09
```

## E2 (Namespace)
Listing namespace
```
kubectl get ns
```
listing namespace kube-system
```
kubectl get po -n kube-system
```
buat yaml namespace baru. EL_GATO_B09.yaml
```
notepad EL_GATO_B09.yaml
```
isi EL_GATO_B09.yaml
```
apiVersion: v1
kind: Namespace
metadata:
  name: elgato-b09
```
create dulu
```
kubectl create -f EL_GATO_B09.yaml
```
listing lagi
```
kubectl get ns
```

## F (Hapus Pod)
Hapus pod wilsoooonnnn
```
kubectl delete po wilsoooonnnn-b09
```

hapus namespace
```
kubectl delete ns elgato-b09
```

hapus all
```
kubectl delete all --all
```

## G (Replication dst whatever)
Menjaga pod tetap sehat dengan Liveness Probe. Buat file BIIIIILLLLLLLL_B09.yaml
```
notepad BIIIIILLLLLLLL_B09.yaml
```
isi BIIIIILLLLLLLL_B09.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: biiiiillllllll-b09
spec:
  containers:
  - image: knrt10/kubia-unhealthy
    name: kubia
    livenessProbe:
      httpGet:
        path:
        port: 8080  
```

## H (Secrets)
buat WILSOOOONNNN_B09.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: wilsoooonnnn-b09
spec:
  containers:
  - name: mycontainer
    image: nginx
    env:
    - name: SECRET_USERNAME
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: kambing
    - name: SECRET_PASSWORD
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: 12345
  restartPolicy: Never
```
Jalanin
```
kubectl create -f WILSOOOONNNN_B09.yaml
```
cek secret
```
kubectl get secrets
```
delete secret
```
kubectl delete secret my-secret
```

## I (Data Injections)
buat configmap ADAAAAAMMMM_B09.yaml
```
notepad ADAAAAAMMMM_B09.yaml
```
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: adaaaaammmm-b09
data:
  mykey: yangadabadaknya
  anotherkey: mereklain
```
```
kubectl create -f ADAAAAAMMMM_B09.yaml
```
buat pod baru dengan reference configmap, EL_GATO_B09.yaml
```
notepad EL_GATO_B09.yaml
```
```
apiVersion: v1
kind: Pod
metadata:
  name: el-gato-b09
spec:
  containers:
  - name: mycontainer
    image: nginx
    env:
      - name: MY_KEY
        valueFrom:
          configMapKeyRef:
            name: myconfigmap
            key: mykey
```
```
kubectl create -f EL_GATO_B09.yaml
```
periksa
```
kubectl get po el-gato-b09 -o yaml
```

## J (Volume)
buat file GATOEL_B09.yaml
```
notepad GATOEL_B09.yaml
```
```
apiVersion: v1
kind: Pod
metadata:
  name: gatoel-b09
spec:
  containers:
  - name: my-container
    image: nginx
    volumeMounts:
    - mountPath: /data
      name: my-volume
  volumes:
  - name: my-volume
    emptyDir: {}
```
jalanin jangan lupa
```
kubectl create -f GATOEL_B09.yaml
```

## K (Rolling update)
buat deployment LLLIIIB_B09.yaml
```
notepad LLLIIIB.yaml
```
isinya
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: llliiib-b09
spec:
  replicas: 3
  selector:
    matchLabels:
      app: trivago-app
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: trivago-app
    spec:
      containers:
      - name: my-container
        image: nginx
```
jalanin dulu
```
kubectl create -f LLLIIIB_B09.yaml
```

lakukan rolling update
```
kubectl set image deployment/llliiib-b09 my-container=nginx:v2
```

## L (jobs)
buat file BAKEDCAT_B09.yaml
```
apiVersion: batch/v1
kind: Job
metadata:
  name: bakedcat-b09
spec:
  completions: 10
  parallelism: 3
  template:
    spec:
      containers:
      - name: worker
        image: nginx
      restartPolicy: Never
```
jalankan
```
kubectl create -f BAKEDCAT_B09.yaml
```
periksa job
```
kubectl describe job bakedcat-b09
```
delete job
```
kubectl delete job bakedcat-b09
```

## M (Scaling)
Buat Deployment dulu
```
kubectl create deployment soonwill-b09 --image=knrt10/kubia --port=8080
```

Horizontal Scaling
```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: soonwill-b09-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: soonwill-b09
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80
```

Vertical Scaling
buat deployment baru dulu
```
kubectl create deployment maadaa-b09 --image=knrt10/kubia --port=8080
```

scalling vertical
```
kubectl scale deployment maadaa-b09 --replicas=3
```
