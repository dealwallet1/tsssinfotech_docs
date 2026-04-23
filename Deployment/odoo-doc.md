#### Complete Odoo 19 Deployment Guide for K3s 

# Project Structure 

odoo-k3s/ 
├── 01-namespace.yaml 
├── 02-postgresql-pv.yaml 
├── 03-postgresql-secret.yaml 
├── 04-postgresql-deployment.yaml 
├── 05-postgresql-service.yaml 
├── 06-odoo-pv.yaml 
├── 07-odoo-deployment.yaml 
├── 08-odoo-service.yaml 
├── custom-addons/ 
│   └── your_custom_module/ 
│       
├── __init__.py 
│       
└── __manifest__.py 
└── README.md 



# Step 1: Create Project Directory 

mkdir -p ~/odoo-k3s/custom-addons 
cd ~/odoo-k3s 

# Create Namespace 

nano  namespace.yaml 

apiVersion: v1 
kind: Namespace 
metadata: 
name: odoo 

kubectl apply -f  namespace.yaml 

### PostgreSQL Setup (Local Database) 

# Create PostgreSQL Storage

nano postgresql-pv.yaml 

apiVersion: v1 
kind: PersistentVolume 
metadata: 
name: postgresql-pv 
namespace: odoo 
spec: 
capacity: 
storage: 10Gi 
accessModes: - ReadWriteOnce 
hostPath: 
path: /data/postgresql 
storageClassName: local-storage --- 
apiVersion: v1 
kind: PersistentVolumeClaim 
metadata: 
  name: postgresql-pvc 
  namespace: odoo 
spec: 
  accessModes: 
    - ReadWriteOnce 
  resources: 
    requests: 
      storage: 10Gi 
  storageClassName: local-storage 
 
 
# Create directory and apply: 
 
sudo mkdir -p /data/postgresql 
sudo chmod 777 /data/postgresql 
kubectl apply -f postgresql-pv.yaml 
 
 
# Create PostgreSQL Credentials 
 
nano postgresql-secret.yaml 
 
apiVersion: v1 
kind: Secret 
metadata: 
  name: postgresql-secret 
  namespace: odoo 
type: Opaque 
stringData: 
  POSTGRES_USER: odoo 
  POSTGRES_PASSWORD: odoo 
  POSTGRES_DB: postgres 
 
kubectl apply -f postgresql-secret.yaml 
 
 
 
# Deploy PostgreSQL 
 
nano postgresql-deployment.yaml 
 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  name: postgresql 
  namespace: odoo 
spec: 
  replicas: 1 
  selector: 
    matchLabels: 
      app: postgresql 
  template: 
    metadata: 
      labels: 
        app: postgresql 
    spec: 
      containers: 
      - name: postgresql 
        image: postgres:15 
        ports: 
        - containerPort: 5432 
        env: 
        - name: POSTGRES_USER 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_USER 
        - name: POSTGRES_PASSWORD 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_PASSWORD 
        - name: POSTGRES_DB 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_DB 
        - name: PGDATA 
          value: /var/lib/postgresql/data/pgdata 
        volumeMounts: 
        - name: postgresql-storage 
          mountPath: /var/lib/postgresql/data 
        resources: 
          requests: 
            memory: "512Mi" 
            cpu: "500m" 
          limits: 
            memory: "1Gi" 
            cpu: "1000m" 
      volumes: 
      - name: postgresql-storage 
        persistentVolumeClaim: 
          claimName: postgresql-pvc 
 
kubectl apply -f postgresql-deployment.yaml 
 
 
# Create PostgreSQL Service 
 
nano postgresql-service.yaml 
 
apiVersion: v1 
kind: Service 
metadata: 
  name: postgresql 
  namespace: odoo 
spec: 
  selector: 
    app: postgresql 
  ports: 
  - port: 5432 
    targetPort: 5432 
  type: ClusterIP 
 
kubectl apply -f postgresql-service.yaml 
 
 
 
 
 
 
# verify PostgreSQL is Running 
 
# Check pod status 
kubectl get pods -n odoo 
 
# Check logs (wait until you see "database system is ready to accept connections") 
kubectl logs -n odoo -l app=postgresql -f 
 
 
# Deploy Default Odoo 19 
 
# Create Odoo Storage 
 
nano  odoo-pv.yaml 
 
apiVersion: v1 
kind: PersistentVolume 
metadata: 
  name: odoo-data-pv 
  namespace: odoo 
spec: 
  capacity: 
    storage: 20Gi 
  accessModes: 
    - ReadWriteOnce 
  hostPath: 
    path: /data/odoo-data 
  storageClassName: local-storage --- 
apiVersion: v1 
kind: PersistentVolumeClaim 
metadata: 
  name: odoo-data-pvc 
  namespace: odoo 
spec: 
  accessModes: 
    - ReadWriteOnce 
  resources: 
    requests: 
      storage: 20Gi 
  storageClassName: local-storage 
 
# Create directory and apply: 
 
sudo mkdir -p /data/odoo-data 
sudo chmod 777 /data/odoo-data 
kubectl apply -f odoo-pv.yaml 
 
 
 # Deploy Default Odoo 
 
nano odoo-deployment.yaml 
 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  name: odoo 
  namespace: odoo 
spec: 
  replicas: 1 
  selector: 
    matchLabels: 
      app: odoo 
  template: 
    metadata: 
      labels: 
        app: odoo 
    spec: 
      containers: 
      - name: odoo 
        image: odoo:19.0 
        ports: 
        - containerPort: 8069 
        env: 
        - name: HOST 
          value: "postgresql" 
        - name: USER 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_USER 
        - name: PASSWORD 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_PASSWORD 
        volumeMounts: 
        - name: odoo-data 
          mountPath: /var/lib/odoo 
        resources: 
          requests: 
            memory: "1Gi" 
            cpu: "500m" 
          limits: 
            memory: "2Gi" 
            cpu: "2000m" 
        livenessProbe: 
          httpGet: 
            path: /web/database/selector 
            port: 8069 
          initialDelaySeconds: 120 
          periodSeconds: 30 
          timeoutSeconds: 10 
        readinessProbe: 
          httpGet: 
            path: /web/database/selector 
            port: 8069 
          initialDelaySeconds: 60 
          periodSeconds: 10 
          timeoutSeconds: 5 
      volumes: 
      - name: odoo-data 
        persistentVolumeClaim: 
          claimName: odoo-data-pvc 
 
kubectl apply -f odoo-deployment.yaml 
 
 
 
# Create Odoo Service 
 
nano odoo-service.yaml 
 
apiVersion: v1 
kind: Service 
metadata: 
  name: odoo 
  namespace: odoo 
spec: 
  selector: 
    app: odoo 
  ports: 
  - port: 8069 
    targetPort: 8069 
    nodePort: 30069 
  type: NodePort 
 
kubectl apply -f odoo-service.yaml 
 
 
 
 
Verify Default Odoo is Working 
 
# Check all pods are running 
kubectl get pods -n odoo 
 
# Check Odoo logs 
kubectl logs -n odoo -l app=odoo -f 
 
# Get your server IP 
ip addr show | grep "inet " 
 
# Access Odoo in browser 
# http://YOUR_SERVER_IP:30069 
 
 
 
 
# Create your first database: 
 
 Go to `http://YOUR_SERVER_IP:30069` 

 # Fill in the form: 
   - Master Password: `admin` (you can change this) 
   - Database Name: `odoo_db` 
   - Email: your email 
   - Password: your admin password 
   - Phone: optional 
   - Language: English 
   - Country: Your country 

   - Click "Create database" 
   - Wait 2-5 minutes for initialization 
 
 
 
 
# Prepare Custom Modules Directory 
 
# Create a test custom module 
mkdir -p ~/odoo-k3s/custom-addons 
 
 
 # Create ConfigMap for Custom Modules 

nano custom-addons-configmap.yaml 
  
apiVersion: v1 
kind: PersistentVolume 
metadata: 
  name: odoo-addons-pv 
  namespace: odoo 
spec: 
  capacity: 
    storage: 5Gi 
  accessModes: 
    - ReadWriteOnce 
  hostPath: 
    path: /data/odoo-custom-addons 
  storageClassName: local-storage --- 
apiVersion: v1 
kind: PersistentVolumeClaim 
metadata: 
  name: odoo-addons-pvc 
  namespace: odoo 
spec: 
  accessModes: 
    - ReadWriteOnce 
  resources: 
    requests: 
      storage: 5Gi 
  storageClassName: local-storage 
 
 
 
 
sudo mkdir -p /data/odoo-custom-addons 
sudo chmod 777 /data/odoo-custom-addons 
 
 
 
# Copy your custom modules 
 
sudo cp -r ~/odoo-k3s/custom-addons/* /data/odoo-custom-addons/ 
kubectl apply -f custom-addons-configmap.yaml 
 
 
 
# Update Odoo Deployment with Custom Addons 
 
nano odoo-deployment-with-addons.yaml 
 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  name: odoo 
  namespace: odoo 
spec: 
  replicas: 1 
  selector: 
    matchLabels: 
      app: odoo 
  template: 
    metadata: 
      labels: 
        app: odoo 
    spec: 
      containers: 
      - name: odoo 
        image: odoo:19.0 
        ports: 
        - containerPort: 8069 
        env: 
        - name: HOST 
          value: "postgresql" 
        - name: USER 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_USER 
        - name: PASSWORD 
          valueFrom: 
            secretKeyRef: 
              name: postgresql-secret 
              key: POSTGRES_PASSWORD 
        volumeMounts: 
        - name: odoo-data 
          mountPath: /var/lib/odoo 
        - name: odoo-custom-addons 
          mountPath: /mnt/extra-addons 
        command: ["/bin/bash"] 
        args: 
          - "-c" 
          - | 
            set -e 
            echo "Starting Odoo with custom addons..." 
            echo "Custom addons path: /mnt/extra-addons" 
            ls -la /mnt/extra-addons || echo "No custom addons found" 
            exec /entrypoint.sh odoo --addons-path=/usr/lib/python3/dist-packages/odoo/addons,/mnt/extra-addons --db_host=postgresql --db_user=$USER --db_password=$PASSWORD 
        resources: 
          requests: 
            memory: "1Gi" 
            cpu: "500m" 
          limits: 
            memory: "2Gi" 
            cpu: "2000m" 
        livenessProbe: 
          httpGet: 
            path: /web/database/selector 
            port: 8069 
          initialDelaySeconds: 120 
          periodSeconds: 30 
          timeoutSeconds: 10 
          failureThreshold: 5 
        readinessProbe: 
          httpGet: 
            path: /web/database/selector 
            port: 8069 
          initialDelaySeconds: 60 
          periodSeconds: 10 
          timeoutSeconds: 5 
          failureThreshold: 3 
      volumes: 
      - name: odoo-data 
        persistentVolumeClaim: 
          claimName: odoo-data-pvc 
      - name: odoo-custom-addons 
        persistentVolumeClaim: 
          claimName: odoo-addons-pvc 
 
kubectl apply -f odoo-deployment-with-addons.yaml 
 
 
 
# Install Custom Module in Odoo 
 
# Wait for pod to restart 
kubectl get pods -n odoo -w 
 
# Check logs to ensure no errors 
kubectl logs -n odoo -l app=odoo --tail=100 

 
In Odoo Web Interface 
 
1. Login to Odoo: `http://YOUR_SERVER_IP:30069` 
2. Go to Apps(top menu) 
3. Click Update Apps List (you might need to enable Developer Mode first) 
4. Remove the "Apps" filter and search for your module name 
5. Click Install 

# Safety Mechanisms (Module Failures Won't Break Odoo) 
# Key Safety Features Already Implemented: 
 
# Separate Storage Volumes: 
 
   - Database: `/data/postgresql` (isolated) 
   - Odoo data: `/data/odoo-data` (isolated) 
   - Custom modules: `/data/odoo-custom-addons` (isolated) 
 
 
 
 
### Testing Custom Module Safely 
 
# Check pod status before adding new module 
kubectl get pods -n odoo 

# Add new module to custom-addons directory 
sudo cp -r /path/to/new_module /data/odoo-custom-addons/ 

# Restart Odoo pod to load new modules 
kubectl rollout restart deployment/odoo -n odoo

# Watch for issues 
kubectl logs -n odoo -l app=odoo -f 

# If module has errors, remove it 
sudo rm -rf /data/odoo-custom-addons/bad_module 
kubectl rollout restart deployment/odoo -n odoo 

### Backup Strategy 

# Backup PostgreSQL database 
kubectl exec -n odoo deployment/postgresql -- pg_dump -U odoo postgres > backup_$(date +%Y%m%d).sql 

# Backup Odoo data 
sudo tar -czf odoo_data_backup_$(date +%Y%m%d).tar.gz /data/odoo-data 

# Backup custom addons 
sudo tar -czf custom_addons_backup_$(date +%Y%m%d).tar.gz /data/odoo-custom-addons 

### Troubleshooting Commands 

# View all resources 
kubectl get all -n odoo 

# Check pod details 
kubectl describe pod -n odoo -l app=odoo 

# Check logs 
kubectl logs -n odoo -l app=odoo --tail=200 

# Check PostgreSQL logs 
kubectl logs -n odoo -l app=postgresql --tail=100 

# Access Odoo pod shell 
kubectl exec -it -n odoo deployment/odoo -- /bin/bash 

# Access PostgreSQL shell 
kubectl exec -it -n odoo deployment/postgresql -- psql -U odoo 

# Delete and recreate everything (CAREFUL!) 
kubectl delete namespace odoo 

# Then start from Step 3 
Common Issues and Solutions 
Issue 1: Pod CrashLoopBackOff 
# Check logs 
kubectl logs -n odoo -l app=odoo --previous 
# Common causes: 
# - Database not ready: Wait 2-3 minutes 
# - Wrong credentials: Check secret 
# - Storage permission: Check /data directories have 777 permissions 
 
Issue 2: Custom Module Not Showing 
# Ensure module is in correct location 
sudo ls -la /data/odoo-custom-addons/ 
# Check Odoo sees the module 
kubectl exec -it -n odoo deployment/odoo -- ls -la /mnt/extra-addons 

# Update apps list in Odoo interface 
Issue 3: Module Installation Fails - The module will simply not install - Other modules and Odoo continue working - Check module dependencies in `__manifest__.py` - Check Odoo logs for specific error - Remove problematic module and restart 
sudo ls -la /data/odoo-custom-addons/ 


# Copy your_custom_module module to the host path 
sudo cp -r ~/odoo-k3s/custom-addons/your_custom_module /data/odoo-custom-addons/

# Verify the copy 
sudo ls -la /data/odoo-custom-addons/ 

# Check your_custom_module directory contents 
sudo ls -la /data/odoo-custom-addons/your_custom_module/ 

# Set ownership to Odoo container user (UID 101) 
sudo chown -R 101:101 /data/odoo-custom-addons/

# Set proper read permissions 
sudo chmod -R 755 /data/odoo-custom-addons/ 

# Verify permissions are correct 
sudo ls -la /data/odoo-custom-addons/ 

# Check if your_custom_module appears in pod's mount point 
kubectl exec -it deployment/odoo -n odoo -- ls -la /mnt/extra-addons/ 

# Check your_custom_module module files 
kubectl exec -it deployment/odoo -n odoo -- ls -la /mnt/extra-addons/your_custom_module/ 
 
 
 
 
 
 
 
 
 