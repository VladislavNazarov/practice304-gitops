# Практическая работа 304

## Helm и GitOps с Argo CD

В работе выполнено развёртывание приложения Kubernetes с использованием Helm и Argo CD.

### Helm

- Создан Helm chart для Practice 304.
- helm lint: 1 chart(s) linted, 0 chart(s) failed.
- Выполнен helm install: Revision 1.
- Выполнен helm upgrade с 1 до 2 реплик: Revision 2.
- Helm-версия приложения доступна через NodePort 30040.

### Argo CD

- Argo CD установлен в namespace argocd.
- Версия Argo CD: v3.5.5.
- GitHub: https://github.com/VladislavNazarov/practice304-gitops
- Application: practice304-gitops.
- Включены automated sync, prune и selfHeal.
- GitOps-версия приложения доступна через NodePort 30041.

### Проверка GitOps

В values.yaml replicaCount был изменён с 1 до 3 и отправлен в GitHub.
Argo CD автоматически синхронизировал Kubernetes без helm upgrade и kubectl apply.

Результат:

- Sync Status: Synced
- Health Status: Healthy
- Deployment: 3/3 replicas
- Git revision и Argo CD revision совпали.

### Проверка Self Heal

Deployment был вручную масштабирован до 1 реплики командой kubectl scale.
В Git оставалось replicaCount: 3.
Argo CD автоматически обнаружил расхождение и восстановил Deployment до 3/3.

Итоговая схема: Git -> Argo CD -> Kubernetes.
