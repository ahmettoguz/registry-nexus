# Registry Nexus

<h2 id="system-startup">🚀 System Startup</h2>

- Create a new directory named `registry`.

```
mkdir registry
cd registry
```

- Clone project.

```
git clone https://github.com/ahmettoguz/registry-nexus
cd registry-nexus
```

- Switch version.

```
git checkout v1.0.0
```

- Create `.env` file based on the `.env.example` file with configurations.

```
cp .env.example .env
nano .env
```

- Create `network-registry` network if not exists.

```
docker network create network-registry
```

- Manage container.

```
docker stop                      container-nexus
docker rm                        container-nexus
docker volume rm                 volume-nexus
docker compose -p registry up -d service-nexus
docker logs -f                   container-nexus
```

- Get initial admin password and login.
```
docker container exec container-nexus cat /nexus-data/admin.password
```

- Generate secure password and change initial password.

```
docker run --rm alpine/openssl rand -base64 32
```

<br/>

<h2 id="contributors">👥 Contributors</h2>

<a href="https://github.com/ahmettoguz" target="_blank"><img width=60 height=60 src="https://avatars.githubusercontent.com/u/101711642?v=4"></a>

### [🔝](#top)
