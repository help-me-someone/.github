# help-me-someone
> What one programmer can do in one month, two can do in two months.

This organization holds all the repositories for the `Scalable-p2 toktik` project.

Everything is written in Golang (for learning purposes).

The main repository for deploying can be found [here](https://github.com/help-me-someone/scalable-p2-orchestrator).

It holds the following structure:
```rust
├── components               // 
│  ├── scalable-p2-backend   // 
│  ├── scalable-p2-frontend  // Submodules.
│  ├── scalable-p2-user-svc  //
│  └── scalable-p2-worker    // 
├── docker
│  └── docker-compose.yml
├── k8s
│  ├── auth-deployment.yaml
│  ├── auth-svc.yaml
│  ├── backend-deployment.yaml
│  ├── backend-ingress.yaml
│  ├── backend-svc.yaml
│  ├── forward-auth-middleware.yaml
│  ├── frontend-deployment.yaml
│  ├── frontend-svc.yaml
│  ├── mysql-deployment.yaml
│  ├── mysql-pvc.yaml
│  ├── mysql-svc.yaml
│  ├── redis-deployment.yaml
│  ├── redis-svc.yaml
│  ├── set-cors-middleware.yaml
│  ├── strip-prefix-middleware.yaml
│  ├── worker-deployment.yaml
│  └── worker-svc.yaml
├── README.md
└── traefik.yaml
```

# Design
![alt text](https://github.com/help-me-someone/.github/blob/main/design.png?raw=true)

# Building

The following secrets are required.
```bash
kubectl create secret docker-registry ghcr-login-secret \
    --docker-server='...' \
    --docker-username='...' \
    --docker-password='...'

kubectl create secret generic aws-credentials \
    --from-literal='AWS_ACCESS_KEY_ID=...' \
    --from-literal='AWS_SECRET_ACCESS_KEY=...'

kubectl create secret generic db-secret \
    --from-literal='DB_NAME=...' \
    --from-literal='DB_USER=...' \
    --from-literal='DB_PASS=...' \
    --from-literal='DB_PORT=...' \
    --from-literal='DB_IP=...' \
    --from-literal='DB_ROOT_PASS=...'
```

cd into the `k8s` directory.

Set up the deployments and services.
```bash
kubectl apply -f .
```

Install traefik.
```bash
helm upgrade --install traefik traefik/traefik
```

Now you should be able to access the [login page](http://localhost/login).

# Pointless Venture (The presentation)
If you are interested in seeing the fruits of my pointless venture, check out the presentation [here](https://github.com/help-me-someone/pointless-venture).


