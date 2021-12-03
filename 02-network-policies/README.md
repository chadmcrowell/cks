# Network Policies

## Create two pods
```bash
kubectl run frontend --image nginx

kubectl run backend --image nginx
```

## Expose port 80 on the pod
```bash
kubectl expose po frontend --port 80

kubectl expose po backend --port 80
```

## communicate from frontend pod to backend pod
```bash
kubectl exec frontend -- curl backend

kubectl exec backend -- curl frontend
```

## create a deny-all network policy
```bash
kubectl apply -f netpol-default-deny.yml
```

## test network policy (it shouldn't work)
```bash
kubectl exec frontend -- curl backend

kubectl exec backend -- curl frontend
```

## create network policy to allow using podselector and labels
```bash
kubectl apply -f netpol-allow-backend-to-frontend.yml

kubectl apply -f netpol-allow-frontend-to-backend.yml
```

## test network policy again (it should work)
```bash
kubectl exec frontend -- curl backend

kubectl exec backend -- curl frontend
```