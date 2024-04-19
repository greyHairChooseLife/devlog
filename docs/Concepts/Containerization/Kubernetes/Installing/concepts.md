---
hide:
title: '직접 설치에 수반되는 필수 개념들'
date: 2024-04-15
update:
---

## concepts

1. **kubeadm**

   - 공식 클러스터 생성/관리 도구

2. **kubespray**

   - 쿠버네티스 클러스터를 배포하는 오픈소스 프로젝트
   - 다양한 형식으로 쿠버네티스 클러스터 구성가능
   - **온프레미스에서 상용 서비스 클러스터 운영시 유용**
   - 다양한 CNI 제공 - p.60,61

3. CNI (Container Network Interface)

   - container간 통신을 지원하는 VxLAN (Pod Network라고도 부름)
   - 다양한 종류의 플러그인이 존재
     - flannel
     - calico
     - weavenet
