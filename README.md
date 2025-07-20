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

### Create npm Repositories

After launch registry, create npm repositories.
Create npm-hosted repository as hosted to be able to create own packages.
Create npm-proxy repository as proxy to be able to get packages from default remote repository.
Create npm-group repository as group to be able to manage both own and shared packages.

### Configuration
Modify `~/.npmrc` file with npm-group url.

```
registry=https://nexus-registry.micro-local.net/repository/npm-group
strict-ssl=false
```

Login npm registry.

```
npm login --registry https://nexus-registry.micro-local.net/repository/npm-group
```

Navigate to Security -> Realms.
Add `npm Bearer Token Realm` as active realm.


### Publish npm Package
Publish npm package to nexus registry with following command.

```
npm publish --registry https://nexus-registry.micro-local.net/repository/npm-hosted
```

### User Management

To be able to modify user access, for example think that there are 2 team as ui and ux and these teams should be able to change and view their repositories and not intercept each other.
So first create content selector with this expression for ux team.

```
path =~ "@ux.*"
```

Create privilige with type `repository content selectory` and format `npm`with actions: `browse read edit`.

Create role for that priviliage and create user for that role.

and this user will be able to interactwith just ux repo.

<br/>

<h2 id="contributors">👥 Contributors</h2>

<a href="https://github.com/ahmettoguz" target="_blank"><img width=60 height=60 src="https://avatars.githubusercontent.com/u/101711642?v=4"></a>

### [🔝](#top)
