# Installation

## 1. Clone the Linkwarden repository

```
$ git clone https://github.com/linkwarden/linkwarden.git
$ cd linkwarden
```

## 2. Configure the Environment Variables

Inside the ```/linkwarden``` folder, copy the ```.env``` file from above and make required changes to the contents inside it with ```nano .env```

Example ```.env``` contents:
```
NEXTAUTH_SECRET=VERY_SENSITIVE_SECRET
NEXTAUTH_URL=https://subdomain.domain.com/api/v1/auth
POSTGRES_PASSWORD=YOUR_POSTGRES_PASSWORD
```

## 3. Replace the compose file

Delete the original compose inside the ```/linkwarden``` folder with ```rm docker-compose.yml``` and then add my compose file in its place. Make changes to the domain in traefik labels.

## 4. Run

Run it with ```docker compose up -d```