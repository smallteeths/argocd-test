# argocd-test

用于测试 Argo CD GitOps 同步的最小 Nginx Helm Chart。

## Argo CD 应用配置

| 字段 | 值 |
| --- | --- |
| Application Name | argocd-test |
| Project | default |
| Repository URL | https://github.com/smallteeths/argocd-test.git |
| Revision | main |
| Path | chart |
| Destination Cluster | https://kubernetes.default.svc |
| Namespace | argocd-test |

勾选 Auto-Create Namespace。可以选择 Automatic 同步，或先手动 Sync。

同步后访问 http://35.78.113.31:30880/ 。需要确保 TCP 30880 未被占用且安全组允许访问。

## 测试更新

修改 chart/values.yaml 的 message 为 `Hello from Argo CD! Version 2`，提交并推送。
Argo CD 同步后，配置校验值会触发 Pod 更新，刷新页面即可看到新文字。

```powershell
git add .
git commit -m "Add Argo CD test chart"
git push -u origin main
```

## 本地验证（需要 Helm）

```powershell
helm lint ./chart
helm template argocd-test ./chart --namespace argocd-test
```
