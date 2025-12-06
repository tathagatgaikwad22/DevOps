🐳 Docker Logs Troubleshooting Guide

Docker logs are your first line of defense when debugging failing containers. If you aren’t checking logs properly, you’re troubleshooting blind. This guide gives you actionable, real-world commands to diagnose issues fast.


---

📌 1. View Basic Logs

Use this when you simply want to see what the container printed.

docker logs <container_name>


---

📌 2. Follow Logs in Real Time

Watch logs as they’re generated — useful for debugging crashes that happen after requests or events.

docker logs -f <container_name>


---

📌 3. Limit the Log Output

Avoid scrolling through thousands of lines. Fetch only what matters.

Show logs only from the last 10 minutes:

docker logs --since 10m <container_name>

Show the last 100 lines:

docker logs --tail 100 <container_name>

You should rarely need more than this while debugging.


---

📌 4. Logs for Multi-Container Applications

When using Docker Compose, target a specific service:

docker compose logs -f <service_name>

To see logs from all services:

docker compose logs


---

📌 5. Debug Container Exit Codes

A non-zero exit code usually means the app crashed. Use this to inspect the container:

docker container inspect <container_name> --format='{{.State.ExitCode}}'

Then check the logs around the error using --since or --tail.


---

📌 6. Clean Up Noisy or Large Log Files

Docker stores logs in JSON format by default. If logs grow too large, consider:

Fixing overly verbose application logs

Configuring a different log driver (json-file, syslog, journald, etc.)

Using log rotation


Example: configure log rotation in docker-compose.yml:

logging:
  driver: "json-file"
  options:
    max-size: "10m"
    max-file: "3"


---

📌 7. Know Where Docker Stores Logs (Advanced)

On Linux, logs live here:

/var/lib/docker/containers/<container_id>/<container_id>-json.log

Useful when Docker CLI fails or you need manual inspection.


---

🚀 Conclusion

Troubleshooting Docker without logs is a waste of time.
Master these commands → cut debugging time drastically.
