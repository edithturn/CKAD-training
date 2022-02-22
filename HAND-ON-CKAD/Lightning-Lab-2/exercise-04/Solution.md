## **Problem**

Create a single ingress resource called ingress-vh-routing. The resource should route HTTP traffic to multiple hostnames as specified below:

The service video-service should be accessible on http://watch.ecom-store.com:30093/video

The service apparels-service should be accessible on http://apparels.ecom-store.com:30093/wear


Here 30093 is the port used by the Ingress Controller

## **Solution**

```bash
# Check where the appareles-services and video-service are exposed
kubectl get services
```
Create Ingress definition
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-vh-routing
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: watch.ecom-store.com
    http:
      paths:
      - path: /video
        pathType: Prefix
        backend:
          service:
            name: video-service
            port:
              number: 8080
  - host: apparels.ecom-store.com
    http:
      paths:
      - path: /wear
        pathType: Prefix
        backend:
          service:
            name: apparels-service
            port:
              number: 8080
```
```bash
# Create the yaml
kubectl apply -f ingress.yaml

# Check if the services are working
curl -v http://watch.ecom.store.com:30093/video
curl -v http://appareles.ecom.store.com:30093/wear
```