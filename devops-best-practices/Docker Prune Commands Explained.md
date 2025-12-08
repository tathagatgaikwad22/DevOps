# Docker Prune Commands Explained

Docker environments get bloated fast—unused images, dead containers, orphaned volumes, and networks you never touch.  
If you don’t clean regularly, you end up wasting gigabytes and slowing down builds.

This guide breaks down each `docker prune` command with clear use cases and risks.

---

## 1. `docker system prune`

Removes:
- Stopped containers  
- Dangling images  
- Unused networks  
- Build cache  

### Command
```bash
docker system prune
```
Aggressive cleanup (removes all unused images)

docker system prune -a

Include volumes (⚠️ Be careful: removes unused volumes)

docker system prune -a --volumes

When to use

Disk space is bloated

You want a broad cleanup

You understand what will be deleted



---

2. docker image prune

Removes unused or dangling images.

Default (dangling images only)

docker image prune

Remove all unused images

docker image prune -a

When to use

You switch between projects often

Old images eat storage

You want a safe cleanup that avoids containers



---

3. docker container prune

Deletes stopped containers only.

docker container prune

When to use

You run many short-lived containers

CI/CD jobs leave behind temporary containers

You want a safe cleanup without touching running containers



---

4. docker volume prune

Removes all unused volumes.
⚠️ Risk: Volumes may contain persistent data. If you delete it, it’s gone.

docker volume prune

When to use

You’re absolutely sure the volume data is not needed

You're cleaning up after experiments or local environments



---

5. docker network prune

Removes unused networks.

docker network prune

When to use

You see a long list of networks you don’t use

Docker Compose projects left behind old networks



---

One-Liner Full Cleanup

This is the “wipe everything unnecessary” command:

docker system prune -a --volumes

⚠️ Understand exactly what it removes before running it.


---

Summary Table

Command	Purpose	Risk Level

docker system prune	General cleanup	Medium
docker system prune -a	Aggressive cleanup (images too)	High
docker image prune	Remove unused images	Low–Medium
docker container prune	Remove stopped containers	Low
docker volume prune	Remove unused volumes (data loss possible)	High
docker network prune	Remove unused networks	Low



---

Best Practices

Run docker system df to check what’s consuming space before pruning.

Avoid using prune commands blindly in shared servers.

Automate cleanup in local dev machines using cron or scheduled tasks.

Use tags wisely so you don’t accidentally delete needed images.


