
docker-compose up --build -d

docker-compose up --build -d <nomes_services>

docker-compose -f <file.yml> up -d --build

docker build -f php/7.1-fpm/dockerfile -t joaorca/app .

docker build -f nginx/1.13/dockerfile -t joaorca/web .

docker build -f postgres/9.6/dockerfile -t joaorca/postgres .

docker volume create --driver=local joaorca-postgres-data

docker run -d --name joaorca-postgres -p 5432:5432 -v joaorca-postgres-data:/var/lib/postgresql/data joaorca/postgres

docker run -d --name joaorca-app --link joaorca-postgres:joaorca-postgres -v //c/projetos/docker-projects/www:/var/www joaorca/app

docker run -d --name joaorca-app -v //c/projetos/docker-projects/www:/var/www joaorca/app

docker run -d --name joaorca-web --link joaorca-app:app -p 80:80 joaorca/web
