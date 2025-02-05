# **Helm Debugging Guide: Common Mistakes I faced during this Project and How U can Avoid Them**

## **Introduction**
This guide covers common mistakes encountered while working with Helm charts, their causes, and how to fix them. It also includes methods to validate Helm templates before deploying them.

---

## **1. Error: `no template "microservices.fullname" associated with template "gotpl"`**

### **Cause:**
- Missing or incorrectly referenced template helper functions (e.g., `microservices.fullname`).
- `include` function is trying to call a helper template that does not exist.

### **Fix:**
- Ensure that `microservices.fullname` is defined in `_helpers.tpl`.
- NOTE: I faced this error because i unknowingly deleted '_helpers.tpl' file. so, makesure to not delete this file

### **Verification Commands:**
```sh
helm lint
helm template -f values.yaml ./chart --debug
```
---

## **2. Error: `nil pointer evaluating interface {}.port`**

### **Cause:**
- `.Values.service.port` is not defined in `values.yaml` or `custom-values.yaml`.

### **Fix:**
- Ensure `values.yaml` contains:
```yaml
service:
  port: 8080
```
- Use a default value in templates to avoid nil pointer errors:
```yaml
{{ .Values.service.port | default 8080 }}
```

### **Verification Commands:**
```sh
helm template -f values.yaml ./chart --debug
```
---

## **3. Error: `wrong type for value; expected string; got interface {}`**

### **Cause:**
- `service.type` was expected to be a string but was missing or incorrectly formatted.

### **Fix:**
- Define `service.type` in `values.yaml`:
```yaml
service:
  type: "ClusterIP"
```
- Ensure YAML formatting is correct.

### **Verification Commands:**
```sh
helm lint
helm template -f values.yaml ./chart --debug
```
---

## **4. Error: `nil pointer evaluating interface {}.enabled` (Autoscaling and Ingress)**

### **Cause:**
- `.Values.autoscaling.enabled` or `.Values.ingress.enabled` was referenced but not defined in `values.yaml`.

### **Fix:**
- Ensure `values.yaml` contains:
```yaml
autoscaling:
  enabled: false
ingress:
  enabled: false
```
- Modify templates to provide a default value:
```yaml
{{ .Values.autoscaling.enabled | default false }}
```

### **Verification Commands:**
```sh
helm lint
helm template -f values.yaml ./chart --debug
```
---

## **5. Error: `non-absolute URLs should be in form of repo_name/path_to_chart`**

### **Cause:**
- Running `helm install` with an incorrect chart reference.

### **Fix:**
- Use the correct chart reference when installing:
```sh
helm install -f email-custom-values.yaml emailservice ./microservice
```

### **Verification Commands:**
```sh
helm repo list  # Ensure repo is added
helm search repo chart-name  # Check if chart exists in repo
```
---

## **6. Best Practices to Avoid These Errors**
- **Use `helm lint` to validate syntax before applying.**
```sh
helm lint ./chart
```
- **Use `helm template` with `--debug` to inspect rendered templates.**
```sh
helm template -f values.yaml ./chart --debug
```
- **Ensure all necessary values are defined in `values.yaml`.**

By following these best practices, you can significantly reduce Helm chart errors and improve debugging efficiency.


