Tags: [[__Cloud]], [[__DevOps]], [[__Distributed_computing]], [[__Infrastructure_Engineering]]
#Cloud #DevOps #DistributedComputing #DataEngineering 

# Introduction
Helpers is a functionality which allow us to insert variables into yaml files in a Helm chart.

We define those variables in the templates/helpers.tpl file:
```yaml
{{- define "hive-metastore.fullname" -}}
{{ .Release.Name }}-hive-metastore
{{- end -}}
```

And then, we can use them in other yaml files in the same chart:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ include "hive-metastore.fullname" . }}
spec:
  selector:
    app: {{ include "hive-metastore.fullname" . }}
  ports:
    - port: {{ .Values.hive.metastorePort }}
      targetPort: {{ .Values.hive.metastorePort }}
```