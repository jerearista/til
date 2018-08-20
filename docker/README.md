# Docker stuff

- `docker inspect <instance>`
   [Inspect volume mounts](https://www.adelton.com/docs/containers/docker-inspect-volumes-mounts)
   - `docker inspect --format '{{ index .Volumes "/data" }}' test-mount`
   - `docker inspect --format '{{ range .Mounts }}{{ if eq .Destination "/data" }}{{ .Source }}{{ end }}{{ end }}' test-mount /tmp/test`
   - `docker inspect -f '{{ .Mounts }}' awx_task_1`
   - `docker inspect -f '{{ json .Mounts }}' awx_task_1 | python -m json.tool`
   - `docker inspect -f '{{ json .Mounts }}' awx_task_1 | jq
