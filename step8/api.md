$minikube start   

เปิดการใช้งาน ingress ด้วย
$minikube addons enable ingress                          

เริ่มทำการ deploy 
$kubectl apply -f deployment.yaml 
deployment "api" created

$kubectl apply -f service.yaml   
service "api" created

$kubectl apply -f ingress.yaml 
ingress "api" created

$kubectl get deployment
NAME      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
api       3         3         3            0           16s

$kubectl get service
NAME         CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
api          10.0.0.207   <none>        80/TCP         14s
kubernetes   10.0.0.1     <none>        443/TCP        136d
webserver    10.0.0.22    <nodes>       80:30047/TCP   136d

$kubectl get ingress
NAME      HOSTS       ADDRESS          PORTS     AGE
hello     hello.api   192.168.99.100   80        15s

ทำการ map ip ใน /etc/host ด้วยนะ
จากนั้นทดสอบการ deploy ดังนี้

$curl hello.api/home
Hello World

เมื่อทุกอย่างเรียบร้อยก็ลบทิ้งซะ กลับบ้าน
$kubectl delete pods --all
$kubectl delete services --all
$kubectl delete deployments --all