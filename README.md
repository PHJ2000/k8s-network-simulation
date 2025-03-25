# Kubernetes 기반 대규모 네트워크 혼잡 제어 시뮬레이션 프로젝트

본 프로젝트는 Kubernetes 클러스터 위에서 컨테이너 기반의 대규모 네트워크 환경을 구축하고, Java(Spring Boot) 기반 SDN(Software-Defined Networking) 컨트롤러를 활용하여 네트워크 혼잡 상황을 시뮬레이션 및 제어하는 것을 목표로 합니다.

---

## 📌 프로젝트 목표

- Kubernetes 클러스터 환경 구축
- Spring Boot 기반의 SDN 컨트롤러 서버 구현 및 배포
- Docker 컨테이너를 이용한 트래픽 노드 구성 및 확장
- Grafana 및 Prometheus를 활용한 실시간 네트워크 모니터링 구축
- 혼잡 상황 시나리오 구성 및 테스트 수행

---

## 🛠️ 기술 스택

| 구분 | 기술 |
|------|------|
| 컨테이너 환경 | Kubernetes(k3s), Docker |
| 백엔드 | Java 17, Spring Boot |
| SDN 구성 | Open vSwitch 또는 OpenLAN |
| 모니터링 | Prometheus, Grafana |
| 트래픽 시뮬레이션 | iperf3 |

---

## 📂 프로젝트 구조

```
.
├── README.md
├── backend
│   ├── Dockerfile
│   └── src (Spring Boot 프로젝트)
├── deployments
│   ├── controller-deployment.yaml
│   ├── traffic-node-deployment.yaml
│   └── services.yaml
├── monitoring
│   └── grafana-prometheus-stack (설치 및 설정 파일)
└── scripts
    └── traffic-simulation.sh
```

---

## 🚀 프로젝트 실행 절차

### 1. Kubernetes 환경 구성 (k3s)

```bash
curl -sfL https://get.k3s.io | sh -
kubectl get nodes
```

### 2. 컨테이너 이미지 빌드 및 배포

```bash
docker build -t [Your Docker Hub ID]/sdn-controller:latest ./backend
docker push [Your Docker Hub ID]/sdn-controller:latest
```

### 3. Kubernetes 클러스터에 배포

```bash
kubectl apply -f deployments/controller-deployment.yaml
kubectl apply -f deployments/traffic-node-deployment.yaml
kubectl apply -f deployments/services.yaml
```

### 4. 모니터링 환경 구성

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install monitoring prometheus-community/kube-prometheus-stack
```

### 5. 트래픽 시뮬레이션 테스트

```bash
kubectl exec -it [트래픽 생성 Pod 이름] -- iperf3 -c [대상 서비스 이름] -t 300
```

---

## 📊 모니터링

- Grafana 대시보드: `http://<Cluster_IP>:3000`

---

## 📌 버전 관리 및 기여 방법

본 프로젝트는 GitHub를 통해 버전 관리됩니다. 기능 추가 및 수정 사항은 새로운 브랜치를 생성하여 Pull Request로 제출해주세요.

```bash
git checkout -b feature/<기능 이름>
```

---

## 📝 라이선스

본 프로젝트는 MIT 라이선스를 따릅니다.

