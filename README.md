# 🚀 memo-k8s-deploy

Spring Boot 기반 메모 애플리케이션(BE-memo-app)을 쿠버네티스 환경에 배포하기 위한 CI/CD 설정 저장소입니다.
Docker, Jenkins, Kubernetes(k3s), ArgoCD, GitOps를 활용하여 자동화된 배포 파이프라인을 구성하였습니다.

⸻

## 🌟 주요 특징

✅ GitOps 기반 자동 배포: Git 저장소 변경을 기반으로 ArgoCD가 자동으로 Kubernetes에 배포

✅ Jenkins CI/CD 파이프라인 연동: 코드 푸시 → 이미지 빌드 및 푸시 → CD 태그 전달 → GitOps 배포

✅ k3s 경량 클러스터 사용: 개인 서버에서 경량화된 쿠버네티스 운영

✅ Docker 이미지 버전 관리: 태그 기반의 이미지 이력 관리 및 안정적인 롤백

✅ Kustomize 지원: 환경별 설정을 분리하고 선언적으로 관리 가능

⸻

## 📁 저장소 구조
```bash
memo-k8s-deploy/
├── base/                      # 공통 배포 설정
│   ├── deployment.yaml        # Deployment 리소스 정의
│   ├── service.yaml           # Service 정의
│   └── kustomization.yaml     # Kustomize 설정
├── overlays/
│   └── production/            # 운영 환경 전용 설정
│       └── kustomization.yaml
└── README.md
```

⸻

## 📦 사용 기술 스택
| 구성 요소 | 기술 |
|------------|-------|
| CI 도구 | Jenkins |
| 배포 도구 | ArgoCD |
| 클러스터	k3s | k3s (경량 Kubernetes) |
| 이미지 저장소 | Docker Hub |
| 선언적 배포 | Kustomize |
| 컨테이너 | Docker |

⸻

## 🛠️ CI/CD 파이프라인 구성

### 🔁 배포 플로우

```text
[1] GitHub 코드 푸시 (BE-memo-app 저장소)
      ↓ Webhook
[2] Jenkins CI 파이프라인 실행
      ↓ Docker 이미지 빌드 및 Docker Hub 푸시
[3] Jenkins CD 파이프라인에서 memo-k8s-deploy의 Kustomize 설정 변경
      ↓ GitOps Repo 커밋
[4] ArgoCD가 GitOps Repo 변경을 감지하고 자동 배포
      ↓ k3s에 배포 완료
```

### 🔐 배포 이력 관리
- Docker 이미지에 태그를 부여하여 명확한 배포 이력 관리 가능
- 롤백 시 이전 태그의 이미지로 즉시 복원 가능
